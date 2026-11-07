---
title: "Incircle"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-incircle"
---

This section describes how to crop a circle of a specified radius inside the original image, with the center point of the image as the center. The following table lists the parameters and examples.

<span id="8488bf01"></span>
## Parameters


|**Parameter** |**Description** |**Setting** |**Required** |
|---|---|---|---|
|r |Radius of the incircle. |[1,4096] |Yes |


<span id="2d548c7c"></span>
## Note


* If the output format of an image does not support an alpha channel, for example, JPG, fill the area outside the circle with the white color.

* If the input format of an image supports an alpha channel, for example, PNG, WEBP, BMP, or another vector image format, make the area outside the circle transparent. PNG is recommended.

* When the radius exceeds half of the shortest side of the original image, use the shortest side of the original image as the radius of the incircle.


<span id="c443158c"></span>
## Examples


* Set the radius to 200 and output format to JPG and fill the area outside the circle with the white color.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/circle,r_200/format,jpg](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/circle,r_200/format,jpg)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9c266b48c394d99bbf6fe9067a173d8~tplv-goo7wpa0wc-image.image) </span>

* Set the radius to 200 and output format to PNG and fill the area outside the circle with the transparent color.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/circle,r_200/format,png](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/circle,r_200/format,png)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48386dcc51e5408fb82f6c1d21f03393~tplv-goo7wpa0wc-image.image) </span>
