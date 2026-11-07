---
title: "Image Brightness"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-image-brightness"
---

This section describes how to adjust the brightness of the original image. The following table lists the parameters and examples.

<span id="8c4449d2"></span>
## Parameters


|**Parameter** |**Description** |**Setting** |**Required** |
|---|---|---|---|
|value |Image brightness. |[\-100,100]<br><br><br>* A negative value decreases brightness.<br><br>* The value 0 indicates no brightness adjustment.<br><br>* A positive value increases brightness. |Yes |


<span id="81a04d6d"></span>
## Examples


* Set the image width to 200 and brightness to \-50.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200/bright,-50](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200/bright,-50)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca2ea6d2d3ad4958ba74d14bdc970c33~tplv-goo7wpa0wc-image.image) </span>

* Set the image width to 200 and brightness to 50.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200/bright,50](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200/bright,50)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6eb477e6f7c04169bdcb0d17f25c8192~tplv-goo7wpa0wc-image.image) </span>
