---
title: "使用 AI 助手编辑函数代码"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/use_ai_ide_for_code_zh-cn"
---

本文档介绍如何使用边缘函数控制台提供的 AI 助手编辑函数代码。

AI 助手内置了边缘函数运行时 API 的示例代码，可以借助大语言模型帮助您生成、修复和解释函数代码。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">AI 助手生成的代码仅供参考。请您在使用前仔细核对，确保其准确性和适用性。</div>


* <div data-tips="true" data-tips-type="warning">AI 助手提供的代码解释仅供参考。请您以边缘函数官方文档为准。</div>



<span id="使用限制"></span>
## 使用限制

您每天的使用限制如下：


* **会话数量**：您最多可发起 10 个会话。

* **消息数量**：您在每个会话中最多可发送 100 条消息。

* **消息长度**：每条消息不超过 250 个全角字符或 500 个半角字符。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">消息长度的限制不包括被添加为上下文的代码。   </div>
   

<span id="演示视频"></span>
## 演示视频

您可以通过下面的视频快速了解如何使用 AI 助手生成、修复和解释函数代码。

<span id="生成函数代码"></span>
### 生成函数代码

<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_24a9708dedb48d27f964546d5233dd3a.mp4" controls></video>


<span id="修复函数代码"></span>
### 修复函数代码

<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2444f6776854e4c39ae70e54a7c91b94.mp4" controls></video>


<span id="解释函数代码"></span>
### 解释函数代码

<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9c3162811c22d91ed9e1ec0c087c85fd.mp4" controls></video>


<span id="操作步骤"></span>
## 操作步骤

参见以下步骤使用 AI 助手。

<span id="步骤一：打开-ai-助手面板"></span>
### 步骤一：打开 AI 助手面板

在边缘函数控制台，您可以点击代码编辑器右上角的 AI 助手图标来打开 AI 助手面板。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5cc2b4f5601b18ba6794e00e9f0c4850.png) </span>

<span id="步骤二：通过-ai-助手生成代码"></span>
### 步骤二：通过 AI 助手生成代码

参见以下步骤通过 AI 助手生成代码。


1. 在 AI 助手面板的对话框中输入您的需求，然后点击 **发送** 图标。AI 助手会生成符合您的需求的函数代码。例如，您可以输入以下需求：


```text
生成代码用于修改用户请求中的 HTTP 请求头和返回给用户的响应中的响应头：
- 在请求头中添加一个自定义请求头"x-via-function-start"，值为当前时间戳
- 在响应头中添加一个自定义响应头"x-via-function-done"，值为当前时间戳
```


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_8d1228f1e30ce04697a2337a03298b2c.png) </span>

2. 点击生成的代码右上角的 **应用代码** 图标，把代码应用到编辑器。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_30a37116eb5ce7ab0d77e955680b7ff6.png) </span>

接下来，您可以对代码进行调试。参考 [编辑和调试函数代码](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-develop-and-test-function-cn)。

<span id="其他操作"></span>
## 其他操作

<span id="通过-ai-助手修复代码"></span>
### 通过 AI 助手修复代码

如果您在调试中发现问题，需要修复代码问题，可参见以下步骤。


1. 选择代码编辑器中的部分或全部代码，点击 **修复代码**，AI 助手会对代码进行修复。

2. 点击生成的代码右上角的 **应用代码** 图标，把优化或修复后的代码应用到编辑器。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0d61e38df67bd8d4d28361cf18346a09.png) </span>

<span id="通过-ai-助手解释代码"></span>
### 通过 AI 助手解释代码

如果您希望借助 AI 助手了解某个代码片段或整个代码文件的逻辑，可选择代码编辑器中的部分或全部代码，点击 **解释代码**。AI 助手会对代码进行解释。

<span id="把代码添加为会话上下文"></span>
### 把代码添加为会话上下文

如果您需要把某个代码片段或整个代码文件添加为聊天的上下文，您可以选择代码编辑器中的部分或全部代码，点击 **添加到聊天**。您可以使用自然语言描述您的需求，例如修改代码、优化代码等。
