---
title: "Average Hue Query"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-average-hue-query"
---

This section describes how to get the average hue of the image. The returned result is a JSON hex value. The following table lists the parameters and examples.

<span id="ff757151"></span>
## Parameters

None.

<span id="3a93a465"></span>
## Examples

Get the average hue of the image.

[https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/average-hue](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/average-hue)

```JSON
{
    "RGB": "0x5A79A1"
}
```


The obtained value #5A79A1 represents the following color:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de46d13f1a6341a6a98d26471f413fb4~tplv-goo7wpa0wc-image.image) </span>
