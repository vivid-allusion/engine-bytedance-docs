---
title: "Image Processing Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-overview_2"
---

You can send a GetObject request carrying an image processing parameter to process images stored in TOS. Image processing operations include resizing, cropping, watermarking, and format conversion.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Using the image processing service incurs image processing, request, and traffic fees. For more information on billing, see <a href="https://docs.byteplus.com/en/tos/docs/data-processing-fee?version=1.0.0">Data processing fee</a>, <a href="https://docs.byteplus.com/en/tos/docs/request-fee?version=1.0.0">Request fee</a>, and <a href="https://docs.byteplus.com/en/tos/docs/traffic-fee?version=1.0.0">Traffic fee</a>.</div>


* <div data-tips="true" data-tips-type="tip">When using image processing functions on images of Infrequent Access Storage and Flashback Archive types, data retrieval fees will be incurred, charged based on the size of the image before processing. For billing details, please refer to <a href="https://docs.byteplus.com/docs/tos/docs-data-retrieval-fee">Data Retrieval Fee</a>.</div>



<span id="db79e63a"></span>
## Restrictions


* The original image can be only in the jpg/jpeg, png, bmp, gif, webp and tiff format.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">There are special cases regarding the original image formats supported by some image processing operations, and these will be additionally explained in the corresponding individual documents.   </div>
   

* The original image can be up to 20 MB.

* The width and height of the original image cannot exceed 30,000 pixels, and the original image size cannot exceed 250 million pixels. The width and height cannot exceed 4,096 pixels for rotation.

* TOS will not process WebP images that exceed 16,383 pixels in width or height. Any image processing features applied to such images will leave them unchanged.

* The width and height of the resized image cannot exceed 16,384 pixels, and the original image size cannot exceed 16,777,216 pixels.


<span id="ba7fc644"></span>
## Image processing methods

You can process images in TOS buckets through RESTful APIs or file URLs. Specifically, you can simply resize, crop, or watermark the images and quickly get the processed images anytime.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Processed images will be returned immediately and will not be saved to your bucket.</div>



* Using RESTful APIs:

   A sample request is as follows:

   ```JSON
   GET /example.jpg?x-tos-process=image/resize,w_300 HTTP/1.1
   Host: endpoint
   X-Tos-Content-Sha256: sha256
   X-Tos-Date: 20220827T132948Z
   Authorization: authorization
   json
   ```
   

* Using file URLs:

   A sample URL is as follows:

   ```JSON
   http://bucket.endpoint/example.jpg?x-tos-process=image/resize,w_300
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To process private images, you need to use the SDK to generate a presigned URL carrying an image processing parameter.   </div>
   

<span id="582914d9"></span>
## Image processing features

The following table lists image processing features supported by TOS. Each feature corresponds to a parameter. If you specify multiple parameters in a request, TOS will process the image in the order of the parameters.


|**Image Processing Feature** |**Parameter** |**Description** |
|---|---|---|
|[Image resizing](https://docs.byteplus.com/en/tos/docs/image-resizing?version=1.0.0) |resize |Resizes an image as specified. |
|[Watermarking](https://docs.byteplus.com/en/tos/docs/watermarking?version=1.0.0) |watermark |Adds an image watermark or a text watermark to an image. |
|[Custom cropping](https://docs.byteplus.com/en/tos/docs/custom-cropping?version=1.0.0) |crop |Crops an image into a rectangle of a specified size. |
|[Incircle](https://docs.byteplus.com/en/tos/docs/incircle?version=1.0.0) |circle |Crops an image into a circle of a specified radius based on the center point of the image. |
|[Indexed slicing](https://docs.byteplus.com/en/tos/docs/indexed-slicing?version=1.0.0) |indexcrop |Crops an image along the x\-axis or y\-axis into multiple images and selects one. |
|[Rounded rectangle](https://docs.byteplus.com/en/tos/docs/rounded-rectangle?version=1.0.0) |rounded\-corners |Crops an image into a rounded rectangle of a specified size. |
|[Quality change](https://docs.byteplus.com/en/tos/docs/quality-change?version=1.0.0) |quality |Adjusts the quality of a JPG or WEBP image. |
|[Format conversion](https://docs.byteplus.com/en/tos/docs/format-conversion?version=1.0.0) |format |Converts the image format. |
|[Information query](https://docs.byteplus.com/en/tos/docs/information-query?version=1.0.0) |info |Gets image information, including basic information and EXIF information. |
|[Average hue query](https://docs.byteplus.com/en/tos/docs/average-hue-query?version=1.0.0) |average\-hue |Gets the average hue of an image. |
|[Auto-orient](https://docs.byteplus.com/en/tos/docs/auto-orient?version=1.0.0) |auto\-orient |Automatically rotates an image. |
|[Blur](https://docs.byteplus.com/en/tos/docs/blur?version=1.0.0) |blur |Blurs an image. |
|[Rotation](https://docs.byteplus.com/en/tos/docs/rotation?version=1.0.0) |rotate |Rotates an image clockwise with specified degrees. |
|[Progressive display](https://docs.byteplus.com/en/tos/docs/progressive-display?version=1.0.0) |interlace |Configures JPG images as progressive. |
|[Image brightness](https://docs.byteplus.com/en/tos/docs/image-brightness?version=1.0.0) |bright |Adjusts the image brightness. |
|[Sharpening](https://docs.byteplus.com/en/tos/docs/sharpening?version=1.0.0) |sharpen |Sharpens an image. |
|[Contrast](https://docs.byteplus.com/en/tos/docs/contrast?version=1.0.0) |contrast |Adjusts the image contrast. |
|[Advanced compression](https://docs.byteplus.com/en/tos/docs/advanced-compression?version=1.0.0) |heic |convert the image format to High Efficiency Image Format (HEIF). |
|[Image storage](https://docs.byteplus.com/en/tos/docs/image-storage?version=1.0.0) |save |Stores a processed image in a specified bucket. |
