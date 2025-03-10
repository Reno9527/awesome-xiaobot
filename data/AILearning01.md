# AI 工作流设计手册_小报童_Awesome_XiaoBOT

## AI 工作流设计手册介绍
> 专栏作者：艾木和大圣，两位热爱 AI Agent 技术的软件工程师，AI 开源社区《通往 AGI 之路》共创作者，《成为 Agent 工程师之 Coze  
实战》课程作者。\n\n本专栏会分享我们打造 AI 工作流提效的心得，包括但不限于：AI 工作流设计技巧、 LLM 基础认知、提示词技巧、RAG 技术以及  
AI 时代的编程思维等主题。\n\n内容形式是简短的、碎片化的。\n\n期望你可以梳理出你个人的工作流，并对每个环节利用 AI 进行优化，打造专属于自己的  
AI 工作流。\n\n限时 99 元，每周至少更新一篇内容，持续一年。  
  


|名称|作者|读者数量|内容数量|更新时间|
|---|---|---|---|---|
|[AI 工作流设计手册](https://xiaobot.net/p/AILearning01?refer=0b133df9-27dc-423b-8101-639049001c13)|艾木 × 大圣|381人|16篇|2024-12-15|

## 最近更新
### 小报童退款通知

大家好，这篇文章推送是用来告知大家一件事情：我和艾木的这个小报童要停止更新了。

我们的客户有以下几类：

1、Coze实战课程的学员，这个我会在微信群跟大家说明原因。大家不会收到退款，请见谅

2、付全款99 RMB的小伙伴，请务必联系大圣，我会给你全额退款，非常抱歉给你带来不好的体验

3、我之前的知识星球付费同学，后来免费转的小报童，我已经微信私聊给各位退款了，如果有漏的，请私聊大圣

再次抱歉给大家带来不好的体验，请符合条件的朋友务必联系我，感谢！

![](https://static.xiaobot.net/file/2024-12-16/324920/8a4aebe0c929801dcb547bc6ce50fe97.png)

### 提示词编程｜我从顶级的提示词工程团队（Anthropic）那里学到了什么

写在前面的话：

我有一个很好的学习习惯，养成好多年了，它也让我受益好多年。这个习惯叫“追本溯源”。

所谓“追本”就是追问本质。为什么要追问？因为问题是思考的起点。为什么要......

### 提示词编程｜如何在提示词里控制任务流程？

在面对复杂的任务时，我们通常需要将它拆解成不同的部分或者步骤，一步一步去完成，才能获得比较好的效果，这应该是我们人类在解决问题时的一个认知常识。对于大语言模型来说，也是如此，所以才会有
思维链（......

### 提示词编程｜有必要用 Lisp 语言写提示词吗？

有些人玩提示词是工程风格的，比如我。我之前追求的就是把任务清晰表达出来就好了，所以我没有去学任何框架、模板、技巧，也没有花多少时间去精细雕琢过我写的提示词。

我一直觉得提示词工程（p......

### LLM 基础认知｜词嵌入和类比

写在前面的话

“词嵌入和类比”是我最近比较感兴趣的一个主题。我陆陆续续地看了一些资料，但自觉尚未达到完全消化的程度，所以还无法基于自己的理解作体系化的论述。这篇文章是一份索引，希望能为同样对此主题......

### AI 编程｜使用 Cursor AI 的意识与工作流

我上周做了一次主题为《与 Cursor AI 一起玩代码》的直播分享，这篇内容可以看作是那次分享的伴随笔记。

最近，随着 Cursor 的出圈，AI 编程也跟着火起来了。像 Curs......

### AI编程｜用LLM编写Coze代码节点

本文归属于AI编程系列文章，该系列介绍请参考：[成为Agent工程师之AI编程](https://xiaobot.net/post/626f0069-8f1a-4261-8797-bf1140a8646b)

# 引言

前面我们讲了很多的编程理论和基础知识，这一章开始，我们就正式进入到AI编程的实战阶段。

前面我们讲过：对于普通人而言，AI时代的编程更多的是在**现有框架或平台的约束下实现特定功能** 。

在AI时代的编程我分为三个场景

>   1. 编写一个特定的方法，用来实现**特定输入到特定输出的转换**
>
>   2. 编写一个**逻辑简单的产品** ，例如Chrome插件，**用来提高自身的效率**
>
>   3. 编写一个产品，涉及到页面展示，后台复杂逻辑处理以及数据存储，用来进行售卖
>
>

第三种可能是好多人畅想的，期望利用AI可以像程序员一样开发各种复杂系统。

这里我要跟大家泼一盆冷水，在未来很长的一段时间内，**普通人** 利用AI编程做出**生产级别可用**
的复杂系统都是非常困难的。**除非你自学编程知识，达到了程序员的级别**

PS：这里大家不要抬杠，贪吃蛇这种游戏还有简单的Chrome插件都不是生成级别可用的复杂系统，这最多算个玩具或者说Demo

但是第一种和第二种却是实实在在可以实现的，而且是具有生产价值的。

当下AI Agent概念非常火，而以Coze为代表的等AI Agent平台也逐渐兴起。

Coze平台的出现给了普通人打造一款轻量级产品的可能性，Coze中有丰富的插件以及功能节点，让非编程人士可以像搭积木一样实现某个具体的功能。

同样的，Coze中也提供了代码节点，我们可以通过代码节点编写代码，实现特定的功能，从而让我们的工作流更加稳定和强大

Coze中的代码节点使用就是一个非常典型的AI编程的应用场景，本文我们就以这个为案例来讲解AI编程的应用场景：**编写一个特定的方法，用来实现特定输入到特定输出的转换**

* * *

这里我默认你已经了解了如下的知识点

  * 你对Python这门编程语言有基本的认知与了解

  * 你了解了编程的中很重要的一个概念JSON，并且能熟练运用

  * 你了解了Coze的使用，并知道其代码节点是怎么一回事

  * 你已经看到我的关于《理解输入、处理和输出的框架》这篇文章

# Coze的代码节点

Coze中目前支持两种编程语言Python和Javascript教程全部以Python为语言进行讲解

我们先来看下Coze代码节点中的模版代码

    
    
    async def main(args: Args) -> Output:
        params = args.params
        ret: Output = {
            "key0": params['input'] + params['input'],
            "key1": ["hello", "world"],
            "key2": {
                "key21": "hi"
            },
        }
        return ret

我们来分析下这个代码模版

  * 对于 **async def main(args: Args) - > Output**: 这一段代码你根本不用管，这是Coze要求的一种规范，你只要遵循在这个规范下写代码即可

  * **params = args.params** 这行代码非常重要，这代表着如何**获取输入 ，这里的args.params就是获取输入的JSON结构，然后传递给params这个变量供后续使用**

  * 而下面这段代码则是在**构建输出**

    * ret: Output = { "key0": params['input'] + params['input'], "key1": ["hello", "world"], "key2": { "key21": "hi" }

分析完Coze的代码节点，你会发现它非常契合我们前面讲到的**输入、处理和输出的框架** ，

我把上述的代码模版再抽象一层如下，你会对这个模版的理解会更加清晰

    
    
    async def main(args: Args) -> Output:
        # 从args中获取输入参数
        params = args.params
        
        # 在此处理输入并生成输出所需要的数据
        
        # 构建输出JSON
        ret: Output = {
            # 在此构建输出JSON
        }
        
        # 返回结果
        return ret

# AI与人的分工

分析完Coze的代码节点格式，在开始使用AI辅助我们编程之前，我们要理解AI和人的分工边界

看完上面抽象出来的代码模版，我想答案已经呼之欲出了：

>   * 人定义清楚输入和输出的JSON格式
>
>   * 人用自然语言描述由输入转成输出的处理逻辑
>
>   * AI则负责根据输入+输出的格式以及人描述的处理逻辑，生成可以执行的代码
>
>

**这里需要特别注意的是，你生成的完整代码必须符合Coze的模版规范**

既然要利用AI编程，并且还对输出有一定的要求，那我们可以编写一个提示词来辅助我们

为了排版美观，我把编写的提示词放在了附录中，大家可以自行参考。（提示词非常好懂，无需讲解）

# 编程案例

为了让大家学会使用这个提示词，我这里举两个实际的场景。

PS：由于Claude是目前公认编程能力最强的AI，所以AI编程建议使用Claude。但是由于费用限制，国内的智谱和豆包也还行，具体我没有做大量的测试，请在使用过程中自行测试

### 字符串转数组

**输入** ：

    
    
    {
       "input": "徐州#杭州#贵州"
    }

**输出** ：

    
    
    {
        "result": [
            "徐州",
            "杭州",
            "贵州"
        ]
    }

**处理逻辑** ：

输入是用#分割的中文字符串，帮我转成字符串数组输出

**使用提示词生成的代码（Claude大模型）**

    
    
    async def main(args: Args) -> Output:
        # 从args中获取输入参数
        params = args.params
        
        # 获取输入字符串
        input_string = params['input']
        
        # 使用split方法将字符串分割成列表
        result_list = input_string.split('#')
        
        # 构建输出JSON（必须是字典格式）
        ret: Output = {
            "result": result_list
        }
        
        return ret

### 两个数组合并

这个案例取自我的《Coze实战课程》中的儿童绘本

**输入：**

    
    
    {
        "imageInputList": [
            {
                "code": 0,
                "data": {
                    "images": [
                        {
                            "image_url": "https://s.coze.cn/t/CimtF2Uq9AyhVbo0/"
                        }
                    ]
                },
                "log_id": "202409162345450CB01612D96016D1FDE4",
                "msg": "success"
            },
            {
                "code": 0,
                "data": {
                    "images": [
                        {
                            "image_url": "https://s.coze.cn/t/Ctch3b7aHPVn8n4g/"
                        }
                    ]
                },
                "log_id": "202409162345450CB01612D96016D1FDE4",
                "msg": "success"
            }
        ],
        "storyList": [
            {
                "desc": "小猴子皮皮🐒在井边玩耍，它看到井里有一个圆圆的月亮。皮皮惊讶地叫道：“哇！月亮怎么掉进井里了？”它赶紧找来小伙伴们，一起想办法把月亮捞出来。小猴子们围在井边，好奇又兴奋。",
                "prompt": "一群好奇的小猴子围在一个古老的井边，井水清澈映着夜空中的圆月，小猴子皮皮表情惊讶，手指着井中的月亮，其他猴子们也露出好奇和兴奋的神情，背景是宁静的森林夜晚，星光闪烁。",
                "title": "1. 月亮掉进井里了？🌕"
            },
            {
                "desc": "小猴子们决定用长长的树枝去捞月亮。皮皮小心翼翼地把树枝伸进井里，可是每次树枝一碰到水面，月亮就碎了。皮皮困惑了：“月亮怎么捞不起来呢？”小伙伴们也皱起了眉头，但它们没有放弃。",
                "prompt": "小猴子皮皮和其他小猴子正尝试用一根长长的树枝从井中捞起月亮的倒影，水面波光粼粼，每次树枝触碰水面，月亮的倒影就碎裂开来，小猴子们的表情从兴奋转为困惑，但仍然坚持不懈，背景是夜晚的森林，井边有温馨的灯光。",
                "title": "2. 捞月亮大作战🐒🌊"
            }
        ]
    }

**输出：**

    
    
    {
        "resultList": [
            {
                "desc": "小猴子皮皮🐒在井边玩耍，它看到井里有一个圆圆的月亮。皮皮惊讶地叫道：“哇！月亮怎么掉进井里了？”它赶紧找来小伙伴们，一起想办法把月亮捞出来。小猴子们围在井边，好奇又兴奋。",
                "prompt": "一群好奇的小猴子围在一个古老的井边，井水清澈映着夜空中的圆月，小猴子皮皮表情惊讶，手指着井中的月亮，其他猴子们也露出好奇和兴奋的神情，背景是宁静的森林夜晚，星光闪烁。",
                "title": "1. 月亮掉进井里了？🌕",
                "imageUrl": "https://s.coze.cn/t/CimtF2Uq9AyhVbo0/"
            },
            {
                "desc": "小猴子们决定用长长的树枝去捞月亮。皮皮小心翼翼地把树枝伸进井里，可是每次树枝一碰到水面，月亮就碎了。皮皮困惑了：“月亮怎么捞不起来呢？”小伙伴们也皱起了眉头，但它们没有放弃。",
                "prompt": "小猴子皮皮和其他小猴子正尝试用一根长长的树枝从井中捞起月亮的倒影，水面波光粼粼，每次树枝触碰水面，月亮的倒影就碎裂开来，小猴子们的表情从兴奋转为困惑，但仍然坚持不懈，背景是夜晚的森林，井边有温馨的灯光。",
                "title": "2. 捞月亮大作战🐒🌊",
                "imageUrl": "https://s.coze.cn/t/Ctch3b7aHPVn8n4g/"
            }
        ]
    }

**处理逻辑：**

将两个数组imageInputList和storyList可以合并成一个数组输出

**使用提示词生成的代码（Claude）**

PS：此代码没有经过任何人为修改，是直接可用的代码

    
    
    async def main(args: Args) -> Output:
        # 从输入参数中获取imageInputList和storyList
        params = args.params
        image_input_list = params['imageInputList']
        story_list = params['storyList']
        
        # 创建结果列表
        result_list = []
        
        # 确保image_input_list和story_list长度相同
        if len(image_input_list) != len(story_list):
            raise ValueError("imageInputList和storyList的长度不一致")
        
        # 合并两个列表的信息
        for image_input, story in zip(image_input_list, story_list):
            # 从image_input中提取图片URL
            image_url = image_input['data']['images'][0]['image_url']
            
            # 创建新的字典，包含story的所有信息和图片URL
            result_item = {
                "desc": story['desc'],
                "prompt": story['prompt'],
                "title": story['title'],
                "imageUrl": image_url
            }
            
            # 将新创建的字典添加到结果列表中
            result_list.append(result_item)
        
        # 构建并返回输出JSON（字典格式）
        ret: Output = {
            "resultList": result_list
        }
        
        return ret

注意：代码写完之后，代码节点的输出设置一定要设置为和输出一样的JSON格式

![](https://static.xiaobot.net/file/2024-09-17/324920/c1e32b34ddf118fd31a52b41419ad234.png)

# 写在最后

这篇文章以Coze的代码节点为例，提供了一种利用AI辅助编程的思路。

这里我更想表达的是：

  * 要清楚AI编程的能力边界，AI和人应该如何分工

  * 以Coze为代表的AI Agent平台的出现，让我们不必编写完整的系统代码也能构建产品

  * AI编程的一个应用场景：编写一个特定的方法，用来实现特定输入到特定输出的转换

AI编程之路道阻且长，但是既然决定踏上这条路，那就不要心急，多练，多想。厚积薄发

**看完如果觉得有启发，请帮忙点个有启发呀～**

# 附录

### 提示词

    
    
    # Coze代码节点生成器
    
    作者：大圣
    版本：1.0.0
    用途：你是一个专业的Python开发者，负责为Coze平台创建代码节点。请根据用户提供的输入和输出JSON格式，生成符合Coze代码节点规范的Python代码。
    
    ### 输入格式
    
    用户将提供以下信息：
    
    1. 输入JSON格式
    2. 输出JSON格式
    3. 所需的处理逻辑描述（可选）
    
    ### 输出要求
    
    生成的代码必须：
    
    1. 遵循Coze代码节点的模板结构
    2. 正确处理输入参数
    3. 返回符合指定格式的输出，**必须是字典格式**
    4. 实现用户描述的处理逻辑（如果提供）
    5. 包含通俗易懂的注释，适合编程小白理解
    6. 保持简洁，尽量不依赖第三方库（除非绝对必要）
    
    ### 代码模板
    
    ```python
    async def main(args: Args) -> Output:
        # 从args中获取输入参数
        params = args.params
        
        # 在此处理输入并生成输出
        
        # 构建输出JSON（必须是字典格式）
        ret: Output = {
            # 在此构建输出字典
        }
        
        return ret
    ```
    
    ### 示例
    
    #### 输入
    
    输入JSON格式：
    ```json
    {
        "text": "string",
        "number": "integer"
    }
    ```
    
    输出JSON格式：
    ```json
    {
        "processed_text": "string",
        "doubled_number": "integer"
    }
    ```
    
    处理逻辑：将输入的文本转为大写，将数字翻倍。
    
    #### 输出
    
    ```python
    async def main(args: Args) -> Output:
        # 从输入参数中获取文本和数字
        params = args.params
        input_text = params['text']
        input_number = params['number']
        
        # 处理文本：将其转换为大写
        processed_text = input_text.upper()
        
        # 处理数字：将其翻倍
        doubled_number = input_number * 2
        
        # 构建并返回输出JSON（字典格式）
        ret: Output = {
            "processed_text": processed_text,
            "doubled_number": doubled_number
        }
        
        return ret
    ```
    
    #### 代码解释
    
    以下是对上述代码的逐行解释：
    
    1. `async def main(args: Args) -> Output:`: 这是函数定义。它是异步的，接受一个`args`参数，并返回`Output`类型的结果。
    
    2. `params = args.params`: 从`args`中获取输入参数。
    
    3. `input_text = params['text']`: 从参数中提取文本输入。
       `input_number = params['number']`: 从参数中提取数字输入。
    
    4. `processed_text = input_text.upper()`: 使用`upper()`方法将输入文本转换为大写。
    
    5. `doubled_number = input_number * 2`: 将输入数字乘以2，实现翻倍。
    
    6. `ret: Output = {...}`: 创建一个字典作为输出，包含处理后的文本和翻倍后的数字。这里确保返回值是一个字典格式，符合Coze的要求。
    
    7. `return ret`: 返回处理结果，这个结果是一个字典。
    
    ### 注意事项
    
    1. 确保代码能够处理所有输入参数
    2. 使用类型提示以增强代码的可读性和健壮性
    3. 如果需要导入Python标准库模块，请在代码开头添加必要的import语句
    4. 如果处理逻辑复杂，可以创建辅助函数来提高代码的可读性和可维护性
    5. 添加清晰、简洁的注释，解释代码的功能和原理，使编程新手也能理解
    6. 在代码生成后，提供详细的逐行解释，帮助用户理解代码的每个部分
    7. 尽量使用Python标准库，避免不必要的第三方依赖
    8. **始终确保返回值 `ret: Output` 是一个字典格式，这是Coze代码节点的要求**
    
    现在，请提供你的输入和输出JSON格式，以及所需的处理逻辑（如果有），我将为你生成相应的Coze代码节点，并附上详细解释。

### AI编程｜理解输入、处理和输出的框架

本文归属于AI编程系列文章，该系列介绍请参考：成为Agent工程师之AI编程

引言

对于普通人而言，AI时代的编程更多的是在现有框架或平台的约......

### AI编程｜工程师思维

本文归属于AI编程系列文章，该系列介绍请参考：成为Agent工程师之AI编程

引言

在《从零理解编程》章节中，我们探讨了编程的本质和目的。

### AI编程｜从零理解编程

引言

在讲AI编程之前，我们必须要先对编程这个概念有一定的了解。

这一章，我们就用通俗易懂的语言来讲解下编程是什么？

为什么要编程

......


<a href="https://github.com/Reno9527/awesome-xiaobot" style="color: white; text-decoration: none;">awesome-xiaobot</a>

返回 [首页](../README.md)
