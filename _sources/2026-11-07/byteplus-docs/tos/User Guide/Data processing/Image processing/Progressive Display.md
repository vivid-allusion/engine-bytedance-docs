---
title: "Progressive Display"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-progressive-display"
---

This section describes how to make the original image progressive. The following table lists the parameters and examples.

<span id="5956296a"></span>
## Parameters


|**Parameter** |**Description** |**Setting** |**Required** |
|---|---|---|---|
|value |Specifies whether to use progressive display. |* 1: yes<br><br>* 0: no (standard display is used) |Yes |


<span id="99fd3ec6"></span>
## Note


* If the image format is not JPG, convert it to JPG first.

* Progressive display is valid only for JPG images.


<span id="b8aa6a6e"></span>
## Examples

Set progressive display for an image.

[https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/format,jpg/interlace,1](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/format,jpg/interlace,1)

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eea559d3e3824a07a74a94269ac273b9~tplv-goo7wpa0wc-image.image) </span>
