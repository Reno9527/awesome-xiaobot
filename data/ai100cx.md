# 100个AI创业小项目解析_小报童_Awesome_XiaoBOT

## 100个AI创业小项目解析介绍
> 在中国，2023-2024人工智能（AI）风起云涌，无数创新者加入这个赛道。本专栏将深度解析100个落地的AI创业项目，与创始人进行深度采访，旨在形成AI创新社群，共同进步。\n\n作为本专栏的作者，我将不仅跟踪并解析这些项目，还将与项目创始人进行深度交流，探讨他们的初心、困惑、成功与失败。重点关注这些项目的商业模式、盈利路径以及在中国市场的实际运营情况。\n\n如果你也是一个AI创新者或未来计划在AI领域创业，可以加入我们一起探讨，研究，前进。  
  


|名称|作者|读者数量|内容数量|更新时间|
|---|---|---|---|---|
|[100个AI创业小项目解析](https://xiaobot.net/p/ai100cx?refer=0b133df9-27dc-423b-8101-639049001c13)|AI人金伟|9人|11篇|2024-06-11|

## 最近更新
### 创新！一个中医大模型项目分析

  * 如果有人训练了一个中医大模型，你感觉会怎么样？ 2023-2024年我跟踪了100多个AI项目，现在这些项目发展情况怎么样？今天来分享一个中医大模型开源项目。

![](https://static.xiaobot.net/file/2024-06-11/580209/ea5594469e836d9264e4581d7dba7092.jpeg)

  * 全部项目，资料，测评移步 自学AI网 [xuechatgpt.com](http://xuechatgpt.com)

2024创业创新社群已有100人，请你加入：

![](https://static.xiaobot.net/file/2024-06-11/580209/281ca083e91c5f0c74d52e6473726fd5.png)

# **项目介绍**

这是一个学院派的项目，基于已知开源的若干大模型，针对中医场景做了一个大模型，名字叫”本草“大模型，github的star数也达到了4k多，非常有影响力，主要给相关领域的开发者提供了一个基础的研究模型。

下面是他们自己的项目介绍：

![](http://api1024.oss-cn-
shanghai.aliyuncs.com/xuegpt/WechatIMG2427.jpg?x-oss-
process=image/resize,w_800)

该项目核心有两点，1是基于各种开源公用大模型训练出不同的版本，2是针对医疗场景做了相应的数据集，微调了开源大模型在医疗领域的效果，给相关领域的研究者提供了一个范本。

项目开始时间非常早，大概为2023年3月，更新到2023年9月发表论文之后，没有新的更新，是一个典型的学院派研究项目。

# **模型训练**

该模型的训练方面，有两个特点，分别是：1，用GPT创建医疗领域问答数据集；2，训练了所有基模型版本的医疗模型

#### **1\. 基模型**

  * [活字1.0](https://github.com/HIT-SCIR/huozi)，哈尔滨工业大学基于Bloom-7B二次开发的中文通用问答模型

  * [Bloom-7B](https://huggingface.co/bigscience/bloomz-7b1) huggingface提供的基模型

  * [Alpaca-Chinese-7B](https://github.com/ymcui/Chinese-LLaMA-Alpaca)，基于LLaMA二次开发的中文问答模型

  * [LLaMA-7B](https://huggingface.co/decapoda-research/llama-7b-hf) 羊驼大模型基座

  * 基于相同的数据，我们还训练了医疗版本的ChatGLM模型: [ChatGLM-6B-Med](https://github.com/SCIR-HI/Med-ChatGLM)

我们看一下团队针对这些模型的训练的时间线，可见团队再不断增加基模型训练，并且寻找到了目前最优的解决方案：[活字1.0](https://github.com/HIT-
SCIR/huozi)

![](http://api1024.oss-cn-
shanghai.aliyuncs.com/xuegpt/WechatIMG2428.jpg?x-oss-
process=image/resize,w_800)

#### **2\. 数据集**

大模型训练最核心的部分其实是数据集构建，我们看一下这个项目的数据集构建情况。

**医学知识库**

团队采用了公开和自建的中文医学知识库，主要参考了[cMeKG](https://github.com/king-yyf/CMeKG_tools)。

医学知识库围绕疾病、药物、检查指标等构建，字段包括并发症，高危因素，组织学检查，临床症状，药物治疗，辅助治疗等。知识库示例如下:

    
    
    {"中心词": "偏头痛", "相关疾病": ["妊娠合并偏头痛", "恶寒发热"], "相关症状": ["皮肤变硬", 
    "头部及眼后部疼痛并能听到连续不断的隆隆声", "晨起头痛加重"], "所属科室": ["中西医结合科", "内科"], 
    "发病部位": ["头部"]}
    
    

然后利用GPT3.5接口围绕医学知识库构建问答数据，设置了多种Prompt形式来充分利用知识。

指令微调的训练集数据示例如下：

    
    
    "问题：一位年轻男性长期使用可卡因，突然出现胸痛、呕吐、出汗等症状，
    经检查发现心电图反映心肌急性损伤，请问可能患的是什么疾病？治疗方式是什么？"
    
    回答: 可能患的是心肌梗塞，需要进行维拉帕米、依普利酮、硝酸甘油、ß阻滞剂、吗啡等药物治疗，
    并进行溶栓治疗、低分子量肝素、钙通道阻滞剂等辅助治疗。
    此外需要及时停用可卡因等药物，以防止病情加重。"
    
    

训练数据集，共计八千余条，需要注意的是，虽然训练集的构建融入了知识，但是仍存在错误和不完善的地方，后续我们会利用更好的策略迭代更新数据集。

指令微调数据集质量仍有限，后续将进行不断迭代，同时医学知识库和数据集构建代码还在整理中，整理完成将会发布。

# **模型测评**

针对中医场景，团队构建了一个用户测评的问答测试集合，并且对比了各个大模型的效果：

![](http://api1024.oss-cn-
shanghai.aliyuncs.com/xuegpt/WechatIMG2429.jpg?x-oss-
process=image/resize,w_800)

# **发展现状**

发完论文之后基本没有进展，Star数在4.2k，很有影响力，但是商用存在一定距离，用于研究目的尚可。

# **总结**

该项目提供了一个训练行业大模型的范本，并且最终的效果也还可以，作为研究够用了，行业大模型训练的核心是数据集和测评集的构建，工程成本控制的核心是大模型训练人员的经验，该项目只在小数据集上跑了最小参数的模型训练，成本可控。但要工程化的话，核心成本控制就显得非常重要，因此普通无经验人员很难做好。

  * 除了这个项目，我还整理了100多个项目，工具和测评 参见 自学AI网 [xuechatgpt.com](http://xuechatgpt.com)

### 【访谈】微信AI项目创始人访谈

社群满1000人开始访谈，请先加我微信，加入AI创业社群：

### 你别不服！我认为这才是最接地气的中国AI创业项目

  * 2023-204年我跟踪了100多个AI项目，现在这些项目发展情况怎么样？要说中国最接地气的AI项目，非属于下面这个微信AI项目不可，看了这么多项目，发现这个才是真正的王者。

![](https://static.xiaobot.net/file/2024-05-06/580209/d87ae62e51042202fd6303d4a6483e08.jpeg)

  * 全部项目，资料，测评移步 自学AI网 [xuechatgpt.com](http://xuechatgpt.com)

# **项目介绍**

先给你看看这个项目的客户列表，包含了几乎所有互联网头部公司：

![](http://api1024.oss-cn-
shanghai.aliyuncs.com/xuegpt/WechatIMG2420.jpg?x-oss-
process=image/resize,w_800)

如果我有这么多头部公司客户，我一定拼命宣传自己的产品，但你仔细去看这家公司网站的话，会发现底部的公司名字，
它都故意写错，拿这个公司名字是查不到任何信息的。这个项目是基于微信群的AI机器人，显然用户需求痛点及其明确，但是
微信官方并不支持这种工具，这也为什么它只能闷声发大财的原因。

![](http://api1024.oss-cn-
shanghai.aliyuncs.com/xuegpt/WechatIMG2421.jpg?x-oss-
process=image/resize,w_800)

# **功能特点**

微信群AI显然是一个痛点明确的需求，这个项目经过10年的发展，功能已经非常完善，要说这个AI的第一功能特点的话，肯定得是：
防封杀，这也是该项目的核心竞争力。 其他功能特点部分列表如下：

![](http://api1024.oss-cn-
shanghai.aliyuncs.com/xuegpt/WechatIMG2422.jpg?x-oss-
process=image/resize,w_400)![](http://api1024.oss-cn-
shanghai.aliyuncs.com/xuegpt/WechatIMG2423.jpg?x-oss-
process=image/resize,w_400)

几乎覆盖了所有能够想到的自动化功能。

# **盈利模式**

该项目也分为免费版和收费版两个版本，其中免费版是不带防封杀功能的，这个做的太绝了，没有防封杀功能，这个AI几乎等于废铁，任何公司都不会购买，因此也就把想免费白嫖的个人全部剔除了，剩下的都是能付费的公司客户。

![](http://api1024.oss-cn-
shanghai.aliyuncs.com/xuegpt/WechatIMG2425.jpg?x-oss-
process=image/resize,w_800)

中国公司100%都需要这个群AI功能，就算只有

# **发展现状**

我们看看这个项目的关键词的百度搜索指数：

![](http://api1024.oss-cn-
shanghai.aliyuncs.com/xuegpt/WechatIMG2424.jpg?x-oss-
process=image/resize,w_800)

作为一个工具来说，这个项目搜索量已经非常惊人了，也表明微信群AI这个需求一直会持续强烈。该项目目前也没有其他竞争对手，
处于这个领域的垄断地位，未来也很难有人能发起挑战，预测该项目至少还能盈利30年以上。

# **总结**

微信机器人是一个现在还可以去做的AI，该项目深耕多年，达到了商用级别，也是市场上最大的一家，光是防封杀这一个技术已经可以让他成为霸主了；很多做类似项目的人都死在防封杀这一点上。

  * 除了这个项目，我还整理了100多个项目，工具和测评 参见 自学AI网 [xuechatgpt.com](http://xuechatgpt.com)

### 【访谈】码多多项目创始人访谈

社群满1000人开始访谈，请先加我微信，加入AI创业社群：

### AI扫地僧！原来真正通过AI赚到100万的项目长这样

  * 每一次淘金热的背后都有无数发财的项目，它们专门提供铲子和水，2023-2024年我跟踪了100多个AI项目，现在这些项目发展情况怎么样？今天来分享一个年赚100万以上的”铲子“项目。

![](https://static.xiaobot.net/file/2024-05-06/580209/043a7aba6474c7f4a4d124c44f51dcda.jpeg)

  * 全部项目，资料，测评移步 自学AI网 [xuechatgpt.com](http://xuechatgpt.com)

# **项目介绍**

我开始关注这个项目是2023年AI刚起来的时候，当时这个项目已经非常火爆了，简单的说就是基于各种大模型AI接口，搭建了一套软件界面，实现一个智能聊天，谁都知道这种给淘金人卖铲子的生意肯定能成功，当时做这类软件的团队或个人也非常多，为什么很多都销声匿迹了，只有这个项目赚钱并且发展的无敌好？

我想建议大家看一看这家老板的自媒体账号（下面是他们的小红书）：

![](http://api1024.oss-cn-
shanghai.aliyuncs.com/xuegpt/WechatIMG2409.jpg?x-oss-
process=image/resize,w_400)

我持续观察了1年，发现这家伙的自媒体每天都更新，而且越做越好，这个开发项目的成功绝对不只是开发这么简单！

# **功能特点**

简单的说，这个项目提供了一套代码，实现了AI聊天，AI绘画，多终端适配，界面模版等等符合中国人的功能，而且是快速迭代的，
最新更新到了3.9.0版本，很多同期出来的产品最多只更新到了1.0版本，这个项目值得好好研究。 下面先进入它的演示系统，体验一下这套AI系统的功能：

1.

![](https://static.xiaobot.net/file/2024-05-08/580209/652459d1fe9bf9b22c6930a5657a2d3a.jpeg)

2.

![](https://static.xiaobot.net/file/2024-05-08/580209/19f5ccd1f97d92d4017c56b711122d95.jpeg)

3.

![](https://static.xiaobot.net/file/2024-05-08/580209/8af7b0eefe207e87d485d7590d83a5fc.jpeg)

# **盈利模式**

这套软件只支持付费使用，这也让它的初始盈利模式变得非常简单，而且价格是几千一套，这样就筛去了很多低端客户，留下的都是优质客户，只要有用了几个初始客户，马上就可以继续优化系统，形成良性循环。
下面仅仅是它一个版本2023年的销售情况：

![](http://api1024.oss-cn-
shanghai.aliyuncs.com/xuegpt/WechatIMG2410.jpg?x-oss-
process=image/resize,w_800)

粗略估算了一下，光靠买系统1年已经盈利100万以上了。而且它还不至于系统，还有更高级的盈利模式，下面会详细说说。对比很多同期的免费软件，因为无法盈利，更新了一个版本之后，作者就不再维护了，客户也是气的半死，还不如一开始就收费。

当然，这个项目敢于一开始收费，也是和他自身的两个特点有关的，第一：这个项目的老板很早就开始做自媒体，有很强的运营能力，吸引了一大批初始客户，第二：这个团队之前做的是另外一个收费的Sass系统源代码，因此这个收费模式走的轻车熟路。就是下面这个：

![](http://api1024.oss-cn-
shanghai.aliyuncs.com/xuegpt/WechatIMG2412.jpg?x-oss-
process=image/resize,w_800)

# **发展现状**

注意看该项目主页下面的问题板块，跟我预想的一样，因为项目的传播，很多客户会有定制的AI需求，这个团队现在主要的盈利已经开始做定制开发，而且从老板的自媒体看，已经需要大量招聘AI工程师才能完成业务了，发展只会越来越好。

![](http://api1024.oss-cn-
shanghai.aliyuncs.com/xuegpt/WechatIMG2411.jpg?x-oss-
process=image/resize,w_800)

# **总结**

这个项目之所以从无数同类的产品中脱颖而出，我认为最重要的有两点值得学习，一是一开始就收费，这样更容易实现盈利飞轮，第二是开发人员更需要做自媒体，才能补足运营的短板。
当然该项目再次证明，中国成功的AI创业项目一定是原来就在相关领域有深厚积累的团队，绝对不是没有任何背景的小白创业者。

  * 除了这个项目，我还整理了100多个项目，工具和测评 参见 自学AI网 [xuechatgpt.com](http://xuechatgpt.com)

### 【访谈】标小智项目创始人访谈

社群满1000人开始访谈，请先加我微信，加入AI创业社群：

### 绝了！这个中国女生做的AI项目太懂用户了

  * 如果有个人跟你说，有个AI可以免费做名片设计，你觉得这个项目会怎么样？2023-2024年我跟踪了100多个AI项目，现在这些项目发展情况怎么样？今天来分享这个AI名片项目，神奇的是这个项目背后还藏着一个宝藏女生。

![](https://static.xiaobot.net/file/2024-05-06/580209/0b3902eda4c21108ec84400c25bdce0a.jpeg)

  * 全部项目，资料，测评移步 自学AI网 [xuechatgpt.com](http://xuechatgpt.com)

# **项目介绍**

用AI做名片是一个人人都可以想到的项目，但你要是深入去做这个项目的话，你会发现这个项目需要很强的AI设计能力，这就不是一般公司可以完成的了；一开始我也很好奇什么公司可以做出这样的项目，直到我深入挖掘了这家公司的背景我才搞明白，你看看它除了AI名片之外，还有AI设计，AI头像，AI抠图，AI做Logo等项目。

![](http://api1024.oss-cn-
shanghai.aliyuncs.com/xuegpt/WechatIMG2401.jpg?x-oss-
process=image/resize,w_400)![](http://api1024.oss-cn-
shanghai.aliyuncs.com/xuegpt/WechatIMG2402.jpg?x-oss-
process=image/resize,w_400)

从这些项目的特点看，该团队是先围绕一个强需求的产品 ”智能Logo设计“ 开始，获取了大量流量之后，逐步根据用户的需求开发了一系列 相关的AI。

# **功能特点**

因为AI做logo和AI做名片都是一个团队做的，我们可以一起来体验一下；根据过往用户的评价，这个AI名片有几个特点：

  * 免费，操作简单，AI 一键生成；

  * 生成名片包括印刷名片和数字名片两种类型；

  * 一键下载，快速印刷；

  * 使用评价：简单好用，名片生成效果好，良心产品。

从这些特点也可以看出创始人有非常接地气的思维，能考虑到用户的需求细节，自然也就吸引了大量的免费流量。

#### **1\. 体验一下AI生成Logo**

1.1 名字:

![](https://static.xiaobot.net/file/2024-05-08/580209/076d82a6548beff38ecc39def252f344.png)

1.2 选择:

![](https://static.xiaobot.net/file/2024-05-08/580209/dfa9f28b91435310b4c627c7067aa501.png)

1.3 结果:

![](https://static.xiaobot.net/file/2024-05-08/580209/e68b5faea79d57072b274b33e8a43a53.png)

#### **2\. 用Logo制作名片**

2.1 Logo：

![](https://static.xiaobot.net/file/2024-05-08/580209/c41b15ad507a3be3372278d61b7e3275.png)

2.2 名片生成：

![](https://static.xiaobot.net/file/2024-05-08/580209/fe7581521a4ee67647e23dacbcc3ee8f.png)

# **盈利模式**

我们从AI名片项目，查到AI做Logo项目，也就是 [标小智](https://www.logosc.cn/)
，发现制作方是这个公司：上海婷平网络科技有限公司 才是背后的巨无霸，不看不知道，这个公司居然运营了10年以上：

![](http://api1024.oss-cn-
shanghai.aliyuncs.com/xuegpt/WechatIMG2404.jpg?x-oss-
process=image/resize,w_800)

注册资本10万，员工数3个人，从这些信息可以看到这个创始人是一个非常接地气，有耐性的创业者；也可以看出这些AI项目免费的目的就是为了引流用户，一定会有部分用户有深入的设计需求，这样的生意循环就成了。
另外从股权方面看，这个创始人还是其他设计相关大公司的股东，也就说明这些免费引流的流量价值又得到了进一步的变现。

# **神秘女子**

研究了这个项目，我真的非常佩服这个项目的创始人，是一个中国女生，能坚持10年以上不断地优化AI产品，并且不断地进化，小小的团队产生出巨大的价值。
说一个更神奇的事，我在研究AI过程中，发现一个非常好用的AI项目收集网站 ”神器集“：

![](http://api1024.oss-cn-
shanghai.aliyuncs.com/xuegpt/WechatIMG2405.jpg?x-oss-
process=image/resize,w_800)

这个项目的用户量非常大，每天都会有很多AI项目注册上来，供需两相循环，导致这个网站成了事实上的AI入口，这种网站有一种直击用户痛点的能力，调查发现，这个项目居然也是这个小公司做的，背后还是这个女生，持续的产品力简直爆表了！

# **总结**

从这个项目我们可以看到，中国AI创业者成功者一定是那些原来就在某个行业里深耕多年的团队，像这个项目创始人非常聪明且接地气，采用免费策略大量吸引用户，从用户里筛选客户，有做不完的生意，再从客户需求里不断开发各种相关AI应用，小团队做成了一个行业标杆。

  * 除了这个项目，我还整理了100多个项目，工具和测评 参见 自学AI网 [xuechatgpt.com](http://xuechatgpt.com)

### 【访谈】周报项目创始人访谈

社群满1000人开始访谈，请先加我微信，加入AI创业社群：

### 牛逼立体！分享一个一天就有100万人使用的AI项目

这样一个小小的AI项目，每天居然有100万人使用，秘诀是什么？2023-2024年我跟踪了100多个AI项目，今天来盘点这个”周报项目“！

全部项目，资料，测评移步 自......

### 【访谈】背景抠图BgSub创始人访谈

社群满1000人开始访谈，请先加我微信，加入AI创业社群：


<a href="https://github.com/Reno9527/awesome-xiaobot" style="color: white; text-decoration: none;">awesome-xiaobot</a>

返回 [首页](../README.md)