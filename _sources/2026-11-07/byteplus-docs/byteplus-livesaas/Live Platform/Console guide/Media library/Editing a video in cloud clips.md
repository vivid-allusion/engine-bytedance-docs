---
title: "Editing a video in cloud clips"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/editing-a-video-in-cloud-clips"
---

You can use cloud clips to edit videos in the cloud, which makes video editing more efficient, more convenient, and easier.

<span id="c8f8cf5c"></span>
## Context

By using cloud clips, you can edit videos in the cloud without downloading any software, which is both easy and time\-saving. In addition, the cloud clips feature works seamlessly with playbacks. After a playback is generated, you can edit the playback in cloud clips based on your requirements.

<span id="b4488631"></span>
## Page overview

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38ffffa4a7274400803a71b2c6d39c4b~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Name** |**Description** |
|---|---|---|
|1 |Material area |Select and drag a video on the **Video library**, **Live caching**, or **Live** tab to the track in the working area.<br><br><br>* **Video library**: Existing videos in the video library.<br><br>* **Live caching**: Playbacks automatically generated after live streams end, which are stored on the **Media library** \> **Videos** \> **Temporary storage** page.<br><br>* **Live**: Live videos. For more information on how to edit live videos, see [Editing a live video](https://docs.byteplus.com/docs/byteplus-livesaas/editing-a-live-video).<br><br><br>You can also click **Local file** to upload a local video to the video library and then select and drag the video on the **Video library** tab to the track. |
|2 |Preview area |Control the video on the track in real time by using play control components, preview the video on the track, and change the canvas size. |
|3 |Play control components |Play, fast forward, and rewind the video on the track, and jump to the start point and end point of the selected video. |
|4 |Working area |Edit the video, including splitting and deleting the selected video, selecting and dragging the video to adjust the sequence, adjusting the video volume, and zooming in or out the view on the track. |
|5 |Undo |Click the **Undo** icon to cancel the previous operation. To undo multiple operations, you can repeatedly click the icon. |
|6 |Redo |Click the **Redo** icon to restore the undone operation. To restore multiple operations, you can repeatedly click the icon. |
|7 |Split |Locate where you want to split the video and click the **Split** icon to split the selected video into two parts. |
|8 |Delete |Select the video that you want to delete and click the **Delete** icon. |
|9 |Adjust volume |Adjust the volume of the video. |
|10 |Zoom in or out the view on the track |Zoom in or out the view on the track, thereby adjusting the granularity in the timeline. |


<span id="63fe2034"></span>
## Prerequisite

A BytePlus account or an IAM user with **Cloud clips** \> **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

<span id="374bda20"></span>
## Procedure


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. You can use one of the following ways to enter the **Cloud clips** page.

   * On BytePlus Live's menu bar, click **Media library**. On the left navigation pane, click **Videos** \> **Video library** or **Temporary storage**. On the right of the target video, click **Clip** in the **Actions** column.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aecf06a6102c4095a603b240d7a76608~tplv-goo7wpa0wc-image.image) </span>

   * On BytePlus Live's menu bar, click **Media library**. On the left navigation pane, click **Cloud clips**. Click **New clip** or **Enter the Cloud clips page** on an existing clip project.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55ee18dcf5d84071acb3bafd5c041573~tplv-goo7wpa0wc-image.image) </span>

   * On the live room list, click to open a live room. On the left navigation pane, click **Playbacks**. On the right of the target video, click **Clip** in the **Actions** column.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc6ea59201ac4edeb07aab884ca124a1~tplv-goo7wpa0wc-image.image) </span>

3. Select and drag a video in the material area to the track in the working area.

4. Edit the video based on your requirements. In this topic, take the following two scenarios as examples.

   * Delete the beginning and the end of a video: The playback usually contains the test content before the live stream starts. Use cloud clips to delete the beginning and the end of a playback so that the test content can be deleted.

      1. Locate where you want to split the video at the beginning of the playback and click the **Split** icon to split the selected video into two parts.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c5394b5e47b43cb8478c6d6d641f1f3~tplv-goo7wpa0wc-image.image) </span>

      2. Select the part that you want to delete and click the **Delete** icon or press Delete or Backspace on your keyboard to delete the beginning of the playback.

      3. Locate where you want to split the video at the end of the playback and click the **Split** icon.

      4. Select the part that you want to delete and click the **Delete** icon or press Delete or Backspace on your keyboard to delete the end of the playback.

   * Merge videos: Use cloud clips to merge multiple playbacks into one video. You can also add a local video to the merged playback as the transition.

      1. Select and drag multiple videos in the material area to the track in the working area. Videos are automatically merged.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ea3082a784440f18bae71eba1dee45e~tplv-goo7wpa0wc-image.image) </span>

      2. (Optional) Select and drag the video on the track to adjust the sequence.

5. (Optional) You can save your current editing progress to **Media library** \> **Cloud clips**. Click **Save** in the upper\-right corner of the page and enter the project name in the dialog box that appears. Then, click **Confirm**. You can then select the existing clip project to continue editing from the current progress.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26faa9adb8fb4cfb97c94bda7edb31f5~tplv-goo7wpa0wc-image.image) </span>

6. Click **Export to video library** in the upper\-right corner of the page to export the video clip to the video library for permanent storage. In the **Export to video library** dialog box that appears, enter the video name, select the video quality, and then click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0338205fbeb241b2a9050760a1322763~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We recommend that you keep the length of the video to within three hours. Otherwise, it will take a long time to export the video clip to the video library.   </div>
   

7. (Optional) After the video clip is exported to the video library, you can download the video clip or release the video clip as the playback of a live room.

   * Download the video clip

      1. On BytePlus Live's menu bar, click **Media library**.

      2. On the left navigation pane, click **Videos** \> **Video library**.

      3. On the right of the video clip, click **Download** in the **Actions** column.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77cf40c2f5234c689a3916fab0c3480a~tplv-goo7wpa0wc-image.image) </span>

   * Release the video clip

      1. On the live room list, click to open a live room.

      2. On the left navigation pane, click **Playbacks**.

      3. Click **Select from video library** in the upper\-right corner.

      4. Select the video clip and click **OK**.

      5. On the right of the video clip, click **Release** in the **Actions** column.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5bc3164ff0e34d41b10a48d8fd2df593~tplv-goo7wpa0wc-image.image) </span>
