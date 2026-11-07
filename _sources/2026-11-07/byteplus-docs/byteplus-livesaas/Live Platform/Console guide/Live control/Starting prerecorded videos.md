---
title: "Starting prerecorded videos"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-starting-the-carousel"
---

To schedule prerecorded videos to go live, you can use the prerecorded video broadcast method to loop videos as a live stream. This guide provides step\-by\-step instructions on how to add videos, manage your video list, and start the stream.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Prerecorded videos do not support the <a href="https://docs.byteplus.com/zh-CN/docs/byteplus-livesaas/docs-synchronizing-a-live-stream-from-byteplus-live-to-third-party-platforms">multi\-platform streaming</a> feature. To synchronize a live stream from BytePlus Live to third\-party platforms, select another broadcast method. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-your-web-browser">Live streaming from your web browser</a>, <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-pulling-streams">Pulling streams</a>, <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-pushing-streams">Pushing streams (Using OBS as an example)</a>, <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-ios-phone">Live streaming from an iOS phone</a>, or <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-android-phone">Live streaming from an Android phone</a>.</div>


<span id="6dffa3e0"></span>
## What your viewers see


<Tabs>
<Tab zoneid="zMQ3PejNpc" title="Viewers on PCs">
<TabTitle>Viewers on PCs</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25bafb534e5e45d0bfafb4eabc9407be~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="xYtrpJZGwH" title="Viewers on mobile devices">
<TabTitle>Viewers on mobile devices</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d483928a913e44fd84ca684b0b7078b8~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


The program list feature is only supported on PCs and mobile devices in landscape mode.

The time interval in the program list indicates the start and end times of the video. For example, if the time interval is 02:49 to 02:52, it means the video starts playing at 02:49 and ends at 02:52.

<span id="22b436c8"></span>
## Prerequisite

You must have a BytePlus account or an IAM user with **Live control** \> **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

<span id="0060ffcf"></span>
## Procedure


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the live room list, click a live room to open it.

3. On the **Broadcast method** tab under the player, click **Prerecorded video**.

4. Click **Edit video list**.

   If you have multiple live sources in the live room, select the corresponding source from the **Switch source** drop\-down list before completing this step. For more information on how to configure live sources, see [Managing live sources](https://docs.byteplus.com/docs/byteplus-livesaas/docs-setting-multi-source-live-streaming).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef61ee4752da473baada1a789defbdc6~tplv-goo7wpa0wc-image.image) </span>

5. In the **Edit video list** dialog box, add videos in one of the following ways. You can add up to 50 videos, and the total size of the videos cannot exceed 200 GB.

   * Click **Select from video library** to add a video from the library.

   * Click **Upload video** to upload an MP4 video.

6. (Optional) Configure the following settings and then click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba352b1e66ba40b78ae328d14b6269ee~tplv-goo7wpa0wc-image.image) </span>

   * Drag to adjust the order of the videos in the video list.

   * Modify the video name.

   * Click the **Copy** icon next to the ID to copy the video ID.

   * Click **Edit** in the **Start time** column to modify the start time of the video. After the prerecorded video starts, the video plays from this start time.

   * Delete specific videos.

   * If two or more videos are added, you can turn on the **Show program list** switch and enter the program list name. After the prerecorded videos start, the program list appears on the viewing page for viewers on PCs and mobile devices in landscape mode.

7. Click **Start stream** to loop the videos on the viewing page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/286da75be2664f6dac2ad991d7fe289e~tplv-goo7wpa0wc-image.image) </span>

   If you have multiple live sources in the live room, a confirmation message appears after you click **Start stream**. Click **OK** to start the stream for all sources, or click **Single source** to start it for the current source only. For more information about how to configure multiple live sources, see [Managing live sources](https://docs.byteplus.com/docs/byteplus-livesaas/docs-setting-multi-source-live-streaming).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a1e07d69e0a947238e026c1deacfdfe5~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Primary and backup streams are supported to ensure a smooth viewing experience. For more information on how to enable the primary and backup streams, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-setting-multi-source-live-streaming">Managing live sources</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can configure an automatic start for prerecorded videos. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-setting-an-auto-start">Setting an auto\-start</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Videos start to pre\-warm automatically after being added. To ensure better live streaming quality, we recommend that you start prerecorded videos after the pre\-warming is complete.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The pre\-warmed status is retained for one day. After one day, you must manually click <strong>Pre\-warm</strong> in the <strong>Pre\-warming progress</strong> column to pre\-warm all the videos in the current live source.   </div>
   

8. Click **End stream** to end the prerecorded video stream.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71fb1cabf86b431a8971eff5fc3bac8d~tplv-goo7wpa0wc-image.image) </span>

   If you have multiple live sources in the live room, a confirmation message appears after you click **End stream**. Click **OK** to end the stream for all sources, or click **Single source** to end it for the current source only. For more information about how to configure multiple live sources, see [Managing live sources](https://docs.byteplus.com/docs/byteplus-livesaas/docs-setting-multi-source-live-streaming).
