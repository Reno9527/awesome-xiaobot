# .NET 内网实战攻防_小报童_Awesome_XiaoBOT

## .NET 内网实战攻防介绍
> 我们创办的dot.Net安全矩阵知识库，已成为国内最大的.NET安全社区，如今开设.NET内网实战攻防报刊。内容主要有.NET在各个内网渗透阶段与Windows系统交互的方式和技巧，可细分为以下8个方向：\n1）  
.NET 安全防御绕过、本地权限提升\n2） .NET 内网信息收集、代理通道、横向移动\n3） .NET  
目标权限维持、数据传输外发、痕迹清理\n原价899，现在限时只需59元，永久买断！每增加五十人涨价10元，抓紧订阅！订阅后请关注公众号：dotNet安全矩阵，发送订单截图和您的微信号，邀请您加入专属交流群  
  


|名称|作者|读者数量|内容数量|更新时间|
|---|---|---|---|---|
|[.NET 内网实战攻防](https://xiaobot.net/p/dotNetAttack?refer=0b133df9-27dc-423b-8101-639049001c13)|ken|248人|23篇|2024-10-28|

## 最近更新
### .NET 通过指定的COM接口执行命令绕过UAC

在Windows操作系统中，UAC（用户帐户控制）机制用于防止未经授权的程序以管理员权限执行操作，从而增加系统安全性。然而，特定的系统组件和接口，例如
CMSTPLUA 组件中的 ICMLuaU......

### .NET 通过调用API接口模拟实现PowerShell

在红队内网渗透中，PowerShell 常常被用于执行各种任务，然而也常常受到安全工具的监控。因此，寻找和开发一个能够有效规避检测的 PowerShell
替代工具是非常有意义的。本文将介绍一种......

### .NET 通过白名单文件反序列化漏洞绕过UAC

在渗透测试和红队活动中，权限提升是重要的一环，尤其是在没有管理员权限的情况下执行更高权限的操作。有一种思路利用 Windows 事件查看器
(eventvwr.msc) 的高权限加载特性和 XA......

### .NET 通过第三方库批量读取Word敏感数据

借助 Microsoft.Office.Interop.Word 和 Marshal.GetActiveObject，红队可以自动化地读取
Microsoft Word 文档内容。这一技术使红队......

### 不安全的令牌特权 - SeImpersonatePrivilege (2)

在 Windows 系统中，某些权限对于进程的操作至关重要，特别是在进行进程间通信或执行特权操作时。下面将详细解析一个 C# 类
PrivilegeChecker，其主要功能是检查当前进程是否具......

### 不安全的令牌特权 - SeImpersonatePrivilege (1)

在 Windows
操作系统中，用户和进程可以拥有不同的权限，这些权限控制着能够执行的操作范围。如果当前进程获取到本地用户或者系统服务账户启用了一些不安全的权限，那么有可能会完成权限提升。SeI......

### .NET 白名单文件通过反序列化执行系统命令

在日常的红队行动中，利用微软签名的白名单文件来绕过防护措施是一种常见的行为，有些场景下红队通过利用系统白名单文件加载反序列化漏洞的方式执行恶意指令。

0x01 VisualU......

### .NET 通过Fsharp执行命令绕过安全防护

这是一个基于 F# 语言的红队工具，使用 F# 交互式编译器来执行攻击负载。Fsi.exe 是一个包含在 Visual Studio 中的
Microsoft 签名的合法二进制文件，允许通过交互......

### .NET 通过命令行解密web.config配置

在.NET应用系统中，保护数据库连接字符串的安全性至关重要。.NET 提供了一种通过 DataProtectionConfigurationProvider
加密连接字符串的方法，以防止敏感数据......

### .NET 通过执行XOML文件代码绕过安全防护

WFC.exe是一款工具，用于执行嵌入在XOML中的.NET代码。由于该程序自带微软的数字签名，它能够绕过杀毒软件的监控，执行潜在的恶意代码。该技术利用了XOML的合法性以及系统中对白名单程序的......


<a href="https://github.com/Reno9527/awesome-xiaobot" style="color: white; text-decoration: none;">awesome-xiaobot</a>

返回 [首页](../README.md)
