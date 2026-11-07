---
title: "将观众踢出或屏蔽观众的 IP 地址"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-kick-out-or-block-zh-CN"
---

为维护秩序并确保直播流期间观众获得良好的观看体验，您可以通过将扰乱秩序的观众踢出房间或屏蔽其 IP 地址来进行管理。本指南提供了使用这些功能以便及时移除不守规矩参与者的分步操作说明。

<span id="prerequisites"></span>
## 前提条件


* 拥有 BytePlus 账号或具备 Live control \> Edit 权限的 IAM 用户。有关如何添加 IAM 用户的更多信息，请参见 [管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles-zh-CN)。

* 聊天互动菜单。更多信息，请参见 [管理聊天区域](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-chat-area-zh-CN)。


<span id="scenarios"></span>
## 使用场景

在直播流过程中，可能会出现扰乱直播间并影响其他观众体验的行为，例如：


* 刷屏

* 发送不当评论

* 传播虚假信息

* 骚扰其他观众


为保障直播流的顺利进行，您可以将观众踢出直播间或屏蔽观众的 IP 地址。

<span id="procedure"></span>
## 操作流程

您可以在聊天互动菜单或 **观众列表**页面执行这些操作。这两处均可在 BytePlus Live 控制台和网页版直播页面访问。

各处操作步骤基本一致。本主题以 BytePlus Live 控制台的聊天互动菜单为例进行说明。


1. 登录 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 在直播间列表中，点击打开一个直播间。

3. 在 **Live control**页面的聊天互动菜单中，点击评论右侧的省略号图标，然后选择 **踢出**或**屏蔽 IP**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90ae8cf49d0c48dea8f62a77920cb072~tplv-goo7wpa0wc-image.image) </span>

   * 将观众踢出直播间：选择 **踢出**后，发送该评论的观众会被踢出直播间，无法重新加入直播间。该评论也会从公共聊天中删除。如需允许观众重新加入直播间，点击该观众发送评论右侧的省略号图标，选择 **取消踢出**。

      观众通过其用户 ID 和设备 ID 进行识别。若被踢出的观众通过不同的登录方式或设备重新加入，则会被视为新观众，可以进入房间。

   * 屏蔽观众的 IP 地址：选择 **屏蔽 IP**后，发送该评论的观众会被踢出直播间，并且来自被屏蔽 IP 地址的任何人都无法进入直播间。该评论也会从公共聊天中删除。如需解除 IP 地址屏蔽，点击该观众发送评论右侧的省略号图标，选择 **解除屏蔽**。


<span id="what-your-viewers-see"></span>
## 观众看到的内容


|功能 |在 PC 上 |在移动设备上 |
|---|---|---|
|已被踢出直播间 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fefad6f79fb48f5a197beb1df8a2ede~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a10c51f2ad34744b04f2af8486740af~tplv-goo7wpa0wc-image.image) </span> |
|IP 地址已被屏蔽 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/523aa832b4b646e5ab22d166a0ff2d3d~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efe708030403412c9304a418155a8dbf~tplv-goo7wpa0wc-image.image) </span> |
