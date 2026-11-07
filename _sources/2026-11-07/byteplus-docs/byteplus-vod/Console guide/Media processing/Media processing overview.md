---
title: "Media processing overview"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-processing"
---

To enhance your audio and video files, simply process them in the BytePlus VOD console. You can use the pre\-built media processing and workflow templates available on the console or create customized ones tailored to your specific business requirements.

<span id="0f9a9591"></span>
## Media processing templates

A media processing template includes the specific configurations you want the BytePlus VOD transcoding service to implement, such as the preferred codec and resolution for your processed file. Within the BytePlus VOD console, you have the option to choose from various types of media processing templates. You can either select one of the pre\-built templates or create a custom template that meets your unique business needs.


|**Media processing template type** |**Description** |
|---|---|
|[Video transcoding template](https://docs.byteplus.com/en/docs/byteplus-vod/docs-video-transcoding-template) |This template configures video parameters such as the encoding format, encapsulation format, resolution, and bitrate, to suit different business scenarios, devices, and network environments. |
|[Low-bitrate HD template](https://docs.byteplus.com/en/docs/byteplus-vod/docs-high-definition-and-low-bitrate-template) |This template uses video processing enhancement and adaptive transcoding algorithms to deliver high\-quality images at a lower bitrate. |
|[Audio transcoding template](https://docs.byteplus.com/en/docs/byteplus-vod/docs-audio-transcoding-template) |This template configures audio parameters such as the encoding format, sampling rate, and bitrate, to suit different business scenarios, devices, and network environments. |
|[Video enhancement template](https://docs.byteplus.com/en/docs/byteplus-vod/docs-image-enhancement-template) |This template uses advanced AI algorithms to restore or enhance the quality of videos. |
|[Snapshot template](https://docs.byteplus.com/en/docs/byteplus-vod/docs-snapshot-template) |This template generates different types of screenshots, including static pictures, GIFs, and sprites. |
|[Watermark and ad insertion template](https://docs.byteplus.com/en/docs/byteplus-vod/docs-watermark-and-ad-insertion-template) |This template adds watermarks and in\-stream ads. You can add multiple watermarks for different video sizes, and configure the start and end time, position, offset, and size of the watermarks. |
|[Smart subtitling template](https://docs.byteplus.com/en/docs/byteplus-vod/docs-smart-subtitle-template) |This template generates subtitle sets for audio within media files. |


<span id="c55f5643"></span>
## Trigger single template processing

You can use the BytePlus VOD console to trigger a media processing task by specifying a single media processing template. This method is suitable for single video processing scenarios, offering a simple workflow and a good user experience. The steps are as follows:


1. Log in to the [BytePlus VOD console](https://console.byteplus.com/auth/login) and go to the specified space.

2. On the **Videos** page, under the **Vid mode** and **Uploaded** tab, select the video files you want to process, and click **Start processing**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also click the <strong>DirectUrl mode</strong> tab to initiate media processing in DirectUrl mode. There is no difference in the media processing service itself between Vid mode and DirectUrl mode; the key differences lie in how processing is triggered and how the outputs are stored:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Vid mode: Locates the media assets to be processed using Vid. After processing is complete, the output is automatically uploaded to the VOD space and shares the same Vid as the input video.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">DirectUrl mode: Locates the media assets to be processed using the space name and FileName. You can customize the file path rules for media processing outputs. After processing is complete, the output is stored in the specified location according to the designated file path.   </div>
   

3. In the **Process** drawer, configure the information as prompted on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e94a03e731c647f38d0e8b824adf5344~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Description** |
   |---|---|
   |Processing type |Supports the following options:<br><br><br>* Video transcoding: Trigger transcoding tasks using a single video transcoding template. See [Video transcoding template](https://docs.byteplus.com/docs/byteplus-vod/docs-video-transcoding-template) for details.<br><br>* Low\-bitrate HD: Trigger transcoding tasks using a single low\-bitrate HD template. See [Low-bitrate HD template](https://docs.byteplus.com/docs/byteplus-vod/docs-high-definition-and-low-bitrate-template) for details.<br><br>* Audio transcoding: Trigger transcoding tasks using a single audio transcoding template. See [Audio transcoding template](https://docs.byteplus.com/docs/byteplus-vod/docs-audio-transcoding-template) for details.<br><br>* Video enhancement: Trigger transcoding tasks using a single video enhancement template. See [Video enhancement template](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement-template) for details.<br><br>* Workflow: Trigger media processing tasks using workflow. See [Workflows](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow) for details. |
   |Processing template |Select a processing template based on the chosen processing type. |
   |Watermark template |If the processing type is **video transcoding** or **low\-bitrate HD**, you can also select a watermark template to add a watermark during transcoding. See [Watermark and ad insertion template](https://docs.byteplus.com/docs/byteplus-vod/docs-watermark-and-ad-insertion-template) for details. |
   

4. Click **Start processing**. When the task is successfully triggered, you can click the **Tasks** button in the prompt message to go to the **Tasks** page, where you can view the details and results.
