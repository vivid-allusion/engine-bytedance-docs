---
title: "启动 AI 直播"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/start-a-digital-human-livestream-zh-CN"
---

本指南为使用 BytePlus Live 控制台设置并启动自动化 AI Live 提供逐步操作说明。你将学习如何创建直播脚本、配置观众互动的智能回复、管理直播设置并开始你的直播。如需功能及端到端流程概览，请参见 [AI直播概览](https://docs.byteplus.com/docs/byteplus-livesaas/digital-human-overview-zh-CN)。

## 前提条件

* **订阅 AI Live 服务**：请参考 [订阅计费情况](https://docs.byteplus.com/docs/byteplus-livesaas/digital-human-subscription-billing-method-zh-cn) 并联系销售人员订阅 AI Live 服务。

* **训练你的虚拟形象**：训练你自己的虚拟形象和声音，以便在直播中使用。详情请参见 [训练虚拟形象与声音](https://docs.byteplus.com/docs/byteplus-livesaas/train-a-digital-human-and-voice-zh-CN)。

* **准备商品和知识库**：为使主播能够展示商品并回答产品问题，请先将你的商品添加至 **商品库**并上传相应的知识库文件。详情请参见 [管理商品库](https://docs.byteplus.com/docs/byteplus-livesaas/manage-digital-human-livestream-product-zh-CN) 和 [配置知识库](https://docs.byteplus.com/docs/byteplus-livesaas/prepare-and-upload-knowledge-base-file-zh-CN)。

## 操作流程

请按照以下步骤设置并启动你的 AI Live。

### 步骤 1：创建 AI 直播间

1. 登录 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 点击顶部导航栏中的 **AI Live** 。

3. 在 **直播间**页面，点击  **+新建直播间**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef3aeee5a60a49349568177223f3a92d~tplv-goo7wpa0wc-image.image)

   直播间将自动标记为 **数字人直播**，便于识别。

4. 在 **创建直播间**对话框中，设置房间名称、声音、虚拟形象和语速，然后点击 **创建** 进入脚本配置页面。

   |**配置项** |**说明** |
   |---|---|
   |**直播间名称** |输入直播间名称。名称最多可达150个字符。 |
   |**语言** |系统会自动检测语音的语言。 |
   |**Avatar** |为直播间选择一个 Avatar。如果你的对话框显示无可用 Avatar，请参考[训练虚拟形象与声音](https://docs.byteplus.com/docs/byteplus-livesaas/train-a-digital-human-and-voice-zh-CN)。 |
   |**Avatar语音** |* 从可用选项中选择语音。如果你的对话框显示无可用语音，请参考[训练虚拟形象与声音](https://docs.byteplus.com/docs/byteplus-livesaas/train-a-digital-human-and-voice-zh-CN)。<br><br>* 调整 Avatar 的语速。请在开播前设置，直播过程中无法更改语速。范围为 [0.5,2]。 |

### 步骤 2：添加直播脚本

虚拟形象会根据脚本内容主持直播。你可以添加两种类型的脚本，并在一次直播中混合多条脚本。详情请参见 [生成直播脚本](https://docs.byteplus.com/docs/byteplus-livesaas/generating-ai-live-scripts-zh-CN)。

你可以查看预计播报时长和字符数，并点击 **试听脚本**，在开播前听取所选声音的播报效果。

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fd5a3aef27847b58d9e7b88cb237a31~tplv-goo7wpa0wc-image.image)

你可以添加多条商品脚本，并点击拖拽图标调整顺序。

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ff21d518f5040d7b15809c86712c9b4~tplv-goo7wpa0wc-image.image)

在此添加产品脚本后，其对应的产品知识库也会自动启用用于回复。你可以点击**直播互动**查看设置。

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3ca9fb746dd44fb83c7e40ee0c3bd17~tplv-goo7wpa0wc-image.image)

### 步骤 3：配置互动设置

AI Live 可在直播过程中自动回复观众评论和互动事件。配置 **直播互动**后，AI 主播会在适当时机暂停当前脚本，根据你的知识库、提示词和过滤规则生成回复，然后继续播报脚本。详情请参见 [配置 AI Live 互动](https://docs.byteplus.com/docs/byteplus-livesaas/configuring-ai-live-interactions-zh-CN)。

### 步骤 4：配置推流目的地

设置 AI 推流的目标平台，以便在 TikTok、BytePlus Live 或其他平台进行直播。

1. 在顶部导航栏点击 **直播平台**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6b082de70e24ddc8aa86c4726e151de~tplv-goo7wpa0wc-image.image)

2. 在 **直播平台**对话框中，配置以下设置，然后点击 **保存**。

   |**配置项** |**说明** |
   |---|---|
   |直播平台设置 |选择推流平台：**TikTok**、**BytePlus Live**或**其他**。 |
   |推流方式 |仅当你选择**TikTok**作为直播平台时才会显示此选项。<br><br><br>* **RTMP**：通过 RTMP 协议拉取直播流。详见[通过 RTMP 在 TikTok 上开播](https://docs.byteplus.com/docs/byteplus-livesaas/Synchronizing_a_live_stream_from_AI_Live_to_third-party_platforms-zh-CN)。<br><br>* **虚拟摄像头**。通过 OBS 开启直播。详见[通过 OBS 虚拟摄像头在 TikTok 直播](https://docs.byteplus.com/docs/byteplus-livesaas/Going_live_on_TikTok_via_Digital_Human_and_OBS-zh-CN)。 |
   |TikTok ID |**TikTok 用户 ID**用于从直播中获取观众活动。仅当你选择**TikTok**作为直播平台时，才会显示此选项。按照下方所示，在你的 TikTok 应用中获取该 ID。<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10ac18d800e74e5dbc8c28146e8b1580~tplv-goo7wpa0wc-image.image) |
   |URL服务器 |输入目标平台的推流 URL（RTMP 服务器地址）。详情请见[获取服务器 URL 和流密钥](https://docs.byteplus.com/docs/byteplus-livesaas/Synchronizing_a_live_stream_from_AI_Live_to_third-party_platforms-zh-CN#how-to-synchronize-a-live-stream-to-major-live-streaming-platforms)。 |
   |推流密钥 |输入目标平台的推流密钥。详情请见[获取服务器 URL 和流密钥](https://docs.byteplus.com/docs/byteplus-livesaas/Synchronizing_a_live_stream_from_AI_Live_to_third-party_platforms-zh-CN#how-to-synchronize-a-live-stream-to-major-live-streaming-platforms)。 |
   |推流 |启用此选项，将 Avatar 的直播流推送到所选平台。 |

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9269d0affec041ab96bc5e24801eb065~tplv-goo7wpa0wc-image.image)

### （可选）步骤 5：添加直播水印

添加水印，例如“AI 生成”标签，显示在直播画面右下角。

1. 在右上工具栏点击 **更多**（ **...** ）图标，然后选择 **直播设置**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36909d863cff43708758decab9fe46ef~tplv-goo7wpa0wc-image.image)

2. 在 **直播设置**对话框中，开启 **直播水印**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e99ea7d2eef42e1873b375b1eeef501~tplv-goo7wpa0wc-image.image)

3. 点击 **上传图片**上传你的水印 logo，然后点击 **保存**。图片需满足以下要求：

   * **格式**：JPG 或 PNG

   * **最大大小**：500 KB

   * **最大尺寸**：540px（宽）× 300px（高）

### 第6步：开启直播并管理直播流

在你开始直播前，BytePlus Live 会运行**直播设置**配置流程，检查你的内容、加载 Avatar，并在开播前确认直播流目的地。

1. 点击**开始直播**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/311ca298ee63456b814fbd870c404605~tplv-goo7wpa0wc-image.image)

   **直播设置**配置流程将在**直播间内容检查**环节启动。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b069c5c5cf440fdb23ce9eb375db610~tplv-goo7wpa0wc-image.image)

2. 审核开播前的内容。如有检查项提示警告，点击**修改内容**返回并修正你的脚本或知识库，然后重新开始。

   |**检查项** |**要求** |
   |---|---|
   |脚本检查 |建议预计直播时长**超过 30 分钟**。若低于此时长，请参考[生成直播脚本](https://docs.byteplus.com/docs/byteplus-livesaas/generating-ai-live-scripts-zh-CN)丰富脚本内容。 |
   |重复检查 |不允许长篇完全重复的脚本。 |
   |知识库检查 |请**至少添加一个知识库**，以便 AI 主播能正确回答观众问题。 |

3. 设置直播时长，然后点击**下一步**。

4. 在直播时长下，选择**脚本结束后结束直播**或**直播指定小时数**，配置所需设置后，点击**下一步**。

   如果选择**直播指定小时数**，建议开启 AI 重写功能以避免脚本重复。

   > **说明**

   > 你可以将直播时长设置为最长24小时。当设置时长结束后，直播会自动关闭。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b70fd0fa53404d568a9b9738961799e1~tplv-goo7wpa0wc-image.image)

5. 等待**Avatar资源加载**完成后，点击**下一步**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ced49870982b4c9cb9d71ac0725561e0~tplv-goo7wpa0wc-image.image)

   > **说明**

   > 加载 Avatar 需要时间（已有 Avatar 约1分钟，新建 Avatar 约10分钟）。请耐心等待。

6. 确认你在第 4 步配置的推流目的地，然后点击**保存**开始直播。直播开始后，虚拟形象将开始朗读脚本。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04e36f806a7f4656a1d805a2fd144985~tplv-goo7wpa0wc-image.image)

7. 在**聊天**列表中，你可以按状态筛选评论：规则拦截、未读或已读。

8. 点击**结束直播**以停止直播。

## 常见问题

### **问：部分观众昵称包含表情符号和不可读符号。我应该怎么做？**

在你的 AI 回复设置的**提示词**中添加指令，使 AI 在回复前将不可读昵称转换为可读文本。例如，将以下内容添加到你的提示词：

```Plain
If the username is emoji or unreadable symbol, transform those into readable before answering the question.
```
