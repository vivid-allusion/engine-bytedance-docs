---
title: "VideoAnimation"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/VideoAnimation"
---

<span id="a180eac4"></span>
## Description

This api converts video files to animations and stores them in the specified bucket.

<span id="4fa4202b"></span>
## Notes


* Audio\-to\-animation conversion only supports asynchronous processing (x\-tos\-async\-process method).

* Video container formats: MP4/TS/MKV.

* Video encoding formats: H264/H265/VP8/VP9/AV1.

* Video resolution limits: [128, 4096].

* Video size limits: video length no longer than 15 minutes.


<span id="ab3b6e8f"></span>
## Request syntax

```HTTP
// Convert the video file example.mkv to a GIF.
POST /example.mkv?x-tos-async-process HTTP/1.1
Host: bucketname.tos-cn-beijing.volces.com
Date: Fri, 28 Oct 2024 06:40:10 GMT
Authorization: TOS qn6q**************:77Dv****************

x-tos-async-process=video/animation,f_gif,w_100,h_100,inter_1000&x-tos-save-object=YWJjLnBuZw==&x-tos-save-bucket=YXJjdGlj
```


<span id="0f91f283"></span>
## Request parameters and headers

For common request headers, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Field name** | ** ** Location |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|---|
|x\-tos\-async\-process |Query |String |Yes |\- |Special identifier for video\-to\-GIF requests. |


<span id="2a64f58c"></span>
## Request body elements


|**Field name** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|ss |Integer |No |0 |Start time for video\-to\-GIF conversion, in milliseconds. Values:<br><br><br>* `0 (default)`: start from the beginning.<br><br>* `Greater than 0`: start from `ss` milliseconds. |
|f |String |Yes |gif |Output animation format, value: `gif`. |
|num |Integer |No |100 |Number of GIF frames, default is unlimited (frames are extracted until the video ends).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the video is shorter than expected, the actual number of extracted frames will be less than the set parameter value.</div><br> |
|inter |Integer |No |1 |Frame extraction interval for GIFs, in milliseconds. By default, all video frames are extracted.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When this value is less than the source video's frame interval (the inverse of the frame rate), frames are extracted according to the source video's frame interval.</div><br> |
|fps |Integer |No |30 |Animation frame rate, default is `inter` inverse. Value range is [0, 240].<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter controls the playback speed of the animation. When set to the default value, it matches the source video playback speed. A value greater than the default speeds up playback; a value less than the default slows it down.</div><br> |
|w |Integer |No |1024 |Output gif width in px, range [32, 4096].<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If set to 0, scale automatically according to source video resolution ratio.</div><br> |
|h |Integer |No |1024 |Output GIF height in px, range [32,4096].<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If set to 0, it will auto\-calculate based on the source video's resolution ratio.</div><br> |
|scaletype |String |No |crop |Scaling mode. The options are as follows:<br><br><br>* `crop`: scale and crop.<br><br>* `stretch` (default): stretch to fill.<br><br>* `fill`: scale and keep black borders.<br><br>* `fit`: scale without black borders, maintain aspect ratio. |


<span id="45de9113"></span>
## Response headers

The response contains common headers. For more information, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="ef4545b2"></span>
## Response body elements


|**Field name** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|status |String |OK |Status code. |


<span id="dce26f64"></span>
## Sample request

```HTTP
POST /example.mkv?x-tos-async-process HTTP/1.1
Host: bucketname.tos-cn-beijing.volces.com
Date: Fri, 28 Oct 2024 06:40:10 GMT
Authorization: TOS qn6q**************:77Dv****************

x-tos-async-process=video/animation,f_gif,w_100,h_100,inter_1000&x-tos-save-object=YWJjLnBuZw==&x-tos-save-bucket=YXJjdGlj
```


<span id="7a0748ba"></span>
## Sample response

```HTTP
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444ed0        
x-tos-request-id: f91b0c03a01300c1-a444ed0            
Date: Fri, 30 Jul 2021 06:45:39 GMT
server: TosServer
Content-Length: 0
{
    "status": "OK"
}  
```
