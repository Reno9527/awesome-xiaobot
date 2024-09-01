|名称|作者|读者数量|内容数量|创建时间|更新时间|
---
|[Go 语言 与 AI 提效](https://xiaobot.net/p/golanginterview?refer=0b133df9-27dc-423b-8101-639049001c13)|@木川|566人|94篇|2023-07-30|2024-01-13|

# 最近更新
## Go 微服务 | 开源微服务框架 go-kratosKratos 是一个基于 Golang 实现的轻量级微服务框架，它提供了方便的功能来帮助您从零开始快速构建微服务。

Kratos 框架核心：主要包括基础CLI工具、HT......
## Go 微服务 | 开源微服务框架 go-zerogo-zero 是一个集成了各种工程实践的 web 和 rpc 框架。通过弹性设计保障了大并发服务端的稳定性，经受了充分的实战检验。

go-zero 包含极简的 API......
## Go 微服务 | 开源微服务框架 go-microGo Micro是一个插件化的基础框架，基于此可以构建微服务，Micro的设计哲学是可插拔的插件化架构

本文将演示如何从 0 到 1 使用 go-micro 框架实现 ......
## Go Web 开发 | Go 数据库连接 ORM在 Go 中进行数据库操作时，ORM（Object-Relational Mapping）库可以大大简化过程

ORM 允许开发者使用 Go 的结构体（structs）来......
## Go Web 开发 | Go 路由和中间件一、路由
使用 Go 的标准库，你可以通过 http.HandleFunc 或 http.Handle 函数来定义路由
http.HandleFunc("/articles",......
## Go Web 开发 | Go RESTful API 设计和实现一、什么是 RESTful API
RESTful API 是基于 REST（Representational State Transfer）架构风格的应用程序接口。它使用HTTP协......
## Go Web 开发 | Go 第 1 个 Web 程序Go 是一种强大的编程语言，特别适合于构建高效的网络应用程序。下面是创建一个基本的 Go Web 程序的步骤：

1、导入必要的包
2、编写一个处理器函数，用......
## AI 辅助阅读 | 阅读代码一般同事离职时，就会其它人补上，第一件要做的事情就是接手他写的代码

但阅读别人的代码，难不了心态爆炸，一看代码太长又繁琐，看不下去了

传统的方法不仅耗时长，而且效率低下，这时我想到了使用 AI 来辅助这一过程，简直太高效了，整个过程分三步走

<h1>一、AI 生成代码注释</h1>
同事的这段代码有 200 行，核心就是订单打包，比如 10 个订单聚类后生成 8 个包裹
聚类的细节太多，想着用 AI 提取并绘制流程图，更加直观

首先使用 AI 编程工具 Baidu Comate，解读这段代码

在函数代码上方，找到代码解释菜单

<img src="https://static.xiaobot.net/file/2023-12-20/263968/b6061cf4a313947f39a8be265791cf42.png">
点击代码注释，将会打开百度 AI 助手聊天框，显示代码的解读

<img src="https://fastly.jsdelivr.net/gh/muchuang1024/imgcdn/image-20231220125241086.png">
<h1>二、AI 生成流程图代码</h1>
代码可视化一般需要创建 UML 图，这样的工具有很多，从使用文本描述来生成 UML 图的角度，我选择的是 PlantUML

PlantUML 是一个强大的工具，用于快速创建多种类型的图表。这些图表广泛用于软件开发和文档编写中，以下是 PlantUML 支持的一些主要图表类型：

<ol><li><strong>序列图（Sequence Diagram）</strong>：用于展示对象之间交互的时间序列，常用于展示系统内部组件或对象之间的消息传递。
</li><li><strong>用例图（Use Case Diagram）</strong>：描述系统的功能和外部用户（参与者）之间的交互。
</li><li><strong>类图（Class Diagram）</strong>：展示系统中类的结构和类之间的关系，如继承、接口实现、依赖关系等。
</li><li><strong>活动图（Activity Diagram）</strong>：类似于流程图，用于展示从一个活动到另一个活动的控制流。
</li><li><strong>组件图（Component Diagram）</strong>：展示系统的组件如何组合在一起工作。
</li><li><strong>状态图（State Diagram）</strong>：展示一个对象在其生命周期内经历的状态以及状态间的转移。
</li><li><strong>对象图（Object Diagram）</strong>：类图的一个实例，显示了系统中对象之间的关系。
</li><li><strong>部署图（Deployment Diagram）</strong>：展示系统的物理部署，包括硬件和软件的配置。
</li><li><strong>时序图（Timing Diagram）</strong>：展示对象状态随时间的变化。
</li><li><strong>包图（Package Diagram）</strong>：展示代码的包结构，有助于理解代码的模块化组织。
</li><li><strong>组织结构图（Wireframe Graphic Interface）</strong>：用于描述图形用户界面的布局和元素。
</li><li><strong>甘特图（Gantt Diagram）</strong>：用于项目管理中，展示项目的时间线和进度。
</li></ol>
PlantUML 中的活动图就是流程图，左边是代码语法，右边是可视化图形

<img src="https://static.xiaobot.net/file/2023-12-20/263968/63675439f509a9072b281bb78dfc9451.png">
将步骤一种拿到的代码注释，询问 ChatGPT：<strong>请基于下面这段代码注释，生成 PlantUML 活动图代码</strong>

<img src="https://fastly.jsdelivr.net/gh/muchuang1024/imgcdn/image-20231220125558839.png">
<img src="https://static.xiaobot.net/file/2023-12-20/263968/be276240dfce76ac6091cbdf9dd0e3d0.png">
<h1>三、流程图可视化</h1>
将步骤二中生成的流程图代码，复制到 plantuml 可视化网站
网址： <a target="_blank" rel="noopener noreferrer nofollow" href="http://www.plantuml.com/plantuml">http://www.plantuml.com/plantuml</a>

<img src="https://static.xiaobot.net/file/2023-12-20/263968/ce649542aedfbe4bff4edfcf746cbff6.png">
点击 Submit 按钮，就可以获取到图片了

<img src="https://static.xiaobot.net/file/2023-12-20/263968/23aa06ca9d1ff962f8327011b9ae33d3.png">
看流程图就大概知道这段代码的含义了，AI 解读代码绘制流程图，真的很方便

<h1>四、总结</h1>
以上通过代码 -&gt; 注释 -&gt; 绘制流程图的方法是经过了三个步骤，实际上也可以直接让 AI 解读代码，获取到流程图，只需要两步就可以完成，但是效果可能不如先生成注释，再绘制流程图

毕竟代码生成注释，是通过专有代码大模型生成，相比 通用大模型 GPT 理解代码可能更加顺畅一些

最后分享一个小技巧：代码的可视化呈现方式有很多种，为什么必须是流程图，而不是其它类型的图，可以问 AI 这段代码生成什么图比较好，选择最优呈现方式可视化

比如基于上面的代码，我也可以生成类图

<img src="https://static.xiaobot.net/file/2023-12-20/263968/0305a059706dba5b4fd8e0e9ce775391.png">
## AI 辅助阅读 | 阅读文章阅读万字长文的时候通常需要比较多的时间，一万字的文章阅读时间取决于个人的阅读速度，通常成年人的平均阅读速度约为 200 到 300 字 /分钟。

如果以 250 字/分钟的平均速度来计算，阅读一万字的文章大约需要 40分钟，有什么办法能加速呢？

如果能通过 AI 提炼总结再阅读，可能只需要几分钟，能节省不少时间，本文将介绍电脑和手机两种场景下，如何借助 AI 阅读文章

<h1><strong>一、电脑操作</strong></h1>
直接将需要阅读的文章链接或文章内容发送给我做的「文章总结助手」即可
文章总结助手 GPTs：<a target="_blank" rel="noopener noreferrer nofollow" href="https://chat.openai.com/g/g-KyT4HyjP0-wen-zhang-zong-jie-zhu-shou">https://chat.openai.com/g/g-KyT4HyjP0-wen-zhang-zong-jie-zhu-shou</a>

## <strong>一）直接发送文章链接</strong>
<strong>文章标题</strong>：优秀程序员的习惯
<strong>文章链接</strong>： <a target="_blank" rel="noopener noreferrer nofollow" href="https://chat.openai.com/g/g-KyT4HyjP0-wen-zhang-zong-jie-zhu-shou">https://vadimkravcenko.com/shorts/habits-of-great-software-engineers/</a>

原文 1 万字，预计阅读需要 30 分钟，通过 AI 总结后，预计 5分钟可以完成阅读

根据 3 W 理论（What、How、Why）理论，将 AI 总结的内容主要分为三部分：

1、一句话总结：一句话概况下，文章讲了哪些内容（<strong>What</strong>）
2、关键信息点：文章中的关键点（<strong>How</strong>）
3、相关问题：文章中提到的原理（<strong>Why</strong>）

AI 总结：
<img src="https://static.xiaobot.net/file/2023-12-14/263968/f2ac770748f8234587b08d3b9c140c34.png">
## <strong>二）直接发送文章内容</strong>
<strong>文章标题</strong>：给职场人士的几大建议
<strong>文章内容</strong>：
<pre><code>1、要有弹性 

在职场中，绩效打低分，背黑锅，这些对个人来说，是挺委屈的，但是同事都会看在眼里。 

你能经受挫折，能抗住压力，也是一个优点。 

当然，这也不是任人捏圆搓扁，要有刚性，刚柔并济，把握一个度。 

在项目管理中也是，要保持弹性，不能光听别人的，也不能不听别人的。 

2、有机会，就争取，不要客气

客气，可能要不到机会，争取，就有机会，你选哪一个？ 

3、放下尊严，不要太在意脸面 

做自媒体 3 个原则，第一是坚持，第二是不要脸，第三是坚持不要脸。 

很多大 V ，挺有知识的，但是就是放不下脸面，去收费，怕跟粉丝对骂，怕这怕那的，就放弃了一年收入一两百万的机会。 

你矜持，你失去了好机会，是去了权益，最后还在叹悔，那你活该。 

在职场不要太矜持，创业也不能太矜持，特别是有能力、背景很好的人。 

4、换位思考 

当我们是员工，在职场汇报时，我们会比较在意我做了什么，解决了什么问题，会很强调自身的表现和贡献。 

当我们是老板，员工汇报的那些贡献都是不太关心的，更关心进度怎样，结果怎样，发展预期怎样，项目之间和团队之间有没有影响等等。 

换位思考，就是换维思考，你能从不同的维度看待问题。

5、在职场，向上沟通很重要

 这个，我也是经常跟我们团队的小伙伴说的，基本每次开会都会强调一次。 有想法，有什么问题，都可以主动跟我聊。 

你不主动跟你领导聊，你领导怎么会知道你的想法，怎么会了解你呢？ 

如果有机会，会找你吗？ 

肯定不会，肯定找经常找他聊的。 

6、深究一步 

差不多就行的心态，会错过重点，很多小问题，不能放过去。 

7、学会提问 

tk 教主的搜索能力很强，搜索能力，就是向搜索引擎提问的能力，意味着提问能力很强。 

学会提问很重要。 

曹大出了一个面试题，有一个数据库的故障，现在系统挂了，我是一个初级的操作员，你要向我问问题，每个问题我都会告诉你操作后的答案，看你问我几个问题，能问到故障的原因。 

通过提问，你能准确地把握住问题的本质是什么。</code></pre>
<strong>AI 总结</strong>：

<img src="https://static.xiaobot.net/file/2023-12-14/263968/b0d7cbfb8220fa5f0ee60b44b8aca23b.png">
<h1><strong>二、手机操作</strong></h1>
直接将需要阅读的文章链接发送给企业微信「知了助手」即可

1、关注公众号「知了阅读 ReadKnown」
2、添加好友 「知了阅读助手」：关注公众号会自动发送名片

不过需要注意的是：这个助手只支持文章链接，不支持文章内容总结

这里演示发送一个公众号文章链接，可以分析原文内容 2000 多字，需要 3 分钟 阅读完成，通过 AI 总结下，不到 1 分钟可以阅读完成

<strong>文章标题</strong>：简历优化案例分析，提升面试邀约率
<strong>文章链接</strong>：<a target="_blank" rel="noopener noreferrer nofollow" href="https://mp.weixin.qq.com/s/cf_5M5zr4wjhtvDbILC_8Q">https://mp.weixin.qq.com/s/cf_5M5zr4wjhtvDbILC_8Q</a>

<img src="https://static.xiaobot.net/file/2023-12-14/263968/bd1027d82b126c2379f466f881b58a75.png">
文本效果：默认就是文字总结效果

<img src="https://static.xiaobot.net/file/2023-12-14/263968/bab57594f3668d28416bc0daa6ba4bb1.png"><img src="https://static.xiaobot.net/file/2023-12-14/263968/25c55d00c4e21884b0c62c76357a7c7b.png">
卡片效果：查看导图默认是卡片效果

<img src="https://static.xiaobot.net/file/2023-12-14/263968/bf66d7b7c0d954f06287dcdc9acbe043.png">
思维导图效果：可点击下面的思维导图按钮切换到思维导图效果

<img src="https://static.xiaobot.net/file/2023-12-14/263968/8283161dda695adaf785b650f83b787b.png"><h1></h1><h1>三、总结</h1>
为了节省时间，建议使用 AI 工具来提取文章的关键信息和总结。文中介绍了在电脑和手机两种场景下如何使用 AI 来阅读文章。

对于电脑用户，可以通过发送文章链接或内容给“文章总结助手”GPTs 来获取文章的 AI总结。

对于手机用户，文章建议使用“知了助手”，一个企业微信应用，发送文章链接获取AI总结。

以上内容有启发左下角点击【有启发】告诉我呀，<a target="_blank" rel="noopener noreferrer nofollow" href="https://xiaobot.net/post/68f482c7-b801-4474-a6ad-fc7512df357d">点我可直接跳转小册专栏合集</a>。

## AI 辅助阅读 | 分析数据给你 一个 Excel 数据，你能从中得出什么结论吗？这需要一定的数据分析能力，比如

1、统计分析，计算某项指标的均值、分位数、标准差等
2、相关性分析，比......

