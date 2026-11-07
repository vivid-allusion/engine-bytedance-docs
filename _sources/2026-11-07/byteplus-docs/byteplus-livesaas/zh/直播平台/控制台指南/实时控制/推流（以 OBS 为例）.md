---
title: "推流（以 OBS 为例）"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-pushing-streams-zh-CN"
---

你可以通过第三方直播工具向 BytePlus Live 的直播间推流。本文以 Open Broadcaster Software（OBS）为例进行说明。

<span id="context"></span>
## 背景

[OBS](https://obsproject.com/) 是一款适用于 Windows、macOS 和 Linux 的免费视频录制和直播流的开源软件。如需了解更多信息，请参见 [OBS 用户指南](https://obsproject.com/help)。

<span id="prerequisites"></span>
## 前提条件


* 点击 [此处](https://obsproject.com/download) 下载并安装 OBS。

* 请确保你的计算机满足 OBS 的相应系统要求。如需了解更多信息，请参见 [系统要求](https://obsproject.com/kb/system-requirements)。


<span id="procedure"></span>
## 操作步骤

<span id="step-1-configure-obs-to-push-your-live-stream-to-a-live-room-in-byteplus-live"></span>
### Step 1: 配置 OBS，将你的直播流推送到 BytePlus Live 的直播间


1. 登录 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 在直播间列表中，点击打开一个直播间。

3. 在 **直播控制** 页面下的播放器区域，点击 **推流**，位于 **推流方式** 标签页。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ca0e9561ea049e98ea5663b383078d0~tplv-goo7wpa0wc-image.image) </span>

4. 复制服务器 URL 和流密钥。

   请妥善保管你的服务器 URL 和流密钥。任何获得服务器 URL 和流密钥的人都可以向你的直播间推送直播内容。

5. 打开 OBS，在左上角点击 **文件** \> **设置**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08fa3af089314917b7f3eb826da39c7b~tplv-goo7wpa0wc-image.image) </span>

6. 在 **设置** 对话框中，点击左侧导航栏的 **流**，并选择 **自定义...** ，从 **服务** 下拉列表中选择。

7. 将第 4 步中复制的服务器 URL 和流密钥分别输入到 **服务器** 和 **流密钥** 字段中，然后点击 **确定**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a31253b2bba406a80eebfe44471e1a9~tplv-goo7wpa0wc-image.image) </span>

8. （可选）如果已开启超低延迟功能，请完成以下配置，以确保观众能够以超低延迟观看直播流内容，然后点击 **确定**。如需了解如何开启超低延迟功能，请参见 [超低延时直播](https://docs.byteplus.com/docs/byteplus-livesaas/docs-ultra-low-latency-zh-CN)。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2bb73794258f45958dbcac83c27a8b89~tplv-goo7wpa0wc-image.image) </span>

   * 更高的码率需要更多的上行带宽。

   * 你必须将 **关键帧间隔** 设置为 1 秒或 2 秒。


<span id="step-2-add-sources"></span>
### Step 2: 添加信号源

添加你希望观众在直播过程中观看的信号源。本例中，你将添加一个显示捕获信号源用于直播你的屏幕内容。


1. 在 OBS 底部的 **信号源** 区域点击 +。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ead6c723b104c2094165a6c7c1dd8aa~tplv-goo7wpa0wc-image.image) </span>

2. 从下拉列表中选择 **显示捕获**。

3. 在弹出的 **创建/选择信号源** 对话框中输入名称并点击 **确定**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69b7048f31854fd3a42673b6167b63e4~tplv-goo7wpa0wc-image.image) </span>

4. （可选）在弹出的对话框中，根据需要调整设置，例如是否捕获鼠标光标。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd1789c442c5434d86fa70047dd20c08~tplv-goo7wpa0wc-image.image) </span>

5. 点击 **确定**。


<span id="step-3-start-a-live-stream"></span>
### Step 3: 开播


1. 在 OBS 右下角点击 **开始推流** 以开播。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07085d4f62d94829a1996dd3239fad74~tplv-goo7wpa0wc-image.image) </span>

2. 观众随后可以在 BytePlus Live 的观看页观看你的直播内容。

   从 OBS 向 BytePlus Live 直播间推流可能会引入一定的延迟。
