---
title: "Rounded Rectangle"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-rounded-rectangle"
---

This section describes how to crop a rounded rectangle of a specified size. The following table lists the parameters and examples.

<span id="7d9bcaa7"></span>
## Parameters


|**Parameter** |**Description** |**Setting** |**Required** |
|---|---|---|---|
|r |Radius of the rounded corner. |[1,4096] |Yes |


<span id="44dd8dc6"></span>
## Note


* If the output format of an image does not support an alpha channel, for example, JPG, fill the area outside the circle with the white color.

* If the input format of an image supports an alpha channel, for example, PNG, WEBP, BMP, or another vector image format, make the area outside the circle transparent. PNG is recommended.

* When the radius of the rounded corner exceeds half of the shortest side of the original image, set the radius of the rounded corner to the radius of the largest incircle of the image.


<span id="546de103"></span>
## Examples


* Set the radius to 100 and output format to JPG and fill the area outside the circle with the white color.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/rounded-corners,r_100/format,jpg](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/rounded-corners,r_100/format,jpg)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1eb345ddaa014914ae6220c49fca1e83~tplv-goo7wpa0wc-image.image) </span>

* Set the radius to 100 and output format to PNG and fill the area outside the circle with the transparent color.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/rounded-corners,r_100/format,png](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/rounded-corners,r_100/format,png)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8eaa27c4a38f4288ae6d9a81c345228e~tplv-goo7wpa0wc-image.image) </span>
