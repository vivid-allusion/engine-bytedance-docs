---
title: "Pushing streams (Using OBS as an example)"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-pushing-streams"
---

You can push streams from third\-party live streaming tools to a live room in BytePlus Live. Here, the tool Open Broadcaster Software (OBS) is used as an example.

<span id="380dceb6"></span>
## Context

[OBS](https://obsproject.com/), available for Windows, macOS, and Linux, is a free and open source software for video recording and live streaming. For more information, see the [OBS User Guide](https://obsproject.com/help).

<span id="d5511941"></span>
## Prerequisites


* Click [here](https://obsproject.com/download) to download OBS and install it.

* Make sure your computer meets the corresponding system requirements for OBS. For more information, see [System requirements](https://obsproject.com/kb/system-requirements).


<span id="e3144fe9"></span>
## Procedure

<span id="733e0d7a"></span>
### Step 1: Configure OBS to push your live stream to a live room in BytePlus Live


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the live room list, click to open a live room.

3. On the **Live control** page, click **Push stream** on the **Broadcast method** tab under the player.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ca0e9561ea049e98ea5663b383078d0~tplv-goo7wpa0wc-image.image) </span>

4. Copy the server URL and stream key.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Keep your server URL and stream key confidential. Anyone who has the server URL and stream key can push live content to your live room.   </div>
   

5. Open your OBS and click **File** \> **Settings** in the upper\-left corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08fa3af089314917b7f3eb826da39c7b~tplv-goo7wpa0wc-image.image) </span>

6. In the **Settings** dialog box, click **Stream** on the left navigation pane and select **Custom...**  from the **Service** drop\-down list.

7. Enter the server URL and stream key copied in step 4 into the **Server** and **Stream Key** fields, and then click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a31253b2bba406a80eebfe44471e1a9~tplv-goo7wpa0wc-image.image) </span>

8. (Optional) If the ultra\-low latency feature is enabled, complete the following configurations to ensure viewers can watch the stream with ultra\-low latency, and then click **OK**. To learn how to enable the ultra\-low latency feature, see [Ultra-low latency live streaming](https://docs.byteplus.com/docs/byteplus-livesaas/ultra-low-latency-live-streaming).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2bb73794258f45958dbcac83c27a8b89~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">A higher bitrate requires more upstream bandwidth.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You must set the <strong>Keyframe Interval</strong> to 1 s or 2 s.   </div>
   


<span id="e444c779"></span>
### Step 2: Add sources

Add the sources that you want viewers to watch during the live stream. In this example, you will add a Display Capture source to stream your screen.


1. Click + in the **Sources** section at the bottom of OBS.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ead6c723b104c2094165a6c7c1dd8aa~tplv-goo7wpa0wc-image.image) </span>

2. Select **Display Capture** from the drop\-down list.

3. Enter a name and click **OK** in the **Create/Select Source** dialog box that appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69b7048f31854fd3a42673b6167b63e4~tplv-goo7wpa0wc-image.image) </span>

4. (Optional) In the dialog box that appears, adjust the settings as needed, such as whether to capture your cursor.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd1789c442c5434d86fa70047dd20c08~tplv-goo7wpa0wc-image.image) </span>

5. Click **OK**.


<span id="1fd2dcd6"></span>
### Step 3: Start a live stream


1. Click **Start Streaming** in the lower\-right corner of OBS to start a live stream.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07085d4f62d94829a1996dd3239fad74~tplv-goo7wpa0wc-image.image) </span>

2. Viewers can then watch your live content on the viewing page of BytePlus Live.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Pushing the stream from OBS to the BytePlus Live room may introduce some latency.   </div>
