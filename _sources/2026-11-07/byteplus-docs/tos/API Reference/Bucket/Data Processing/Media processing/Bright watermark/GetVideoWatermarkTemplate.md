---
title: "GetVideoWatermarkTemplate"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetVideoWatermarkTemplate"
---

<span id="b6cd98e2"></span>
## Description

This interface queries the watermark template.

<span id="f1ad317d"></span>
## Notes

When used by a sub\-account, the `GetDataProcessTemplate` permission must be granted for the current bucket.

<span id="98f70aca"></span>
## Request syntax

```JSON
GET /?process_template&tag=Watermark&id={} HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="e4d201f9"></span>
## Request parameters and headers 


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|process_template |String |Yes |\- |Watermark template identifier. |
|Tag |String |Yes |Watermark |Task type, the value is `Watermark` only in clear watermark scenarios. |


<span id="207e3151"></span>
## Request body elements

No elements are used.

<span id="192ed7da"></span>
## Response headers

The response contains common headers. For more information, see [Common Parameters](https://arcosite.bytedance.net/docs/6349/75044).

<span id="85f6ba71"></span>
## Response body elements


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|Name |String |Yes<br><br> |watermark\-template\-1 |User\-defined template name:<br><br><br>* Only supports `a-z`, `A-Z`, `0-9`, `_`, `-`, and `.`, with a maximum length of 64 characters; it must start and end with `a-z`, `A-Z`, or `0-9`<br><br>* No duplicate rules allowed. |
|Watermark |Container |Yes |\- |Watermark template detail information. |
|Type |String |Yes |Text |Watermark type:<br><br><br>* Text: text watermark.<br><br>* Image: image watermark.<br><br><br>Parent node: `Watermark`. |
|Pos |String |Yes<br><br> |BottomLeft |Reference position:<br><br><br>* `TopRight`<br><br>* `TopLeft`<br><br>* `BottomRight`<br><br>* `BottomLeft`<br><br>* `Left`<br><br>* `Right`<br><br>* `Top`<br><br>* `Bottom`<br><br>* `Center`<br><br><br>Parent node: `Watermark`. |
|LocMode |String |Yes |Relative |Offset mode:<br><br><br>* `Relativity`: proportional.<br><br>* `Absolute`: fixed position.<br><br><br>Parent node: `Watermark`. |
|Dx |Integer |Yes |10 |Horizontal offset:<br><br><br>* In the image watermark, if `Background` is `true`, when `locMode` is `Relativity`, the value is in %, range: [\-300, 0]; when `locMode` is `Absolute`, the value is in `px`, range: [\-4096, 0].<br><br>* In the image watermark, if `Background` is `false`, when `locMode` is `Relativity`, the value is in %, range: [0 100]; when `locMode` is `Absolute`, the value is in `px`, range: [0 4096].<br><br>* In the text watermark, when `locMode` is `Relativity`, the value is in %, range: [0 100]; when `locMode` is `Absolute`, the value is in `px`, range: [0 4096].<br><br>* When `Pos` is `Top`, `Bottom`, or `Center`, this parameter is invalid.<br><br><br>Parent node: `Watermark`. |
|Dy |Integer |Yes |10 |Vertical offset:<br><br><br>* In the image watermark, if `Background ` is `true`, when `locMode ` is `Relativity `, it is %, with a value range: [\-300, 0]; when `locMode ` is `Absolute `, it is `px`, with a value range: [\-4096, 0].<br><br>* In the image watermark, if `Background ` is `false`, when `locMode ` is `Relativity `, it is %, with a value range: [0, 100]; when `locMode ` is `Absolute `, it is `px`, with a value range: [0, 4096].<br><br>* In the text watermark, when `locMode ` is `Relativity `, it is %, with a value range: [0, 100]; when `locMode ` is `Absolute `, it is `px`, with a value range: [0, 4096].<br><br>* When `Pos ` is `Left`, `Right `, or `Center`, this parameter is invalid.<br><br>* Parent node: `Watermark`. |
|StartTime |Integer |No |0 |Watermark start time in milliseconds, default is 0.<br><br>Parent node: `Watermark`. |
|EndTime |Integer |No |0 |Watermark end time in milliseconds, default value is 0.<br><br>Parent node: `Watermark`. |
|Text |Container |No |\- |Text watermark details.<br><br>Parent node: `Watermark`. |
|FontSize |Integer |Yes |50 |Font size, unit `px`, range [5, 100].<br><br>Parent node: `Text`. |
|FontType<br><br> |String |Yes |DejaVu Sans |Font types supported include:<br><br><br>* `wqy-zenhei`: WenQuanYi Zen Hei.<br><br>* `wqy-microhei`: WenQuanYi Micro Hei.<br><br>* `fangzhengshusong`: Founder Shu Song.<br><br>* `fangzhengkaiti`: Founder Kai Ti.<br><br>* `fangzhengheiti`: Founder Hei Ti.<br><br>* `fangzhengfangsong`: Founder Fang Song.<br><br>* `droidsansfallback`:DroidSansFallback.<br><br><br>Parent node: `Text`. |
|FontColor |String |Yes |white |Font color, hexadecimal RGB.<br><br>Parent node: `Text`. |
|Transparency |Integer |Yes |50 |Watermark opacity, unit %, range [1, 100].<br><br>Parent node: `Text`. |
|Text |String |Yes |Test<br><br> |The watermark text content must not exceed 64 characters and supports only Chinese, English, numbers, underscore (`_`), hyphen (`-`), and asterisk (`*`).<br><br>Parent node: `Text`. |


<span id="fcecc287"></span>
## Sample request

```JSON
GET /?process_template&tag=Watermark&id={} HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="3a4f4203"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Content-Type: application/json
Content-Length: <length>
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0

{
    "Tag": "Watermark",
    "ID": "31333538316165386539679601************",
    "Name": "watermark-template-1",
    "WatermarkConfig": {
        "Type": "Text",
        "Pos": "BottomLeft",
        "LocMode": "Relative",
        "Dx": 10,
        "Dy": 10,
        "StartTime": 0,
        "EndTime": 0,
        "Text": {
            "FontSize": 50,
            "FontType": "DejaVu Sans",
            "FontColor": "white",
            "Transparency": 50,
            "Text": "Test"
        }
    }
}
```
