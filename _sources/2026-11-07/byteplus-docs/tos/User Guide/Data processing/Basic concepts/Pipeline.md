---
title: "Pipeline"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Pipeline"
---

Pipeline (|) is used to chain multiple data processing tasks without manually passing intermediate results. TOS will execute the data processing tasks in the order defined by the pipeline, thus enhancing data processing efficiency. This article introduces precautions, chaining rules, and examples of using pipelines.

<span id="28e01ec2"></span>
## Precautions

Pipelines (|) only support two types of operations: chaining image processing and image processing, chaining video frame capturing and image processing. For detailed information on image processing and video frame capturing, please refer to [Image Processing Overview](https://docs.byteplus.com/docs/tos/docs-overview_2) and [Video Frame Capture](https://docs.byteplus.com/docs/tos/docs-video-frame-capture).

<span id="352b8e81"></span>
## Chaining Rules

The delimiter for pipeline functions is a vertical line (|). You can use a vertical line (|) in the file URL to chain multiple data processing tasks, and TOS executes these tasks in the order from left to right as specified in the file URL. The specific chaining rules are as follows:


|**Types of Chained Tasks** |**Description** |
|---|---|
|Image Processing and Image Processing |When chaining multiple image processing operations using the pipe symbol, the second and subsequent image processing operations can either include the `image/` parameter or omit the `image/` parameter.<br><br>The file URL format is either `x-tos-process=image/<image processing parameter>\|<image processing parameter>\|<image processing parameter>` or `x-tos-process=image/<image processing parameter>\|image/<image processing parameter>\|image/<image processing parameter>`. |
|Video Frame Capture and Image Processing |When using the pipe symbol to chain video frame extraction and image processing, the file URL must adhere to the following rules:<br><br><br>* The first data processing operation must be video frame extraction.<br><br>* The second data processing operation must be image processing, and it must include the `image/` parameter.<br><br>* The third and subsequent data processing operations must be image processing and may either include the `image/` parameter or not include the `image/` parameter.<br><br><br>The file URL format can be `x-tos-process=video/<video frame extraction parameters>\|image/<image processing parameters>\|<image processing parameters>` or `x-tos-process=video/<video frame extraction parameters>\|image/<image processing parameters>\|image/<image processing parameters>`. |


<span id="a3cc353e"></span>
## Use Cases


* Example 1: Chaining Image Scaling and Image Watermarking

   * Resize the Image

      Specify the image to be scaled to a width of 200, a height of 200, and set the mode to fixed.

      [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200,h_200,m_fixed](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200,h_200,m_fixed)

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf25b5602d464ed0807acfa3d1f341b1~tplv-goo7wpa0wc-image.image) </span>

   * Chaining Image Scaling and Image Watermarking

      Set the image to scale to a width of 200, a height of 200, and mode to fixed, then add a text watermark "Hello" on the image, setting the font size to 72, color to red, and font to Fangzheng Book Song.

      [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200,h_200,m_fixed|watermark,text_SGVsbG8,size_72,color_FF0000,type_ZmFuZ3poZW5nc2h1c29uZw](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200,h_200,m_fixed%7Cwatermark,text_SGVsbG8,size_72,color_FF0000,type_ZmFuZ3poZW5nc2h1c29uZw)

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a2c355800e7468885e44b9f9e4a28ba~tplv-goo7wpa0wc-image.image) </span>

* Example 2: Chaining Video Frame Capture and Image Rotation

   * Capture Image from Video Frame

      Capturing the frame at 26000ms using the default mode, scaling the width to 400 px, the height to 200 px, and the image output format to jpg.

      [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/misc_video.mp4?x-tos-process=video/snapshot,t_26000,w_400,h_200,f_jpg](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/misc_video.mp4?x-tos-process=video/snapshot,t_26000,w_400,h_200,f_jpg)

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/32c30a5c00b94814987498364dd9a871~tplv-goo7wpa0wc-image.image) </span>

   * Chaining Video Frame Capture and Image Rotation

      Capture the frame at 26000ms using the default mode, resize to 400 px width and 200 px height, output the image in jpg format, then rotate the image clockwise by 90 degrees.

      [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/misc_video.mp4?x-tos-process=video/snapshot,t_26000,w_400,h_200,f_jpg|image/rotate,90](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/misc_video.mp4?x-tos-process=video/snapshot,t_26000,w_400,h_200,f_jpg%7Cimage/rotate,90)

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9aed5dbba02a4e7db73242cb86150acc~tplv-goo7wpa0wc-image.image) </span>
