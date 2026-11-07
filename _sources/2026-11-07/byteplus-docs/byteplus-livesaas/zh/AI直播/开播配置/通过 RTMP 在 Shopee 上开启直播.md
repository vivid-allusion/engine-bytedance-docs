---
title: "通过 RTMP 在 Shopee 上开启直播"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/going-live-on-shopee-via-rtmp-zh-CN"
---

你可以通过 RTMP 将 BytePlus AI Live 直播流推送到 Shopee，让观众可以在 Shopee 上观看你的 AI 形象。本指南介绍如何在 AI Live 中将 Shopee 配置为直播目的地、从 Shopee 获取服务器 URL 和流密钥，以及使用 Live Connector 浏览器扩展转发观众评论。配置评论同步后，你的 AI 形象可以根据知识库和提示生成并播报回复。

## 前提条件

* 你已设置 AI 直播间，并准备开始直播。更多信息，请参见[启动 AI Live](https://docs.byteplus.com/docs/byteplus-livesaas/start-a-digital-human-livestream-zh-CN)。

* 你拥有在 Shopee 上直播的权限，并可从 Shopee 直播后台获取 RTMP 服务器 URL 和流密钥。

* 为了让你的 AI 形象回复观众评论，你已准备并配置了用于回复的知识库。更多信息，请参见[配置知识库](https://docs.byteplus.com/docs/byteplus-livesaas/prepare-and-upload-knowledge-base-file-zh-CN)。

* 为收集评论，你已安装 Google Chrome 或 Microsoft Edge，并联系 BytePlus 技术支持获取**Live Connector**扩展包。

## 操作步骤

### 步骤 1：在 AI Live 中配置 Shopee RTMP 推流设置

在 AI Live 中，在**直播平台**对话框内配置 Shopee 的 RTMP 推流设置。

1. 登录[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)，并打开你想要推流的 AI 直播间。

2. 在顶部导航栏，点击**直播平台**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6b082de70e24ddc8aa86c4726e151de~tplv-goo7wpa0wc-image.image)

3. 在**直播平台**对话框中，配置以下设置，然后点击**保存**。

   |配置 |描述 |
   |---|---|
   |直播平台设置 |选择 **Other**，将 Shopee 配置为直播流目标。 |
   |平台名称 |输入名称，例如 `Shopee`，以便识别直播流目标。 |
   |URL 服务器 |输入当前 Shopee 直播流的 RTMP 服务器 URL。在 Shopee 直播控制面板中创建直播流，以获取其服务器 URL 和流密钥。<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de402a754958448c8ad6747bdf7e44de~tplv-goo7wpa0wc-image.image) |
   |流密钥 |输入与上述服务器 URL 关联的 Shopee 流密钥。 |
   |流推送 |启用此选项，将你的 AI 直播流推送至 Shopee。 |

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6143bd00a92c4ada8b19ea234a4487f6~tplv-goo7wpa0wc-image.image)

### 步骤 2：在 AI Live 和 Shopee 中开启直播流

1. 启动你的 AI Live。更多信息，请参见[启动 AI Live](https://docs.byteplus.com/docs/byteplus-livesaas/start-a-digital-human-livestream-zh-CN)。

2. 打开当前直播流的 Shopee 直播后台。确认 Shopee 已接收到来自 BytePlus 的视频和音频后，点击右上角的**Go Live**。

3. 确认 Shopee 页面显示**Live**及已直播时长。

### （可选）步骤 3：将 Shopee 观众评论转发到你的 AI 直播间

使用**Live Connector**浏览器扩展，从 Shopee 直播后台收集观众评论，并发送到你指定的 BytePlus AI 直播间。你的 AI 形象随后可以根据知识库和提示生成并播报回复。

下方展示的 Live Connector 界面为中文。本指南保留中文标签，并提供英文说明，帮助你定位各控件。

#### 步骤 1：安装 Live Connector

1. 联系 BytePlus 技术支持获取 Live Connector 扩展包，并解压到本地文件夹。

2. 打开 Chrome 或 Edge。在地址栏输入`chrome://extensions/`（Chrome）或`edge://extensions/`（Edge），打开扩展管理页面。

3. 开启**开发者模式**。

4. 点击**加载已解压**，并选择已解压的 Live Connector 扩展文件夹。

5. 确认**Live Connector**已出现在扩展列表中并已开启。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/322b352162ef416c802a15d7e0b090d2~tplv-goo7wpa0wc-image.image)

6. 点击浏览器地址栏右侧的**扩展**图标，然后点击**Live Connector**。扩展将在浏览器侧边栏打开。你也可以将扩展固定到工具栏以便快速访问。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0afeaaa89b5452fa3157d1d94dbf7d3~tplv-goo7wpa0wc-image.image)

#### 步骤 2：连接你的 BytePlus 账号

1. 在扩展程序的**登录 BytePlus**步骤，点击**去 BytePlus 登录**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47536cdfd0364931baf73e69dd38a398~tplv-goo7wpa0wc-image.image)

2. 在弹出的 BytePlus 页面完成登录。使用拥有本次直播流的 AI 直播间的账号，并在安装了 Live Connector 的同一浏览器及浏览器配置文件中完成登录。

3. 返回扩展程序，点击**我已登录，连接账号**。

4. 在**选择直播间**步骤，确认扩展程序显示的是拥有你的 AI 直播间的账号，并且状态为**BytePlus 已连接**。如需切换账号，点击**更换账号**，然后重新登录并连接。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/610f294649944ad889cbcb5a6e75d7a9~tplv-goo7wpa0wc-image.image)

#### 步骤 3：识别 Shopee 直播流并输入你的 BytePlus AI 直播间 ID

1. 在安装了 Live Connector 的浏览器中登录 Shopee，并打开你在步骤 2 启动的直播流的控制面板。

2. 确认 Shopee 直播流正在运行。扩展程序会自动检测到该流，并在**采集来源**下显示其信息，状态为**直播中**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f639db64f1f487b929480ce87ace7fd~tplv-goo7wpa0wc-image.image)

3. 在 BytePlus Live 控制台中，打开正在向 Shopee 推流的 AI 直播间，并复制其 ID（`ActivityId`）。将其粘贴到扩展程序的**上报目标**字段。请使用当前正在直播的 BytePlus AI 直播间的 ID，而非 Shopee 直播间的 ID。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/351bafca8b4c4c7187423c1edaeb4d6d~tplv-goo7wpa0wc-image.image)

4. 确认采集来源和上报目标无误后，点击**下一步**，进入**开始同步**步骤。

#### 步骤 4：开始同步评论并验证 AI 回复

1. 在**确认连接，开始同步**页面，再次检查 Shopee 评论采集来源和 BytePlus 直播间上报目标，然后点击**开始同步评论**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1aed26aa899d4b5a926a4ab9d6ef8194~tplv-goo7wpa0wc-image.image)

2. 确认扩展程序显示**连接完成**、状态为**同步中**，并有**停止同步**按钮。保持浏览器和 Shopee 直播控制面板处于打开状态，并保持登录。**关闭 Shopee 直播控制面板会停止评论采集。**

3. 使用观众账号在当前 Shopee 直播流中发布新的测试评论。提出一个你的知识库可以回答的问题，然后检查以下内容：

   * 该评论出现在 Shopee 直播控制面板的**Comments**区域。

   * 同样的评论会出现在扩展程序的**最近评论**区域，并且**已同步评论**计数增加。

   * 该评论出现在你的 BytePlus AI 直播间的**Chats**列表中。

4. 作为 Shopee 观众收听直播流，并确认 AI 形象给出相关回复。评论出现在扩展程序中并不代表 AI 形象已生成或说出回复。还需检查 BytePlus 是否收到该评论，以及回复是否在直播流中可听见。

## 常见问题

### 为什么启动 AI Live 后 Shopee 没有视频？

在**直播平台**对话框中，检查**推流**是否已开启，并确认**URL Server**和**Stream Key**与 Shopee 直播控制面板中当前流提供的值一致。同时确认你已完成在 Shopee 上开播的相关步骤。

### 如果评论来源显示为 待识别（Not yet detected）或 正在等待聊天连接…（Waiting for the chat connection），我应该怎么办？

确认你已在安装 Live Connector 的同一 Chrome 或 Edge 浏览器配置文件中登录 Shopee，并且当前直播流的控制面板已打开。根据 Shopee 页面显示的状态，按照指引操作：

* **流尚未开始：** 确认 Shopee 已收到流，然后点击 **Go Live**。扩展程序会自动检测页面状态。等待状态变为 **直播中**（Live）；无需手动刷新页面。

* **流正在进行：** 确认页面显示 **Live** 及已直播的时间。保持控制面板打开，并检查页面是否正确加载。

* **流已结束：** 如果页面显示 **Live Ended**，则流已结束。开启新的流后，请再次确认评论来源和目标直播间，并开始同步评论。

### 为什么我的 AI 形象没有回复 Shopee 评论？

首先，在 BytePlus AI 直播间的 **Chats** 列表中检查评论是否已到达：

* **评论未到达：** 确认 Shopee 直播控制面板的 **Comments** 下有新的评论出现。然后确认扩展程序显示 **同步中**（Syncing），评论出现在 **最近评论**（Recent comments）下，且 **已同步评论**（Synced comments）数量增加。同时检查已连接的 BytePlus 账号和目标直播间。`ActivityId` 必须识别该账号下当前正在直播的 AI 直播间。保持 Shopee 直播控制面板处于打开状态。

* **评论已到达：** 检查过滤规则是否屏蔽了评论，以及直播间是否已配置知识库和评论回复设置。更多信息请参见 [启动 AI Live](https://docs.byteplus.com/docs/byteplus-livesaas/start-a-digital-human-livestream-zh-CN)。
