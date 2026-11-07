---
title: "Contrast"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-contrast"
---

This section describes how to adjust the contrast of the original image. The following table lists the parameters and examples.

<span id="976f542f"></span>
## Parameters


|**Parameter** |**Description** |**Setting** |**Required** |
|---|---|---|---|
|value |Image contrast. |[\-100,100]<br><br><br>* A negative value decreases the contrast.<br><br>* The value 0 indicates no contrast adjustment.<br><br>* A positive value increases the contrast. |Yes |


<span id="1c933142"></span>
## Examples


* Set the image width to 200 and contrast to \-50.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200/contrast,-50](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200/contrast,-50)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e4fafcf797646068597053ef8e91477~tplv-goo7wpa0wc-image.image) </span>

* Set the image width to 200 and contrast to 50.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200/contrast,50](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200/contrast,50)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9fcd4c5b9e424911bfa604652087662a~tplv-goo7wpa0wc-image.image) </span>
