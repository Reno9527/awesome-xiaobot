|名称|作者|读者数量|内容数量|创建时间|更新时间|
---
|[大模型应用开发 | API 实操](https://xiaobot.net/p/llm-app-dev-api?refer=0b133df9-27dc-423b-8101-639049001c13)|@菠菜|1348人|33篇|2023-12-05|2024-03-16|

# 最近更新
## Audio | 帮我看看他说的啥OpenAI的Audio接口具备将语音转文本的能力，语音转文本也成为ASR，我们来看代码
import openai

client = openai.OpenAI(api_key="sk......
## Assistants | 客服 - 完整流程这个章节我们来看一个Assistants的完整流程：
import openai
import time
import json

client = openai.OpenAI(api_k......
## Assistants | 客服 - 排队并等待客服答复前边我们创建了：客服（Assistant）、用户的会话（Thread）和消息（Message）。这个章节我们看看如何去排队咨询客服（本次的课程代码并不能执行，主要目的是为了给大家讲解功能，下一章......
## Assistants | 客服 - 创建一个用户的会话和消息这个章节我们来创建一个用户的会话和消息，来看下代码：
import openai

client = openai.OpenAI(api_key="sk-xxxx")
# 创建张三的会话
......
## Assistants | 做一个客服 - 创建带知识和Tools的客服接下来我们将用一个打造智能客服的场景，来讲述如何构建Assistants。这章节带来的是创建带知识和Tools的客服，来看个代码
import openai

client = opena......
## Assistants | 一张图轻松理解Assistants交互流程Assistants可以理解为GPTs的底层能力，OpenAI对外开通了API来让开发者灵活构建自己的AI App。但目前Assistant相关的API还处于beta阶段，且不太稳定。这个章节我......
## Tools | 多插件示例我们的学习陪伴群已经带大家实践了一周，有小伙伴对多tool的使用有困惑，所以应大家要求，来一篇加餐，关于如何注册多插件的代码示例，直接来看代码
import openai
import j......
## Tools | 文件插件，保存GPT对你诉说的秘密最后一篇关于GPT插件的文章啦，今天我们来做个稍微有乐趣的插件，就是秘密保存器。让GPT给你说一个秘密，我们保存到文件中，来看代码
import openai
import json

#......
## Tools | 代码插件，让GPT具有创造力今天我们为GPT构建一个代码插件！来看代码
import openai
import json

# 定义一个方法，用于代码执行
def code_exec(param):
    cod......
## Tools | 数学插件，让GPT成为数学天才上一小节我们讲了GPT插件原理，今天我们为GPT构建一个数学插件！来看代码
import openai
import json
import requests

# 定义一个方法，用于数学......

