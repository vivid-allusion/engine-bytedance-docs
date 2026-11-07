---
title: "Managing videos in the video library"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/managing-videos-in-the-video-library"
---

You can manage videos centrally on the **Video library** page, thereby improving the efficiency of video management.

<span id="a5c987b0"></span>
## Prerequisite

A BytePlus account or an IAM user with **Video library** \> **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

<span id="2b5eec79"></span>
## Managing categories


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On BytePlus Live's menu bar, click **Media library**.

3. On the left navigation pane, click **Videos** \> **Video library**.

4. In the category area, you can do the following.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5392eed41b84af4ad2b3913f211abc1~tplv-goo7wpa0wc-image.image) </span>

   * Search for categories by name. Fuzzy search is supported.

   * Click the icon on the left of a category name to expand or collapse the category tree.

   * Click the more icon on the right of a category name and then you can do the following:

      * Click **New sibling** to add a category at the same level as the current category.

      * Click **New child** to add a subcategory under the current category.

      * Click **Rename** to change the name of the current category.

      * Click **Delete** to delete the current category. A category can only be deleted if the category and all its subcategories contain no videos.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The built\-in default category is a root\-level category. You cannot add categories at the same level as the default category, nor rename or delete the default category itself. Videos uploaded locally are saved under the default category.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Up to 7 levels of subcategories are supported.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can add up to 10,000 subcategories.      </div>
      

   * Drag and drop categories to adjust their hierarchy.


<span id="aa2eb77f"></span>
## Managing videos

Videos stored in the video library all consume the media library capacity package and will be saved permanently.


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On BytePlus Live's menu bar, click **Media library**.

3. On the left navigation pane, click **Videos** \> **Video library**.

4. Click a specific category.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/824010f0327645c985113328c2bc30ea~tplv-goo7wpa0wc-image.image) </span>

5. In the video area, you can do the following:

   * Upload videos

      Click **Upload video** to upload one or more local videos in MP4 format. You can upload at most 20 videos at a time and each video cannot exceed 50 GB. You can also view the video upload progress.

   * Filter videos based on any of the following criteria:

      * Whether or not include subcategories.

         * Include: Select **subcategory** from the drop\-down list to display all videos under the current category and its subcategories in the video list.

         * Do not include: Select **Does not contain subcategories** from the drop\-down list to display only videos under the current category in the video list.

      * Video source.

         * **Upload**: Videos uploaded locally.

         * **Recording**: Videos automatically generated after the live stream ends.

         * **Cloud clips**: Videos generated using the cloud clips feature.

      * Video name and video ID. Fuzzy search is supported.

   * Download, delete, or move videos

      * Download or delete a single video

         Click the more icon in the **Actions** column, and then select **Download** or **Delete**. Videos are unavailable in associated live rooms after deletion. Proceed with caution.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59036838dde94e28ab250bd0b3ddebe8~tplv-goo7wpa0wc-image.image) </span>

      * Batch download, delete, or move videos

         Select multiple videos and then do the following.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd9bda036ab345dabe49865b5605b73f~tplv-goo7wpa0wc-image.image) </span>

         * Click **batch movement** to move at most 100 videos to a specific category at a time.

         * Click **batch download** to download at most 20 videos locally at a time.

         * Click **Bulk delete** to delete at most 100 videos at a time. Videos are unavailable in associated live rooms after deletion. Proceed with caution.

   * Clip videos

      Click **Clip** to clip a video online. For more information, see [Editing a video in cloud clips](https://docs.byteplus.com/docs/byteplus-livesaas/editing-a-video-in-cloud-clips).

   * Other actions

      * View the thumbnail, size, duration, name, and ID of a video. You can also modify the video name and click the **Copy** icon next to the video ID to copy the video ID.

      * View the creator and creation time of a video. If videos are transferred from temporary storage to the video library, the creator refers to the user who performed the transfer, and the creation time refers to the time of transfer to the video library.

      * Click the video’s category to view the list of videos under that category.

      * Click **details** and then do the following on the displayed **Video details** page.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71455e7f52694d50a7214dc27f66102d~tplv-goo7wpa0wc-image.image) </span>

         * Preview or replace the video thumbnail.

         * View basic information such as the video name and size.

         * View the live rooms currently using this video. You can also click a live room name to go to the **Live control** page of that live room.
