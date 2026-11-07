---
title: "PutVideoWatermarkTemplate"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutVideoWatermarkTemplate"
---

<span id="2c71c3e9"></span>
## Description

This API uploads visible watermark templates.

<span id="77b41590"></span>
## Notes


* The maximum size of a single rule body is 20KB, and up to 100 custom templates are allowed.

* When used by a sub\-account, the current bucket must have `PutDataProcessTemplate` permission granted.


<span id="2570796e"></span>
## Request syntax

<span id="fd51bf1c"></span>
### Text watermark 

```JSON
PUT /?process_template&tag=Watermark HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Content-Type: application/json
Content-Length: <length>
Authorization: authorization string

{
  "Tag": "Watermark", // fixed identifier
  "Name": "my-test-watermark", // user-defined name
  "WatermarkConfig": {
    "Type": "Text", // text watermark parameters;
    "Pos": "TopRight", // reference position
    "LocMode": "Relative", // offset mode
    "Dx": 10, // horizontal offset
    "Dy": 10, // vertical offset
    "StartTime": 0, // text watermark start time in milliseconds, default 0
    "EndTime": 10000, // text watermark end time in milliseconds, default 0 means video end time
    "Text": { // text watermark settings, effective when Type is Text
      "FontSize": 100, // font size
      "FontType": "fangzhengheiti", // font type
      "FontColor": "#FF0000", // font color
      "Transparency": 20, // opacity, unit %
      "Text": "hello world" // watermark content
    }
  }
}
```


<span id="be0101bb"></span>
### Image watermark

```JSON
PUT /?process_template&tag=Watermark HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Content-Type: application/json
Content-Length: <length>
Authorization: authorization string

{
  "Tag": "Watermark", // Fixed identifier
  "Name": "my-test-watermark", // User-defined name
  "WatermarkConfig": {
    "Type": "Image", // Image watermark
    "Pos": "TopRight", // Reference position
    "LocMode": "Relative", // Offset method
    "Dx": 10, // Horizontal offset
    "Dy": 10, // vertical offset
    "StartTime": 0, // watermark start time in milliseconds, default 0
    "EndTime": 10000, // watermark end time in milliseconds, default 0 means video end time
    "Image": { // image watermark settings, effective when Type is Image
      "Url": "http://myhost.com/my-watermark-img", // watermark image URL
      "Mode": "Fixed", // size mode
      "Width": 3200, // watermark image width
      "Height": 800, // watermark image height
      "Transparency": 20, // opacity in %
      "Background": false // background image enabled
    }
  }
}
```


<span id="3119237d"></span>
## Request parameters and headers 


|Name |  |Type |Required |Example value |Description |
|---|---|---|---|---|---|
|process_template |Query |String |Yes |\- |Watermark template identifier, fixed as `process_template`, no value needed. |
|tag |Query |String |Yes |Watermark |Template type, the value is `Watermark` only in transparent watermark scenarios. |


<span id="ca094fef"></span>
## Request body elements


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|Tag |String |Yes |Watermark |Fixed identifier. The watermark template value can only be `Watermark`, and it must match the `Query` parameter `tag`. |
|Name |String |Yes<br><br> |my\-test\-watermark |User\-defined template name:<br><br><br>* Supports only a\-z, A\-Z, 0\-9, _, \-, and ., with a maximum length of 64 characters; must start and end with a\-z, A\-Z, or 0\-9.<br><br>* No duplicate rules allowed. |
|WatermarkConfig |Container |Yes |\- |Watermark template detail information. |
|Type |String |Yes |Text |Watermark type:<br><br><br>* `Text`: text watermark.<br><br>* `Image`: image watermark.<br><br><br>Parent node: `Watermark`. |
|Pos |String |Yes<br><br> |TopRight |Reference position (see watermark position description in the image below):<br><br><br>* `TopRight`.<br><br>* `TopLeft`<br><br>* `BottomRight`.<br><br>* `BottomLeft`.<br><br>* `Left`<br><br>* `Right`.<br><br>* `Top`.<br><br>* `Bottom`.<br><br>* `Center`.<br><br><br>Parent node: `Watermark`. |
|LocMode |String |Yes |Relative |watermark offset mode, options are:<br><br><br>* `Relativity`: proportional.<br><br>* `Absolute`: fixed position.<br><br><br>parent node: `Watermark `. |
|Dx |Integer |Yes |10 |Horizontal offset.<br><br><br>* For image watermarks, if `Background` is `true`, when `locMode` is `Relativity`, the value is a percentage within [\-300 0]; when `locMode` is `Absolute`, the value is in pixels within [\-4096 0].<br><br>* For image watermarks, if `Background` is `false`, when locMode is `Relativity`, the value is a percentage within [0 100]; when `locMode` is `Absolute`, the value is in pixels within [0 4096].<br><br>* For text watermarks, when `locMode` is `Relativity`, the value is a percentage within [0 100]; when `locMode` is `Absolute`, the value is in pixels within [0 4096].<br><br>* This parameter is invalid when `Pos` is `Top`, `Bottom`, or `Center`.<br><br><br>Parent node: `Watermark`. |
|Dy |Integer |Yes |10 |Vertical offset.<br><br><br>* For image watermarks, if `Background` is `true` and `locMode` is `Relativity`, the value is a percentage ranging from [\-300 0]; if `locMode` is `Absolute`, the value is in pixels ranging from [\-4096 0].<br><br>* For image watermarks, if `Background` is `false` and `locMode` is `Relativity`, the value is a percentage ranging from [0 100]; if `locMode` is `Absolute`, the value is in pixels ranging from [0 4096].<br><br>* For text watermarks, when `locMode` is `Relativity`, the value is a percentage ranging from [0 100]; when `locMode` is `Absolute`, the value is in pixels ranging from [0 4096].<br><br>* When `Pos` is `Left`, `Right`, or `Center`, this parameter is invalid.<br><br><br>Parent node: `Watermark`. |
|StartTime |Integer |No |0 |Watermark start time in milliseconds, default is 0.<br><br>Parent node: `Watermark`. |
|EndTime |Integer |No |10000 |Watermark end time in milliseconds. Default is 0 (indicating it follows the video end time). Must be ≥ `StartTime`.<br><br>Parent node: `Watermark`. |
|Text |Container |No |\- |Text watermark details. Required when `Type` is `Text`.<br><br>Parent node: `Watermark`. |
|FontSize |Integer |Yes |100 |Font size in px, value range [5, 100].<br><br>Parent node: `Text`. |
|FontType<br><br> |String |Yes |fangzhengheiti |Font types, supporting the following fonts:<br><br><br>* `wqy-zenhei`: WenQuanYi Zen Hei.<br><br>* `wqy-microhei`: WenQuanYi Micro Hei.<br><br>* `fangzhengshusong`: Fangzheng Shusong.<br><br>* `fangzhengkaiti`: Fangzheng KaitI.<br><br>* `fangzhengheiti`: Fangzheng HeiTi.<br><br>* `fangzhengfangsong`: Fangzheng Fangsong.<br><br>* `droidsansfallback`：DroidSansFallback.<br><br><br>Parent node: `Text`. |
|FontColor |String |Yes |#FF0000 |Font color, hexadecimal RGB.<br><br>Parent node: `Text`. |
|Transparency |Integer |Yes |20 |watermark opacity, unit %, range [1, 100].<br><br>parent node: `Text`. |
|Text |String |Yes |hello world<br><br> |Watermark text content, no more than 64 characters, supports Chinese, English, numbers, underscore (_), hyphen (\-), and asterisk (\*).<br><br>Parent node: `Text`. |
|Image |Container |No |\- |Image watermark details information. `Type ` is required when `Image `.<br><br>Parent node: `Watermark `. |
|Url |String |Yes |http://myhost.com/my\-watermark\-img |The watermark image URL cannot be empty.<br><br>Parent node: `Image`. |
|Mode |String |Yes |Fixed |Size mode:<br><br><br>* `Original`: original size.<br><br>* `Proportion`: scale proportionally.<br><br>* `Fixed`: fixed size.<br><br><br>Parent node: `Image`. |
|Width<br><br> |Integer |No |3200 |Watermark image width:<br><br><br>* When `Mode` is `Original`, setting watermark image width is not supported.<br><br>* When `Mode` is `Proportion`, unit is %, background image range: [100 300]; foreground image range: [1 100], relative to video width, max not exceeding 4096 px.<br><br>* When `Mode` is `Fixed`, unit is px, value range: [8, 4096].<br><br>* If only `Width` is set, then `Height` is calculated based on the watermark image ratio.<br><br><br>Parent node: `Image`. |
|Height |Integer |No |800 |Watermark image height:<br><br><br>* When `Mode` is `Original`, setting the watermark image height is not supported.<br><br>* When `Mode` is `Proportion`, the unit is %, background image value range: [100 300]; foreground image value range: [1 100], relative to video height, max not exceeding 4096 px.<br><br>* When `Mode` is `Fixed`, the unit is px, value range: [8, 4096].<br><br>* If only `Height` is set, `Width` is calculated according to the watermark image ratio. |
|Transparency |Integer |Yes |20 |Watermark opacity, in %, value range [1, 100].<br><br>Parent node: `Image`. |
|Background |Bool |No |false |Whether it is a background image, the values are as follows:<br><br><br>* `true`.<br><br>* `false `.<br><br><br>Parent node: `Image`. |


<span id="9453bcf4"></span>
### Watermark location description

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b7d0950fb374942f1526d9ec5cbff13c.png) </span>

<span id="e2c57add"></span>
## Response headers

The response contains common headers. For more information, see [Common Parameters](https://arcosite.bytedance.net/docs/6349/75044).

<span id="b70b33cf"></span>
## Response body elements


|Name |Type |Example value |Description |
|---|---|---|---|
|template_id |String |393161343761366633396119012ee2450b08 |Unique ID for creating audio transcoding templates. |


<span id="8543df43"></span>
## Sample request

<span id="765ff55a"></span>
### Text watermark 

```JSON
PUT /?process_template&tag=Watermark HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Content-Type: application/json
Content-Length: <length>
Authorization: authorization string

{
  "Tag": "Watermark", // fixed identifier
  "Name": "my-test-watermark", // user-defined name
  "WatermarkConfig": {
    "Type": "Text", // text watermark
    "Pos": "TopRight", // reference position
    "LocMode": "Relative", // offset method
    "Dx": 10, // horizontal offset
    "Dy": 10, // vertical offset
    "StartTime": 0, // watermark start time in milliseconds, default is 0
    "EndTime": 10000, // watermark end time in milliseconds, default 0 means video end time
    "Text": { // text watermark settings, effective when Type is Text
      "FontSize": 100, // font size
      "FontType": "fangzhengheiti", // font type
      "FontColor": "#FF0000", // font color
      "Transparency": 20, // opacity in %,
      "Text": "hello world" // watermark content
    }
  }
}
```


<span id="2027d19e"></span>
### Image watermark

```JSON
PUT /?process_template&tag=Watermark HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Content-Type: application/json
Content-Length: <length>
Authorization: authorization string

{
  "Tag": "Watermark", // fixed identifier
  "Name": "my-test-watermark", // user-defined name
  "WatermarkConfig": {
    "Type": "Image", // adding watermarks
    "Pos": "TopRight", // reference position
    "LocMode": "Relative", // offset method
    "Dx": 10, // horizontal offset
    "Dy": 10, // vertical offset
    "StartTime": 0, // watermark start time in milliseconds, default 0
    "EndTime": 10000, // watermark end time in milliseconds, default 0 means video end time
    "Image": { // image watermark settings, effective when Type is Image
      "Url": "http://myhost.com/my-watermark-img", // watermark image URL
      "Mode": "Fixed", // size mode
      "Width": 3200, // watermark image width
      "Height": 800, // watermark image height
      "Transparency": 20,// opacity, unit %
      "Background": false // whether background image
    }
  }
}
```


<span id="d6970c38"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Content-Type: application/json
Content-Length: <length>
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0

393161343761366633396119012ee2450b08
```
