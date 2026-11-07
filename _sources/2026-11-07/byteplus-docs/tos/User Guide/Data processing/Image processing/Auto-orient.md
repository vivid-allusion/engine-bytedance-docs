---
title: "Auto-orient"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-auto-orient"
---

This section describes how to automatically rotate the original image. Photos taken by cameras or mobile phones may contain EXIF information, which may contain the orientation parameter. The following table lists the parameters and examples.

<span id="d4548583"></span>
## Parameters


|**Parameter** |**Description** |**Setting** |**Required** |
|---|---|---|---|
|value |Specifies whether to automatically rotate the image. |* 0: no<br><br>* 1: yes |Yes |


<span id="536b1691"></span>
## Note

The `auto-orient` parameter is valid only if the orientation parameter is set for the original image.

<span id="0a484394"></span>
## Examples

Set the image width to 200 pixels without enabling the auto\-orient feature.

[https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200/auto-orient,0](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_200/auto-orient,0)

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2dc2e9769d04cbeac5aba257f77d8e6~tplv-goo7wpa0wc-image.image) </span>
