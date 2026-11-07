---
title: "Watermark and ad insertion template"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-watermark-and-ad-insertion-template"
---

To protect your video content with watermarks or monetize it with ads, you can create a reusable template in the BytePlus VOD console. This guide provides step\-by\-step instructions for creating and configuring a template that supports image, video, or text watermarks, as well as pre\-roll and post\-roll in\-stream ads.

<span id="b2358a27"></span>
## Feature overview

BytePlus VOD offers convenient features to enhance your videos: watermarks and ad insertion.

<span id="f958e586"></span>
### Watermarks

A watermark is an overlay that displays logos, text, or other information on a video. It serves purposes like copyright protection, brand promotion, or adding custom details. BytePlus VOD supports visible watermarks, which can display brand names, logos, TV station logos, or app names. You can use images, videos, or text watermarks.

<span id="baba946d"></span>
### Ad insertion

BytePlus VOD supports seamlessly integrating in\-stream ads into the main video content. You can insert pre\-roll or post\-roll ads within the video stream, ensuring a seamless viewing experience for your audience.

<span id="e894ceb7"></span>
## Prerequisites

Depending on the type of watermark you want to add, upload the corresponding materials to the BytePlus VOD console. For details, see [Media upload](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload).

<span id="75aeb68b"></span>
## Creating a watermark and ad insertion template


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Spaces** on the left navigation bar.

3. On the **Spaces** page, click **Enter space**.

4. Click **Media processing \> Templates** on the left navigation bar.

5. Click the **Watermark and ad insertion template** tab.

6. Click **Add template**.

7. In the dialog box that appears, configure the basic information, add watermarks, and set up ad insertion parameters according to your specific business requirements. For details, see the following documentation:

   * [Configuring basic information](https://docs.byteplus.com/docs/byteplus-vod/docs-watermark-and-ad-insertion-template#3b1da254)

   * [Adding visible watermarks](https://docs.byteplus.com/docs/byteplus-vod/docs-watermark-and-ad-insertion-template#7b543274)

   * [Inserting an in-stream ad](https://docs.byteplus.com/docs/byteplus-vod/docs-watermark-and-ad-insertion-template#59794809)

8. Click **Save**.


<span id="3b1da254"></span>
## Configuring the basic information


|**Parameter** |**Description** |
|---|---|
|Template name |The length of the template name cannot exceed 64 characters. It is recommended to use a name that can identify the content of the template. |
|Template description |The length of the template description cannot exceed 140 characters. |
|Watermark and ad label |A unique identifier for the watermark or ad, used to identify and retrieve video files that have been processed by this template from the BytePlus VOD service. Only lowercase letters and underscores are allowed. The label length must be less than 30 characters. |


<span id="7b543274"></span>
## **Adding visible watermarks**


1. Enable the **Add watermark** toggle.

2. The console will automatically add a watermark that fits a 1280x720 video source. You can add multiple watermarks and customize them for different video source sizes. There are two types of supported source sizes:

   * System presets: Supported source sizes include 16:9 (1280x720), 9:16 (720x1280), 4:3 (960x720), 3:4 (720x960), and 1:1 (720x720).

   * Custom settings: You can specify a custom width and height for the source size.

      * Width: Must be within the range of [360, 4096].

      * Height: Must be within the range of [360, 4096].

3. Select the type of watermark and configure its content based on your requirements.

   * For image watermarks, refer to the following table for the parameters:

      
      |**Parameter** |**Description** |
      |---|---|
      |Material file |Click the **Select material** button and choose a material file in the pop\-up window. |
      |Start time |The time at which the watermark will begin to display, measured in milliseconds. The default value is 0, indicating that the watermark will start displaying from the beginning of the video. |
      |End time |The time at which the watermark will stop displaying, measured in milliseconds. The default value is 0, indicating that the watermark will continue to display until the end of the video. |
      

   * For video watermarks, refer to the following table for the parameters:

      
      |**Parameter** |**Description** |
      |---|---|
      |Material file |Click **Select material** and choose a material file in the pop\-up window. |
      |Start time |The time at which the watermark will begin to display, measured in milliseconds. The default value is 0, indicating that the watermark will start displaying from the beginning of the video. |
      |End time |The time at which the watermark will stop displaying, measured in milliseconds. The default value is 0, indicating that the watermark will continue to display until the end of the video. |
      |Number of loops |The number of times the video watermark will be played. The available options are:<br><br><br>* 1: The video watermark is played once.<br><br>* \-1: The video watermark will loop indefinitely. However, the end time specified for the watermark will still determine when it stops playing.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the main video is longer than the video watermark, it is recommended to set the loop count to \-1. This ensures that the output video duration matches the main video content. Otherwise, there may be black frames after the main video content finishes.</div><br> |
      |Keep last frame |Specifies whether to display the last frame of the video watermark if its playback (including loops) finishes before the watermark's specified end time. If enabled, the last frame is displayed until this end time is reached. |
      

   * For text watermarks, refer to the following table for the parameters:

      
      |**Parameter** |**Description** |
      |---|---|
      |Watermark text |Enter the desired text for the watermark based on your business needs. |
      |Font |The font of the watermark text. |
      |Font size |The font size of the watermark text. The default value is 12. Must be within the range of [4, 120]. |
      |Color |The color of the watermark text. |
      |Start time |The time at which the watermark will begin to display, measured in milliseconds. The default value is 0, indicating that the watermark will start displaying from the beginning of the video. |
      |End time |The time at which the watermark will stop displaying, measured in milliseconds. The default value is 0, indicating that the watermark will continue to display until the end of the video. |
      

4. Set the position, offset, and size of the watermark.

   
   |**Parameter** |**Description** |
   |---|---|
   |Position |The initial placement of the watermark. The available options are:<br><br><br>* Top left<br><br>* Top right<br><br>* Center<br><br>* Bottom left<br><br>* Bottom right |
   |Horizontal offset (px) |The horizontal offset of the watermark in pixels, relative to the initial position. |
   |Vertical offset (px) |The vertical offset of the watermark in pixels, relative to the initial position. |
   |Watermark width (px) |The width of the watermark in pixels. |
   |Watermark height (px) |The height of the watermark in pixels. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The position, offset, and size of the watermark will be applied based on your video source size. Assuming your settings are as follows:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Adapted video source size: 1280x720   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Horizontal offset: 20   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Vertical offset: 20   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Watermark width: 100   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Watermark height: 100   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you input a video source of 720x540, the position, offset, and size of the watermark will be scaled proportionally based on the configured reference source size. Therefore, the watermark offset would be 20<em>720/1280 = 11.25, and the watermark width and height would be 100</em>720/1280 = 56.25.   </div>
   

5. Preview the video with the added watermark in the preview area on the right side.


<span id="59794809"></span>
## Inserting an in\-stream ad


1. Enable the **Insert in\-stream ad** toggle.

2. The console will automatically add an ad insertion template that is compatible with a 1280x720 video source. You can add multiple templates for different video source sizes.

3. Click the **Select material** button to choose a material in the pop\-up window for the pre\-roll or post\-roll. Currently, only MP4 format is supported.
