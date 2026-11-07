---
title: "Information Query"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-information-query"
---

This section describes how to get basic image information, including height, width, size, and format. Any EXIF information contained is returned in JSON format. The following table lists the parameters and examples.

<span id="1b86bc5d"></span>
## Parameters

None.

<span id="b98f654b"></span>
## Examples

Query the image information.

[https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/info](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/info)

```JSON
{
    "ExifOffset": {
        "value": "26"
    },    
    "FileSize": {
        "value": "438212"
    },
    "Format": {
        "value": "png"
    },
    "ImageHeight": {
        "value": "683"
    },
    "ImageWidth": {
        "value": "1023"
    },
    "PixelXDimension": {
        "value": "1023"
    },
    "PixelYDimension": {
        "value": "683"
    }        
}
```
