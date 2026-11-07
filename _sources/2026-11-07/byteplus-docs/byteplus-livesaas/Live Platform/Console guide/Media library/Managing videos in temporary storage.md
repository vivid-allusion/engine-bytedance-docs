---
title: "Managing videos in temporary storage"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-managing-videos-in-the-media-library"
---

After a live stream ends, a video recording the live content (namely the playback) is automatically generated and stored in temporary storage. You can perform operations such as downloading the video or transferring the video to video library on the **Temporary storage** page.

<span id="df8a5a0c"></span>
## Prerequisite

A BytePlus account or an IAM user with **Live temporary** \> **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

<span id="1488df06"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The maximum duration for a playback is 12 hours. If a live stream lasts longer than this, for example, 15 hours, a 12\-hour playback and a 3\-hour playback will be generated.</div>


* <div data-tips="true" data-tips-type="tip">Videos in temporary storage will be kept for 180 days and automatically deleted after the expiration time.</div>


* <div data-tips="true" data-tips-type="tip">Videos in temporary storage do not consume the media library capacity package.</div>


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On BytePlus Live's menu bar, click **Media library**.

3. On the left navigation pane, click **Videos** \> **Temporary storage**.

4. On the **Temporary storage** page, you can perform the following operations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed622bc073eb43a88c1802a8b2a22ca5~tplv-goo7wpa0wc-image.image) </span>

   * Search for specific videos based on the video name and video ID. The video name supports fuzzy search.

   * View the cover, duration, name, ID, generation time, expiration time, and associated live rooms of a video.

   * Modify the video name, copy the video ID, or update the cover image.

   * Click the associated live room name to go to the **Live control** page of the live room.

   * Move your pointer over a video and click the play icon to play the video.

   * View the video source. The source **Recording** indicates videos are automatically generated after the live stream ends. Therefore, videos in temporary storage have only one source: **Recording**.

   * Click **Clip** to clip a video online. For more information, see [Editing a video in cloud clips](https://docs.byteplus.com/docs/byteplus-livesaas/editing-a-video-in-cloud-clips).

   * Click **Download** to download a video.

   * Click **Delete** to delete a video or select one or more videos and then click **Delete** to delete multiple videos at a time.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Videos are unavailable in associated live rooms after deletion. Proceed with caution.      </div>
      

   * Select one or more videos and then click **Transfer to video library**. Select a category in the displayed dialog box to transfer the video to the selected category on the **Media library** \> **Videos** \> **Video library** page. Then, the selected videos are deleted from temporary storage and stored in the video library permanently.
