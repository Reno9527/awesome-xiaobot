# 基于 Gin 封装的高效 Web 框架_小报童_Awesome_XiaoBOT

## 基于 Gin 封装的高效 Web 框架介绍
> 从零开始教你如何基于 Gin 框架封装自己的 Web 框架，涵盖框架设计与实现。无论你经验水平如何，都可获得实际项目开发技巧，提高开发效率。    
    
相比于我的开源项目 go-gin-api（GitHub 5.4K  
Star），此框架去掉了一些集成的功能和界面，使得整个框架更加简洁、轻量。此外也对代码进行了升级以确保性能和稳定性。开发者就可以更灵活地选择所需的功能，并获得更好的性能和稳定性。    
    
原价 199 元，限时特惠，只需 59.9 元。    
    
买过后，从置顶帖【目录合集】加微信，发源码 + 进交流群。  
  


|名称|作者|读者数量|内容数量|更新时间|
|---|---|---|---|---|
|[基于 Gin 封装的高效 Web 框架](https://xiaobot.net/p/goandai?refer=0b133df9-27dc-423b-8101-639049001c13)|新亮|202人|49篇|2024-11-22|

## 最近更新
### 5.7 自动化生成 model、dao、handler、routers 以及 Swagger 接口文档

### 1\. 生成 model、dao

示例：

    
    
    # 根目录下执行  
    go run cmd/gormgen/main.go -dsn "root:123456789@tcp(127.0.0.1:3306)/gin_api_mono？charset=utf8mb4&parseTime=True&loc=Local" -tables "admin"

**具体文档：cmd/gormgen/**[**README.md**](http://README.md)

### 2\. 生成 handler、routers

示例：

    
    
    # 根目录下执行  
    go run cmd/handlergen/main.go -table "admin"

**具体文档：cmd/handlergen/**[**README.md**](http://README.md)

### 3\. 生成 Swagger 接口文档

    
    
    # 根目录下执行
    ./scripts/swagger.sh

### 4\. 注册路由

    
    
    // 定义自动生成的路由组前缀为 /api
    generatedRouterGroup := mux.Group("/api")  
    // 注册路由  
    admin.RegisterGeneratedAdminRoutes(logger, db, generatedRouterGroup)

**文件地址：internal/router/router.go**

### 5\. 重启项目

项目重启后访问：<http://127.0.0.1:9999/swagger/index.html> 会看到生成的接口文档。

![](https://static.xiaobot.net/file/2024-11-22/8433/80ed57e7a47604a3374b4763e175ae10.png)

获取源码，可添加我微信 wx-xinliang 。

* * *

有启发，左下角点击“启发”告诉我呀，[
_点我即可直接跳转到小册目录合集_](https://xiaobot.net/post/e9f7ef4c-81b1-4ffc-9053-bec55c3abb12)。

### 6.10 用 Go 写了一个桌面程序，源码免费分享给大家

用 Go 写了一个桌面程序：生成授权码的小工具，先看下效果。

我已经安装到 macOS 上了。

源码地址：jazr2......

### 6.9 mongo-driver 完整用法与示例代码

1\. 安装 mongo-driver

可以使用以下命令进行安装：

go get go.mongodb.org/mongo-driver/mongo

2\. 基本连接与配置

Mo......

### 6.8 go-redis/redis 完整用法与示例代码

1\. 安装 go-redis

可以使用以下命令安装：

go get github.com/go-redis/redis/v8

2\. 基本连接

你可以通过 redis.NewC......

### 6.7 go-resty/resty 完整用法与示例代码

1\. 安装

可以通过以下命令安装：

go get github.com/go-resty/resty/v2

2\. 创建一个简单的 HTTP 客户端

通过 resty.New(......

### 5.6 示例二：集成登录、注册和用户管理功能

缘起：有部分开发者提出了这样的需求：“亮哥，看了文档和源码后，我还是不知道如何下手，可以基于 gin-api-mono 集成下登录、注册和用户管理功能吗？”

于是就有它......

### 3.6 包装 gin Context

Context 是一个上下文对象，它提供了许多有用的方法和属性，用于处理 HTTP 请求和响应。

代码片段：

// ./internal/pkg/core/con......

### 3.5 包装 gin IRoutes

IRoutes 接口是定义路由组的接口。

IRoutes 接口包含了定义路由的方法，可以用于添加路由和中间件等。

代码片段：

// ./......

### 3.4 实现链路日志记录

目前可收集日志类型包括：

  1. 当前的请求日志

  2. 当前的响应日志

  3. 自定义调试日志

  4. MySQL 操作日志

  5. Redis 操作信息

  6. Mongo 操作信息

  7. 请求三方 API 接口的请求与响应日志

日志收集，代码片段：

    
    
    // ./internal/pkg/core/core.go
    
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
    
    t.WithRequest(&trace.Request{
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
    
    t.WithResponse(&trace.Response{
    	Header:          ctx.Writer.Header(),
    	HttpCode:        ctx.Writer.Status(),
    	HttpCodeMsg:     http.StatusText(ctx.Writer.Status()),
    	BusinessCode:    businessCode,
    	BusinessCodeMsg: businessCodeMsg,
    	Body:            responseBody,
    	CostSeconds:     time.Since(ts).Seconds(),
    })
    
    t.Success = !ctx.IsAborted() && (ctx.Writer.Status() == http.StatusOK)
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
    // endregion

使用日志组件，代码片段：

    
    
    // main.go
    
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
    
    // 如果需要日志分割，可以使用 WithFileRotationP() 方法。

记录自定义调试日志，代码片段：

    
    
    import "gin-api-mono/internal/pkg/debug"
    
    // 示例一，记录多个数据
    debug.WithContext(ctx.RequestContext()).Logger("这是调试信息A1", "这是调试信息A2")
    
    // 示例二，记录单个数据
    debug.WithContext(ctx.RequestContext()).Logger("这是调试信息B")

记录 MySQL 操作日志，代码片段：

    
    
    // 查询数据，核心是使用 .WithContext() 方法
    h.db.GetDbR().WithContext(ctx.RequestContext()).Where(queryWhere).Find(&resultData)

记录 Redis 操作日志，代码片段：

    
    
    import "gin-api-mono/internal/repository/redis"
    
    // get，核心是使用 ctx.RequestContext() 参数
    getResult, err := redis.GetRedisClient().Get(ctx.RequestContext(), "name").Result()

记录 Mongo 操作日志，代码片段：

    
    
    import "gin-api-mono/internal/repository/mongo"
    
    // 获取 Mongo Client
    client := mongo.GetMongoClient()
    
    // 获取 Collection，例如 Database 为 gin_api_mono，Collection 为 user
    collection := client.Database("gin_api_mono").Collection("user")
    
    // 查询数据，核心是使用 ctx.RequestContext() 参数
    findResult, err := collection.Find(ctx.RequestContext(), bson.D{})

记录请求三方 API 接口的日志，代码片段：

    
    
    import "gin-api-mono/internal/pkg/httpclient"
    
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
          Get("/search_result")

日志结构，代码片段：

    
    
    // ./internal/pkg/trace/trace.go
    
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
    }

不同组件能够将日志记录到上下文的核心是 _拦截器_ ，具体在第三方组件集成章节详细描述，此模块有些复杂，也可以微信找我沟通。

* * *

有启发，左下角点击“启发”告诉我呀，[
_点我即可直接跳转到小册目录合集_](https://xiaobot.net/post/e9f7ef4c-81b1-4ffc-9053-bec55c3abb12)。

### 3.3 实现错误处理与告警

使用 IsAborted 函数来判断进行错误处理。

统一处理，代码片段：

// ./internal/pkg/core/core.go // region 发生......


<a href="https://github.com/Reno9527/awesome-xiaobot" style="color: white; text-decoration: none;">awesome-xiaobot</a>

返回 [首页](../README.md)
