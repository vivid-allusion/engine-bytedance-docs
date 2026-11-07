---
title: "Advanced Compression"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-advanced-compression"
---

This section describes how to convert the image format to High Efficiency Image Format (HEIF), which has a high compression ratio. The following table lists the parameters and examples.

<span id="903032c3"></span>
## Note

The image width and height can be up to 4,096 pixels for advanced compression.

<span id="c3d857d9"></span>
## Parameters


|**Parameter** |**Description** |**Setting** |**Required** |
|---|---|---|---|
|heic |Convert the original image format to HEIF. |N/A |Yes |


<span id="115ea6f4"></span>
## Examples


* Convert JPEG to HEIF.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample2.jpg?x-tos-process=image/format,heic](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample2.jpg?x-tos-process=image/format,heic)

* Convert JPEG to HEIF and set the resolution to 600 × 400 by specifying the width.

   [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample2.jpg?x-tos-process=image/resize,w_600/format,heic](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample2.jpg?x-tos-process=image/resize,w_600/format,heic)


<span id="0b458edc"></span>
## **Compression ratio comparison**

The following table compares the resolutions and sizes of JPEG (original image) and HEIF (converted). Data in the table indicates that the compression ratio of the HEIF image is higher than that of the JPEG image, effectively saving the bandwidth and costs.


|Format |Resolution |Size |
|---|---|---|
|JPEG (original image) |1920 × 1280 |350 KB |
|HEIF |1920 × 1280 |60 KB (82.9% compression ratio) |
|HEIF |600 × 400 |9 KB (97.4% compression ratio) |
