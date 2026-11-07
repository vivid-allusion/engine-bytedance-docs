---
title: "Format Conversion"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-format-conversion"
---

This section describes how to convert the format of the original image. The following table lists the parameters and examples.

<span id="24a59877"></span>
## Precautions

Format conversion operations are only supported for original images in jpg/jpeg, png, bmp, gif, webp, tiff, and heic formats.

<span id="04bc80ef"></span>
## Parameters


|**Parameter** |**Description** |**Setting** |**Required** |
|---|---|---|---|
|jpg |Saves the file as a JPG file. |If the original image format is PNG, WEBP, or BMP that supports an alpha channel, the transparent parts are filled with the white color by default. |Yes |
|png |Saves the file as a PNG file. |None |Yes |
|webp |Saves the file as a WEBP file. |None |Yes |
|bmp |Saves the file as a BMP file. |None |Yes |
|gif |Saves the file as a GIF file. |* If the original image is a GIF image, save the processed image as a GIF image.<br><br>* If the original image is not a GIF image, save the processed image in the same format as the original image. |Yes |
|tiff |Saves the file as a TIFF file. |None |Yes |
|heic |Save the file as an HEIC file. |None. |Yes |


<span id="3b75a788"></span>
## Note

If an image is to be resized, we recommend that you put the format conversion parameter at the end of processing parameters.

<span id="6f246c53"></span>
## Examples


* Save the image as a JPG image.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-oss-process=image/format,jpg](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-oss-process=image/format,jpg)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2aee785e60394af99c6dc61c7963a593~tplv-goo7wpa0wc-image.image) </span>

* Set the height to 100 and save the file as a JPG file.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,h_100/format,jpg](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,h_100/format,jpg)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bacac36525384ee181b291ce0f758894~tplv-goo7wpa0wc-image.image) </span>
