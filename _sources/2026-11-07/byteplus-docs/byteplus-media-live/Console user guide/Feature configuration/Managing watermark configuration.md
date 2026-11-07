---
title: "Managing watermark configuration"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-live-stream-watermarks"
---

To protect your content from unauthorized use, you can add a static or dynamic watermark to your transcoded streams or adaptive bitrate (ABR) substreams using MediaLive. This topic describes how to configure watermarks in the MediaLive console.

 &nbsp;

<span id="notes"></span>
## Notes


* Watermarks are supported only for transcoded streams or ABR substreams. Before adding a watermark configuration, make sure that the target `AppName` already has a transcoding or ABR configuration in the same domain name space. To watermark the source stream, add a transcoding configuration that uses the **Original** settings.

* Only one watermark configuration is supported for each `AppName`. Within that configuration, you can apply the watermark to all or specific transcoded streams or ABR substreams.

* After you add, update, or delete a watermark configuration, the change takes effect in 3 to 5 minutes. Transcoded streams or ABR substreams generated after the change takes effect use the latest watermark configuration. Existing transcoded streams or ABR substreams generated before the change takes effect do not automatically apply the update. If no transcoded stream or ABR substream exists before the change, wait for the configuration to take effect. If a transcoded stream or ABR substream already exists before the change and you need to use the updated configuration, wait 3 to 5 minutes after the configuration is added, updated, or deleted, and then push the stream again.

* The actual placement of a static watermark is determined by the watermark's absolute position and size. If the watermark extends beyond the edges of the video, it will not appear on the video at all.


 &nbsp;

<span id="prerequisites"></span>
## Prerequisites


* Add a transcoding or ABR configuration for the target `AppName` in the domain name space where you want to add the watermark configuration. For more information, see [Managing transcoding configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding) or [Managing adaptive bitrate configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-an-hls-abr-task).

* A JPG or PNG image with a maximum file size of 2 MB and a maximum resolution of 1080 x 1080 px. PNG images can include transparency.


 &nbsp;

<span id="procedure"></span>
## Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, select **Settings** \> **Feature configuration**. Click the **Watermark** tab.

3. Select the domain name space where the transcoding or ABR configuration is added from the **Domain name space** drop\-down list.

4. Click **Add configuration** to open the **Add watermark configuration** dialog box.

5. Configure the relevant settings and then click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22f25b46529040bdb0caaa57c8aebdb8~tplv-goo7wpa0wc-topic.webp) </span>

&nbsp;

   
   |**Parameter** |**Description** |
   |---|---|
   |AppName |Select the same `AppName` as that of the transcoding or ABR configuration. |
   |StreamName |The `StreamName` in the push stream address. For example, if the push stream address is `rtmp://push.example.com/live/test?authinfo`, then `StreamName` is `test`.<br><br><br>* If you configure `StreamName`, the watermark applies only to the specific transcoded stream or ABR substream under the current `AppName`.<br><br>* If you leave `StreamName` empty or enter `*`, the watermark applies to all transcoded streams or ABR substreams under the current `AppName`. |
   |Suffix |By default, all suffixes are selected, meaning the watermark applies to all transcoded streams or ABR substreams.<br><br>You can also select one or more suffixes (such as `_uhd` and `_hd`) to add the watermark only to transcoded streams or ABR substreams with those suffixes. |
   |Add watermark |Upload a JPG or PNG image. Maximum file size: 2 MB. Maximum resolution: 1080 x 1080 px.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">PNG images can include transparency.</div><br> |
   |Watermark type |Select the watermark type.<br><br><br>* **Static watermark**: Keeps the watermark fixed at the configured position.<br><br>* **Dynamic watermark**: Moves the watermark during playback to make unauthorized screen recordings and reuse more difficult. |
   |Horizontal offset |For details, see [FAQs](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-live-stream-watermarks#FAQs).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">This field appears only when you select <strong>Static watermark</strong> as the <strong>Watermark type</strong>.</div><br> |
   |Vertical offset |For details, see [FAQs](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-live-stream-watermarks#FAQs).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">This field appears only when you select <strong>Static watermark</strong> as the <strong>Watermark type</strong>.</div><br> |
   |Dynamic Effects |Select how the watermark changes during playback.<br><br><br>* **Dynamic curve movement**: The watermark moves continuously and changes direction when it reaches the video edges.<br><br>* **Dynamic blinking**: The watermark appears at a new random position in the video at intervals.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">This field appears only when you select <strong>Dynamic watermark</strong> as the <strong>Watermark type</strong>.</div><br> |
   |Dynamic speed |A lower value creates slower movement, and a higher value creates faster movement. Valid range: 1\-10.<br><br><br>* For **Dynamic curve movement**, this controls how fast the watermark moves.<br><br>* For **Dynamic blinking**, this controls how often the watermark changes position.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">This field appears only when you select <strong>Dynamic watermark</strong> as the <strong>Watermark type</strong>.</div><br> |
   |Watermark scale |This adjusts the uniform scaling of the watermark. Valid range: 1%\-200%. |
   |Preview |The preview shows your watermark effect in either **Landscape** or **Portrait** mode.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">Watermarks are previewed on a 1920 x 1080 screen. During live\-stream sessions, the actual watermark effect may appear slightly different.</div><br> |
   

   After adding the watermark configuration, you can see the configuration on the list. You can click **Edit** or **Delete** in the **Action** column to edit or delete the watermark configuration.


 &nbsp;

<span id="what-to-do-next"></span>
## What to do next


1. Use the [address generator](https://console.byteplus.com/live/main/locationGenerate) to generate the push stream address, transcoded stream address, or ABR address. For more information, see [Generating stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator).

   * The domain names for stream pushing and pulling must belong to the domain name space where you add the watermark configuration.

   * Use the same `AppName` and `StreamName` to generate the push stream address, transcoded stream address, or ABR address.

2. Get the transcoded stream address or ABR address.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you select specific suffixes in the watermark configuration, select the corresponding suffix when getting the address.   </div>
   

3. Use your push stream address to push the source stream.

4. Use any of the following methods to pull the transcoded stream or ABR substream.

&nbsp;

   
   |Method |Scenario |Description |
   |---|---|---|
   |Third\-party stream pulling tool |No SDK development resources. |Configure the transcoded stream address or ABR address in the third\-party stream pulling tool to play the transcoded stream or ABR substream. For more information, refer to the corresponding official documentation or consult official customer support. |
   |Player SDK for Web |Watch the live stream in a web browser. |Integrate the Player SDK for Web and play the transcoded stream or ABR substream on your website or web app. For more information, see [Feature integration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-web-feature-integration). |
   |Client SDK |Watch the live stream in your own mobile app. |Integrate the client SDK and play the transcoded stream or ABR substream in a mobile app. For more information, see:<br><br><br>* iOS: [Player SDK for iOS: Advanced features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3)<br><br>* Android: [Player SDK for Android: Advanced features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2)<br><br>* Flutter: [Integrating the Player SDK for Flutter](https://docs.byteplus.com/docs/byteplus-media-live/integrating-the-player-sdk-for-flutter)<br><br>* React Native: [Player SDK for React Native: Advanced features](https://docs.byteplus.com/docs/byteplus-media-live/docs-rnplayer-advanced-features) |
   |BytePlus MediaLive console |For quick preview and debugging during development or testing. |On the [Web pull page](https://console.byteplus.com/live/main/webPullStream/play) in the console, enter the transcoded stream address or ABR address to quickly verify playback. For more information, see [Pulling a stream through the console](https://docs.byteplus.com/docs/byteplus-media-live/docs-web-pull).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">This page supports only FLV, HLS, and RTM streams.</div><br> |
   


 &nbsp;

<span id="faq"></span>
## FAQ

 &nbsp;

<span id="what-are-horizontal-and-vertical-offsets?"></span>
### What are horizontal and vertical offsets?

BytePlus MediaLive uses **Horizontal offset** (PosX) and **Vertical offset** (PosY) to specify the position of a static watermark on the video. Relevant parameters are described as follows:

&nbsp;


|**Parameter** |**Description** |
|---|---|
|PosX |**Horizontal offset**, which is the ratio of the distance between the left edge of the watermark and the left edge of the transcoded video to the width of the video. Valid range: 0–1. |
|PosY |**Vertical offset**, which is the ratio of the distance between the top edge of the watermark and the top edge of the transcoded video to the height of the video. Valid range: 0–1. |
|RelativeWidth |The ratio of the width of the watermark to that of the transcoded video. Valid range: 0–1. The height of the watermark is automatically adjusted to its width. |
|Orientation |Two options are available.<br><br><br>* horizontal: Landscape.<br><br>* vertical: Portrait. |


PosX and PosY apply only to static watermarks. The BytePlus MediaLive console uses **Watermark scale** to resize watermarks, whereas our API uses **Relative width** as a size parameter. In this section, we only introduce **Relative width**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee5e570a6c804de6a11c51be467367b9~tplv-goo7wpa0wc-topic.webp) </span>

 &nbsp;

<span id="how-can-i-calculate-the-absolute-position,-width,-and-height-of-the-watermark?"></span>
### How can I calculate the absolute position, width, and height of the watermark?

Suppose you add a 400 x 200 image as a static watermark over a 1920 x 1080 video in landscape mode and set the following parameters:

```plain
PosX = 0.05
PosY = 0.05
RelativeWidth = 0.1
Orientation = "horizontal"
```


Below is how you calculate the absolute position, width, and height of the watermark:

```plain
abs_x = 1920 * 0.05 = 96  // The left edge of the watermark is 96 pixels away from the left edge of the video.
abs_y = 1080 * 0.05 = 54  // The top edge of the watermark is 54 pixels away from the top edge of the video.
abs_w = 1920 * 0.1 = 192  // The width of the watermark is 192 pixels.
abs_h = 192 * 200 / 400 = 96  // The height of the watermark is 96 pixels.
```


The actual placement of a static watermark is determined by its absolute position and size. If the watermark extends beyond the edges of the video, it will not appear on the video at all. Adjust the watermark’s **Horizontal offset**, **Vertical offset**, or **Relative width** to keep the full watermark visible within the video.

 &nbsp;

<span id="why-is-my-watermark-not-showing-during-live-stream-sessions?"></span>
### Why is my watermark not showing during live\-stream sessions?

There are several possible reasons:


* **The watermark configuration change has not taken effect yet.** 

   After adding, updating, or deleting a watermark configuration, wait 3 to 5 minutes for the change to take effect.

* **The transcoded stream or ABR substream was generated before the watermark configuration change took effect.** 

   Existing transcoded streams or ABR substreams do not automatically apply the update. To use the latest watermark configuration, wait 3 to 5 minutes after the configuration is added, updated, or deleted, and then push the stream again.

* **You have not added any transcoding or ABR configuration for the related AppName.** 

   Watermarks can only be applied to an `AppName` that already has a transcoding or ABR configuration. Make sure you have added a transcoding or ABR configuration for the related `AppName`.

* **The suffix of the current transcoded stream or ABR substream is not one of the selected suffixes.** 

   If you select specific transcoding suffixes or ABR substream suffixes in the watermark configuration, the watermark appears only in the transcoded streams or ABR substreams whose suffixes match the selected suffixes.

* **The watermark extends beyond the edges of the video.** 

   This applies to a static watermark. The actual placement is determined by the watermark's absolute position and size. If the watermark extends beyond the edges of the video, it will not appear on the video at all. Adjust the watermark’s **Horizontal offset**, **Vertical offset**, or **Relative width** to keep the full watermark visible within the video.
