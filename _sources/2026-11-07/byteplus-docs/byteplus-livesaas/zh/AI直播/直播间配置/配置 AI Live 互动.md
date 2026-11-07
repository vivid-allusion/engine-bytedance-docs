---
title: "配置 AI Live 互动"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/configuring-ai-live-interactions-zh-CN"
---

AI Live 可在直播过程中自动响应观众评论和互动事件。配置 **Live interaction** 后，AI 主播会在适当时机暂停当前脚本，根据你的知识库、提示和过滤规则生成回复，然后继续朗读脚本。

本指南介绍如何配置评论回复、互动回复以及 AI 回复测试。

> **注意**

> 直播过程中无法更改互动设置。建议在直播前充分测试并完成相关设置。

## 前提条件

* 开始之前，请准备用于回复的知识库。详情请参见 [配置知识库](https://docs.byteplus.com/docs/byteplus-livesaas/prepare-and-upload-knowledge-base-file-zh-CN)。

* 要在 TikTok 上开播，请确保已添加你希望开播的 TikTok 账号的 TikTok 用户 ID：

   1. 在顶部导航栏中，输入你的 **TikTok 用户 ID**，以获取直播观众活动。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40fe23bba5e54a25ba69f4c6fa060a55~tplv-goo7wpa0wc-image.image)

      你可以按照下图在 TikTok App 中获取该 ID。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10ac18d800e74e5dbc8c28146e8b1580~tplv-goo7wpa0wc-image.image)

* 要在 Shopee 上开播，请确保已添加 Live Connector 浏览器扩展，将 Shopee 直播间的观众评论转发至 BytePlus AI Live。详情请参见 [通过 RTMP 在 Shopee 上开启直播](https://docs.byteplus.com/docs/byteplus-livesaas/going-live-on-shopee-via-rtmp-zh-CN)。

## 操作步骤

1. 登录 [BytePlus Live 控制台](https://console.byteplus.com/)。

2. 在顶部导航栏中，选择 **AI Live**。

3. 在 **Live Room** 页面，点击打开已有直播间或创建直播间。

4. 在顶部导航栏中，点击 **Live interaction**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a503096289f4da690c236f6c926b6cf~tplv-goo7wpa0wc-image.image)

   **Live interaction** 窗口会滑出。你可以在此配置评论回复策略和互动回复。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02aa9041d7a54864b563c1cd587f42be~tplv-goo7wpa0wc-image.image)

### 配置评论回复策略

1. 在 **Comment reply** 标签页下，添加你之前创建的一般知识库。产品知识库仅在你为直播添加产品脚本并在 **Knowledge base** 页面上传相应文件时启用。详情请参见 [配置知识库](https://docs.byteplus.com/docs/byteplus-livesaas/prepare-and-upload-knowledge-base-file-zh-CN)。

2. （可选）在 **Prompt Settings** 框中自定义指导 AI 回复风格的指令。

3. 调整 **Dense Weight** 以控制搜索偏好。该数值（0.2 到 1.0）用于平衡关键词匹配与语义理解。较高数值会优先考虑问题的含义而非精确词语。默认值为 0.5。

4. 在 **Chat Settings** 下配置忽略无关评论的规则。

   |**过滤规则** |**说明** |
   |---|---|
   |纯表情消息屏蔽 |忽略仅包含表情符号的评论。（支持BytePlus Live表情符号、标准表情符号和TikTok表情符号）。 |
   |重复刷屏过滤 |过滤重复刷屏的垃圾消息。 |
   |聊天敏感词 |屏蔽包含自定义敏感词列表中词语的评论。详情请参见[屏蔽敏感词](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-sensitive-words)。 |
   |字数过滤 |设置评论可回复的最小和最大字数。默认值为0到50字，超过50字的评论将被忽略。 |
   |评论回复策略 |* **虚拟形象回复**：虚拟形象会朗读并回复评论。目前仅支持此策略。<br><br>* **评论区回复**：自动在聊天中发布回复。此选项暂不支持。 |

### 配置互动回复策略

除了回复评论外，Avatar 还可主动响应观众活动。在 **Engage reply** 标签页下，开启所需的响应类型并设置触发频率。直播过程中，主播会暂停当前脚本，口头播报响应内容，然后继续脚本。

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94c1109d7cdd4c9fbb55cc7aa2eaaac0~tplv-goo7wpa0wc-image.image)

|**回复类型** |**说明** |
|---|---|
|**进房欢迎** |观众进入房间后，生成欢迎语并让主持人朗读。你可以设置观众进房触发欢迎语的概率。默认值为30%。 |
|**互动感谢** |观众点赞、分享或关注后，生成感谢语并让主持人朗读。你可以设置互动触发感谢语的概率。默认值为100%。 |

### 测试 AI 回复

开播前，可模拟观众活动，预览 Avatar 的响应效果。这样可以验证你的评论回复和互动响应设置，并在需要时进行优化。

1. 在脚本配置页面，点击 **Explanation text** 区域右上角的 **AI reply test**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b18a0c4eecc641f283a2f7dca1363a4e~tplv-goo7wpa0wc-image.image)

2. 在 **AI response test** 对话框中，你作为观众发送消息给 AI 回复机器人，并查看其回复。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08d3051167ec45c5b066859058a499a8~tplv-goo7wpa0wc-image.image)

3. （可选）在 **Viewer nickname** 框中编辑测试使用的名称。

   * 触发活动或发送评论以测试对应回复：

   * **Join** / **Like** / **Follow** / **Gifting**：点击按钮模拟观众加入、点赞、关注或送礼。AI回复机器人会生成并展示匹配的互动回复。

   * **评论**：在文本框中输入消息，然后点击**发送**。AI回复机器人会根据你的评论回复设置和知识库进行回复。

4. 在会话区域查看回复，确认其是否符合你的预期。根据需要调整你的互动设置、提示词或知识库，然后再次测试。

## 常见问题

### 问：部分观众昵称包含表情符号或不可读符号。我应该怎么做？

在评论回复设置中的**提示词**添加一条指令，使AI在回复前将不可读昵称转换为可读文本。例如：

```Plain
If the username is emoji or unreadable symbol, transform those into readable before answering the question.
```

### 问：观众评论已进入直播间，但AI主持人未回复。我应该怎么做？

请检查以下项目：

* 评论是否因纯表情、重复垃圾信息、敏感词或字数过滤规则被屏蔽。

* 直播间是否已添加通用知识库，或当前产品是否已上传产品知识库。

* 若评论来自第三方平台，请检查评论同步工具是否仍在同步，以及评论是否已进入BytePlus AI直播间的**聊天**列表。
