---
title: "Managing playbacks"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-uploading-a-video-on-demand-vod"
---

BytePlus Live supports the Video\-on\-Demand (VOD) feature. After you release one or more videos in a live room, the player plays these videos sequentially on the viewing page according to their release order.

<span id="8782c299"></span>
## What your viewers see


<Tabs>
<Tab zoneid="dJE0lFHe8b" title="Viewers on PCs">
<TabTitle>Viewers on PCs</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce91c1bface4494ca29b2bb06dbbae28~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="GmRJ8k7x9O" title="Viewers on mobile devices">
<TabTitle>Viewers on mobile devices</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11902b4455f14faca78972bf80821476~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


<span id="0b697af1"></span>
## Prerequisite

A BytePlus account or an IAM user with **Playbacks** \> **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

<span id="76353a03"></span>
## Procedure


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the live room list, click to open a live room.

3. On the left navigation pane, click **Playbacks**. You can manage playbacks that are automatically generated after the live stream ends, or use uploaded videos or videos selected from the video library as playbacks.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b5a508250d0479882f8064942d0f179~tplv-goo7wpa0wc-image.image) </span>

   * Playbacks automatically generated after the live stream ends: The playbacks are stored to the **Media library** \> **Videos** \> **Temporary storage** page.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The maximum duration for a playback is 12 hours. If a live stream lasts longer than this, multiple playbacks will be generated. If you enable the feature of automatically releasing the playback either on the <strong>Producer</strong> \> <strong>Basic information</strong> page of a live room or when creating a live room, only the last playback generated will be released to the viewing page automatically after the live stream ends. For example, if the live stream lasts 15 hours, a 12\-hour playback and a 3\-hour playback will be generated, and the last 3\-hour playback will be released to the viewing page automatically.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Playbacks in temporary storage will be kept for 180 days and automatically deleted after the expiration time.      </div>
      

   * Videos uploaded locally: Click **Upload video** to upload a video from your local device.

   * Videos selected from the video library: Click **Select from video library** and then select up to 10 videos from the video library at a time.

   * **Playback collection name**: Modify the default name for the playback list entry on the viewing page as needed, and then click **Save**. This entry is only visible on the viewing page when multiple videos are released.

   * **Playback bullet comments**: To display the bullet comments switch and hide the menu for chat interaction on the viewing page when the live room is in the **Playback** status, turn on the switch.

   * **Live bullet comments**: To allow viewers to view bullet comments sent during the live stream when the live room is in the **Playback** status, turn on the switch.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">This switch appears only after you turn on the <strong>Playback bullet comments</strong> switch.      </div>
      

4. In the video list, you can do the following.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ed817bc31784e67b85d680f408f6dde~tplv-goo7wpa0wc-image.image) </span>

   * Search for videos by video name or video ID. The video name supports fuzzy search.

   * View the video's cover, duration, name, and ID, and modify the video name. You can also click the **Copy** icon next to the video ID to copy it.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The modified video name only takes effect in the current live room.      </div>
      

   * Click **Update** to update the video cover.

   * View the video's creation time.

   * View the video's source:

      * **Recording**: Videos automatically generated after the live stream ends.

      * **Upload**: Videos uploaded locally or selected from the video library.

   * View the video location:

      * **Live temporary**: **Media library** \> **Videos** \> **Temporary storage** page.

      * **Video library**: **Media library** \> **Videos** \> **Video library** page.

   * Click **Manage** and do the following in the dialog box that appears as needed.

      * On the **Manage bullet comments** tab, view or manage bullet comments sent when the live room is in the **Live** and **Playback** status.

      * On the **Mark points** tab, mark highlights and key moments in the video.

   * Click **Release** or **Withdraw** to release the playback to the viewing page or withdraw the playback from the viewing page. Once the playback finishes playing, viewers must click **replay** on the viewing page to watch the playback again.

      You can also release multiple playbacks, and then BytePlus Live will play them sequentially according to the release order on the viewing page. After all the playbacks finish playing, viewers must click **replay** on the viewing page to start replaying from the first playback in the playback list.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can release up to 200 playback videos.      </div>
      

   * Click **Clip** to clip a video online. For more information, see [Editing a video in cloud clips](https://docs.byteplus.com/docs/byteplus-livesaas/editing-a-video-in-cloud-clips).

   * Click the more icon in the **Actions** column and then you can do the following as needed:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/006b431998a048cc81030528cdaf665d~tplv-goo7wpa0wc-image.image) </span>

      * Select **Download** to download the video.

      * Select **Transfer to video library** and select a category in the displayed dialog box to transfer the video to the selected category on the **Media library** \> **Videos** \> **Video library** page.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">You can only transfer videos whose video location is <strong>Temporary storage</strong>. After the transfer, videos are deleted from the <strong>Media library</strong> \> <strong>Videos</strong> \> <strong>Temporary storage</strong> page, and stored in the video library permanently.         </div>
         

      * Select **Delete** to delete the video from the current live room. You can still view the video on the **Media library** \> **Videos** \> **Temporary storage** or **Video library** page.
