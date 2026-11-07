---
title: "Video Frame Capture"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-video-frame-capture"
---

The video frame capture feature allows you to capture a frame at a specified point in time from a video and resize it to a specified size. This topic describes the parameters and provides guidance on using the video frame capture feature.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The use of the video frame capture feature incurs fees for video frame capture, requests, and data traffic. For more information on billing, see <a href="https://docs.byteplus.com/en/tos/docs/data-processing-fee?version=1.0.0">Data processing fee</a>, <a href="https://docs.byteplus.com/en/tos/docs/request-fee?version=1.0.0">Request fee</a>, and <a href="https://docs.byteplus.com/en/tos/docs/traffic-fee?version=1.0.0">Traffic fee</a>.</div>


* <div data-tips="true" data-tips-type="tip">When using the video frame capture feature on files of Infrequent Access Storage and Flashback Archive types, there will be data retrieval charges based on the size of the content returned after video frame capture. For billing details, please refer to <a href="https://docs.byteplus.com/docs/tos/docs-data-retrieval-fee">Data Retrieval Fee</a>.</div>



<span id="9af79eda"></span>
## **Note**


* For supported video formats, see the Constraints and limitations section in [Overview](https://www.volcengine.com/docs/6349/336154).

* TOS does not store a captured frame by default. You can store a captured frame in either of the following ways:

   * Download and store it to your computer.

   * Use the image storage feature to store it to a bucket. For more information, see [Image storage](https://docs.byteplus.com/en/tos/docs/image-storage?version=1.0.0).


<span id="cc54f262"></span>
## **Parameters**


|**Parameter** |**Description** |**Valid value** |**Required** |
|---|---|---|---|
|t |Sets the point in time to capture a frame. |[0, video duration]<br><br>Unit: ms |Yes |
|w |Sets the width for frame capture. If you set it to 0, the width is automatically calculated based on the resolution of the original video. |[0, video width]<br><br>Unit: px |No |
|h |Sets the height for frame capture. If you set it to 0, the height is automatically calculated based on the resolution of the original video.<br><br>> If both w and h are 0, the captured frame will retain the same width and height as the original video. |[0, video height]<br><br>Unit: px |No |
|m |Sets the frame capture mode. |* Default: If you do not set the frame capture mode, a frame is captured exactly at the specified point in time.<br><br>* fast: Captures the most recent key frame before the specified point in time. |No |
|f |Sets the format of the captured frame. |* jpg (default)<br><br>* png |No |
|ar |Specifies whether to automatically rotate the captured frame based on video information. |* auto: Rotates the captured frame based on video information.<br><br>* w: Rotates the captured frame in a mode where the width exceeds the height.<br><br>* h: Rotates the captured frame in a mode where the height exceeds the width. |No |


<span id="7301f7d9"></span>
## **Examples**

Original video: https://tos\-tools.tos\-ap\-southeast\-1.bytepluses.com/misc/misc_video.mp4


* Capture the frame at 26,000 ms in default mode, setting the width to 400, height to 200, and format as jpg. Sample URL:

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/misc_video.mp4?x-tos-process=video/snapshot,t_26000,w_400,h_200,f_jpg](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/misc_video.mp4?x-tos-process=video/snapshot,t_26000,w_400,h_200,f_jpg)

   The following image is expected to be returned:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0169b8e8d88c44eeb3f608379ea3e2ea~tplv-goo7wpa0wc-image.image) </span>

* Capture the frame at 26,000 ms in fast mode, setting the width to 400, height to 200, and format as jpg. Sample URL:

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/misc_video.mp4?x-tos-process=video/snapshot,t_26000,w_400,h_200,f_jpg,m_fast](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/misc_video.mp4?x-tos-process=video/snapshot,t_26000,w_400,h_200,f_jpg,m_fast)

   The following image is expected to be returned:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ad0e78855fd4c879871c01195ea5a27~tplv-goo7wpa0wc-image.image) </span>
