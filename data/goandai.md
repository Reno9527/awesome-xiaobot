|名称|作者|读者数量|内容数量|创建时间|更新时间|
---
|[基于 Gin 封装的高效 Web 框架](https://xiaobot.net/p/goandai?refer=0b133df9-27dc-423b-8101-639049001c13)|@新亮|158人|44篇|2023-12-04|2024-02-20|

# 最近更新
## 5.6 示例二：集成登录、注册和用户管理功能缘起：有部分开发者提出了这样的需求：“亮哥，看了文档和源码后，我还是不知道如何下手，可以基于 gin-api-mono 集成下登录、注册和用户管理功能吗？”

于是就有它。

<strong>为了避免有些开发者不需要这些功能，我重新开了一个新项目去实现。</strong>

## 效果<img src="https://static.xiaobot.net/file/2024-02-20/8433/4907d9a81d7d137c7a6b733e09879d1c.jpeg">
## 操作流程<ol><li>初始化数据表时，请使用 README.md 文档中的表结构。
</li><li>项目启动与 gin-api-mono 一致，查看接口文档。
</li><li>操作「管理员注册」接口，创建数据。
</li><li>操作「管理员登录」接口，登录成功并获取 Token。
</li><li>在接口文档 Authorize 中配置 Token，可访问用户管理相关接口。
</li></ol>
获取源码，可添加我微信 <u>wx-xinliang </u>。
<hr class="xbt-hr">有启发，左下角点击“启发”告诉我呀，<a target="_blank" rel="noopener noreferrer nofollow" href="https://xiaobot.net/post/e9f7ef4c-81b1-4ffc-9053-bec55c3abb12"><u>点我即可直接跳转到小册目录合集 </u></a>。

## 3.6 包装 gin ContextContext 是一个上下文对象，它提供了许多有用的方法和属性，用于处理 HTTP 请求和响应。

代码片段：
// ./internal/pkg/core/con......
## 3.5 包装 gin IRoutesIRoutes 接口是定义路由组的接口。

IRoutes 接口包含了定义路由的方法，可以用于添加路由和中间件等。

代码片段：
// ./......
## 3.4 实现链路日志记录目前可收集日志类型包括：
<ol><li>当前的请求日志
</li><li>当前的响应日志
</li><li>自定义调试日志
</li><li>MySQL 操作日志
</li><li>Redis 操作信息
</li><li>Mongo 操作信息
</li><li>请求三方 API 接口的请求与响应日志
</li></ol>
日志收集，代码片段：
<pre><code>// ./internal/pkg/core/core.go

// region 记录日志
var t *trace.Trace
if x := context.Trace(); x != nil {
	t = x.(*trace.Trace)
} else {
	return
}

decodedURL, _ := url.QueryUnescape(ctx.Request.URL.RequestURI())

// ctx.Request.Header，精简 Header 参数
traceHeader := map[string]string{
	"Content-Type": ctx.GetHeader("Content-Type"),
}

t.WithRequest(&amp;trace.Request{
	TTL:        "un-limit",
	Method:     ctx.Request.Method,
	DecodedURL: decodedURL,
	Header:     traceHeader,
	Body:       string(context.RawData()),
})

var responseBody interface{}

if response != nil {
	responseBody = response
}

t.WithResponse(&amp;trace.Response{
	Header:          ctx.Writer.Header(),
	HttpCode:        ctx.Writer.Status(),
	HttpCodeMsg:     http.StatusText(ctx.Writer.Status()),
	BusinessCode:    businessCode,
	BusinessCodeMsg: businessCodeMsg,
	Body:            responseBody,
	CostSeconds:     time.Since(ts).Seconds(),
})

t.Success = !ctx.IsAborted() &amp;&amp; (ctx.Writer.Status() == http.StatusOK)
t.CostSeconds = time.Since(ts).Seconds()

logger.Info("trace-log",
	zap.Any("method", ctx.Request.Method),
	zap.Any("path", decodedURL),
	zap.Any("http_code", ctx.Writer.Status()),
	zap.Any("business_code", businessCode),
	zap.Any("success", t.Success),
	zap.Any("cost_seconds", t.CostSeconds),
	zap.Any("trace_id", t.Identifier),
	zap.Any("trace_info", t),
	zap.Error(abortErr),
)
// endregion</code></pre>
使用日志组件，代码片段：
<pre><code>// main.go

import "gin-api-mono/internal/pkg/logger"

// 将日志输出到文件
accessLogger, err := logger.NewJSONLogger(
	logger.WithField("domain", fmt.Sprintf("%s[%s]", configs.ProjectName, env.Active().Value())),
	logger.WithTimeLayout(timeutil.CSTLayout),
	logger.WithFileP(configs.ProjectAccessLogFile),
)

// 将日志输出到文件 + 控制台
accessLogger, err := logger.NewJSONLogger(
	logger.WithOutputInConsole(),
	logger.WithField("domain", fmt.Sprintf("%s[%s]", configs.ProjectName, env.Active().Value())),
	logger.WithTimeLayout(timeutil.CSTLayout),
	logger.WithFileP(configs.ProjectAccessLogFile),
)

// 如果需要日志分割，可以使用 WithFileRotationP() 方法。</code></pre>
记录自定义调试日志，代码片段：
<pre><code>import "gin-api-mono/internal/pkg/debug"

// 示例一，记录多个数据
debug.WithContext(ctx.RequestContext()).Logger("这是调试信息A1", "这是调试信息A2")

// 示例二，记录单个数据
debug.WithContext(ctx.RequestContext()).Logger("这是调试信息B")</code></pre>
记录 MySQL 操作日志，代码片段：
<pre><code>// 查询数据，核心是使用 .WithContext() 方法
h.db.GetDbR().WithContext(ctx.RequestContext()).Where(queryWhere).Find(&amp;resultData)</code></pre>
记录 Redis 操作日志，代码片段：
<pre><code>import "gin-api-mono/internal/repository/redis"

// get，核心是使用 ctx.RequestContext() 参数
getResult, err := redis.GetRedisClient().Get(ctx.RequestContext(), "name").Result()</code></pre>
记录 Mongo 操作日志，代码片段：
<pre><code>import "gin-api-mono/internal/repository/mongo"

// 获取 Mongo Client
client := mongo.GetMongoClient()

// 获取 Collection，例如 Database 为 gin_api_mono，Collection 为 user
collection := client.Database("gin_api_mono").Collection("user")

// 查询数据，核心是使用 ctx.RequestContext() 参数
findResult, err := collection.Find(ctx.RequestContext(), bson.D{})</code></pre>
记录请求三方 API 接口的日志，代码片段：
<pre><code>import "gin-api-mono/internal/pkg/httpclient"

// 支持在上下文记录执行日志的 httpclient
client := httpclient.GetHttpClientWithContext(ctx.RequestContext())

// 普通的 httpclient
client := httpclient.GetHttpClient()

// GET
resp, err := client.R().
      SetQueryParams(map[string]string{
          "page_no": "1",
          "limit": "20",
          "sort":"name",
          "order": "asc",
          "random":strconv.FormatInt(time.Now().Unix(), 10),
      }).
      SetHeader("Accept", "application/json").
      SetAuthToken("BC594900518B4F7EAC75BD37F019E08FBC594900518B4F7EAC75BD37F019E08F").
      Get("/search_result")</code></pre>
日志结构，代码片段：
<pre><code>// ./internal/pkg/trace/trace.go

// Trace 记录的参数
type Trace struct {
	mux                sync.Mutex
	Identifier         string     `json:"trace_id"`             // 链路ID
	Request            *Request   `json:"request"`              // 请求信息
	Response           *Response  `json:"response"`             // 返回信息
	ThirdPartyRequests []*HttpLog `json:"third_party_requests"` // 调用第三方接口的信息
	Debugs             []*Debug   `json:"debugs"`               // 调试信息
	SQLs               []*SQL     `json:"sqls"`                 // 执行的 SQL 信息
	Redis              []*Redis   `json:"redis"`                // 执行的 Redis 信息
	Mongos             []*Mongo   `json:"mongos"`               // 执行的 Mongo 信息
	Success            bool       `json:"success"`              // 请求结果 true or false
	CostSeconds        float64    `json:"cost_seconds"`         // 执行时长(单位秒)
}</code></pre>
不同组件能够将日志记录到上下文的核心是 <u>拦截器</u>，具体在第三方组件集成章节详细描述，此模块有些复杂，也可以微信找我沟通。
<hr class="xbt-hr">有启发，左下角点击“启发”告诉我呀，<a target="_blank" rel="noopener noreferrer nofollow" href="https://xiaobot.net/post/e9f7ef4c-81b1-4ffc-9053-bec55c3abb12"><u>点我即可直接跳转到小册目录合集 </u></a>。

## 3.3 实现错误处理与告警使用 IsAborted 函数来判断进行错误处理。

统一处理，代码片段：
// ./internal/pkg/core/core.go

// region 发生......
## 3.2 实现异常捕获与告警使用 defer 和 recover 函数来实现异常捕获与告警。defer 用于延迟函数的执行，recover 用于捕获 panic 异常并进行处理。

框架已经集成，代......
## 3.1 实现服务启动时可选的配置项使用 Options 设计模式实现，它可以让我们在服务启动时根据需要选择性地配置应用程序。

可配置项，代码片段：
<pre><code>// ./internal/pkg/core/core.go

type option struct {
	enablePProf      bool
	enableSwagger    bool
	enablePrometheus bool
	enableCors       bool
	alertNotify      proposal.AlertHandler
	recordHandler    proposal.RecordHandler
}

// WithEnablePProf 启用 pprof
func WithEnablePProf() Option {
	return func(opt *option) {
		opt.enablePProf = true
	}
}

// WithEnableSwagger 启用 swagger
func WithEnableSwagger() Option {
	return func(opt *option) {
		opt.enableSwagger = true
	}
}

// WithEnablePrometheus 启用 prometheus
func WithEnablePrometheus(recordHandler proposal.RecordHandler) Option {
	return func(opt *option) {
		opt.enablePrometheus = true
		opt.recordHandler = recordHandler
	}
}

// WithAlertNotify 设置告警通知
func WithAlertNotify(alertHandler proposal.AlertHandler) Option {
	return func(opt *option) {
		opt.alertNotify = alertHandler
	}
}

// WithEnableCors 设置支持跨域
func WithEnableCors() Option {
	return func(opt *option) {
		opt.enableCors = true
	}
}</code></pre>
服务启动，代码片段：
<pre><code>// ./internal/router/router.go

mux, err := core.New(logger,
	core.WithEnableCors(),
	core.WithEnableSwagger(),
	core.WithEnablePProf(),
	core.WithAlertNotify(alert.NotifyHandler()),
	core.WithEnablePrometheus(metrics.RecordHandler()),
)</code></pre>
通过使用 Options 设计模式，我们可以根据需要选择性地配置服务器参数，使得应用程序更加灵活和可扩展。
<hr class="xbt-hr">有启发，左下角点击“启发”告诉我呀，<a target="_blank" rel="noopener noreferrer nofollow" href="https://xiaobot.net/post/e9f7ef4c-81b1-4ffc-9053-bec55c3abb12"><u>点我即可直接跳转到小册目录合集 </u></a>。

## 2.3 配置管理与环境切换在 Go 项目中，配置管理和环境切换是一项重要的任务，用于将不同环境（如开发、测试、生产）的配置分离，并在运行时根据当前环境加载相应的配置。

以下是一种常见的方法来实现......
## 2.2 项目目录结构规划在 Go 中，使用清晰的项目结构是很重要的，可以提高代码的可读性、可维护性和可扩展性。

.
├── configs
├── docs
├── internal
│&nbsp;......
## 2.1 框架设计理念与目标框架设计理念和目标是提供简化和抽象的编程接口，使开发者能够更加高效和方便地构建应用程序。

主要涉及到几个方面：

提高开发效率：封装框架隐藏了复......

