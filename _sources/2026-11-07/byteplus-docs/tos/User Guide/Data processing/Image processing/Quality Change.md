---
title: "Quality Change"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-quality-change"
---

This section describes how to compress the original image to adjust the quality. The following table lists the parameters and examples.

<span id="3f857976"></span>
## Parameters


|**Parameter** |**Description** |**Setting** |**Required** |
|---|---|---|---|
|q |Relative quality. After this parameter is set, the original image is compressed to q%. |[1,100] |Yes |
|Q |Absolute quality. After this parameter is set, the original image is compressed to Q%. The quality of the compressed image does not depend on that of the original image. |[1,100] |Yes |


<span id="daf361b2"></span>
## Note


* The `q` parameter is only valid for original images in the pjpeg, jpg/jpeg formats.

* The `Q` parameter is only valid for original images in the formats of webp, pjpeg, jpg/jpeg, jpeg\-2000, avif, and heic.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When using the <code>q</code> parameter or the <code>Q</code> parameter to perform quality transformation on images in png, tiff, bmp, gif, and psd formats, the system will not report an error. However, in fact, the operation does not take effect, and the image quality does not change at all.   </div>
   

* If both q and Q are specified, Q prevails.


<span id="780416fb"></span>
## Examples

Original image:[https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample2.jpg](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample2.jpg)


* Set q to 60 and output format to JPG.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample2.jpg?x-tos-process=image/quality,q_60](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample2.jpg?x-tos-process=image/quality,q_60)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57135c71b47246c8aba12e959a25047f~tplv-goo7wpa0wc-image.image) </span>

* Set Q to 60 and output format to JPG.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample2.jpg?x-tos-process=image/quality,Q_60](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample2.jpg?x-tos-process=image/quality,Q_60)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec46dfb56f4a4b229b646e538dd31f50~tplv-goo7wpa0wc-image.image) </span>
