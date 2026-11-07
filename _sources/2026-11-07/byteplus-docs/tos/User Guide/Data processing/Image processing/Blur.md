---
title: "Blur"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-blur"
---

This section describes how to blur the original image. The following table lists the parameters and examples.

<span id="88304798"></span>
## Parameters


|**Parameter** |**Description** |**Setting** |**Required** |
|---|---|---|---|
|r |Blur radius. |[1,50]<br><br>The larger the value, the blurrier the image. |Yes |
|s |Standard deviation of a normal distribution. |[1,50]<br><br>The larger the value, the blurrier the image. |Yes |


<span id="c4921633"></span>
## Note

A dynamic image will become static after blur.

<span id="4abdcf81"></span>
## Examples

Set r to 3 and s to 2.

[https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/blur,r_3,s_2](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/blur,r_3,s_2)

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/020ed8296cf0429997f3146c62655315~tplv-goo7wpa0wc-image.image) </span>
