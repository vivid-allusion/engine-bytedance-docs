---
title: "Rotation"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-rotation"
---

This section describes how to rotate the original image clockwise. The following table lists the parameters and examples.

<span id="496fd85a"></span>
## Parameters


|**Parameter** |**Description** |**Setting** |**Required** |
|---|---|---|---|
|value |Degree of the clockwise rotation of the image. |The image will be rotated clockwise. |Yes |


<span id="074479b1"></span>
## Note


* If the degree is not 90, 180, 270, or 360, the processed image will be larger in size.

* The image width or height can be up to 4,096 pixels.


<span id="5c343975"></span>
## Examples


* Set the image width to 200 and clockwise rotation degree to 90.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200/rotate,90](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200/rotate,90)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab437f45bfce4e4a9ff61d106be371f4~tplv-goo7wpa0wc-image.image) </span>

* Set the image width to 200 and clockwise rotation degree to 245.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200/rotate,245](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200/rotate,245)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30fb0328004c47d991af079424e3045d~tplv-goo7wpa0wc-image.image) </span>
