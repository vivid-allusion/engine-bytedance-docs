---
title: "CreateAudioConvertJob"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/AudioConvert"
---

<span id="a180eac4"></span>
## Description

This API converts audio files to specified formats and stores them in the designated bucket.

<span id="4fa4202b"></span>
## Notes


* Currently, audio file formats supported for conversion include mp3, wav, aac, m4a, flac, ac3, opus, and oga.

* Audio transcoding only supports asynchronous processing (x\-tos\-async\-process method).


<span id="ab3b6e8f"></span>
## Request syntax

```TypeScript
POST /ObjectName?x-tos-async-process HTTP/1.1
Host: bucketname.tos-cn-beijing.volces.com
Date: GMT Date
Authorization: authorization string
 
x-tos-async-process=audio/convert,f_mp3,ab_128000,abopt_0,ar_0,ac_0,ss_0,t_0&x-tos-save-bucket=dGVzdGJrdA==&x-tos-save-object=dGVzdG9iag==
```


<span id="0f91f283"></span>
## Request parameters and headers

For common request headers, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Field name** | ** **  |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|---|
|x\-tos\-async\-process |Query |String |Yes |\- |Represents a unique identifier for audio transcoding requests. |


<span id="2a64f58c"></span>
## Request body elements


|**Field name** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|x\-tos\-async\-process |String |Yes |audio/convert |Name of the media processing operation, only `audio/convert` is supported. |
|f |String |Yes |mp3 |Transcoding output format, possible values are:<br><br><br>* `mp3`<br><br>* `aac`<br><br>* `m4a`<br><br>* `flac`<br><br>* `oga`<br><br>* `ac3`<br><br>* `opus`<br><br>* `wav` |
|ab |String |Yes |9000 |Transcoded output bitrate, with a range of [8000, 1000000] in bps. |
|abopt |int |No |0 |Audio bitrate options.<br><br>The options are as follows:<br><br><br>* `0` (default): always use the target audio bitrate.<br><br>* `1`: when the source audio bitrate in the splice list is lower than the value of the `ab` parameter, use the lowest source audio bitrate in the splice list.<br><br>* `2`: when the source audio bitrate in the splice list is lower than the value of the `ab` parameter, return a failure.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter must be set together with the value of the <code>ab</code> parameter.</div><br> |
|ar |int |No |8000 |Audio sample rate.<br><br>Defaults to the source audio rate if specified, values include:<br><br><br>* `8000`<br><br>* `11025`<br><br>* `12000`<br><br>* `16000`<br><br>* `22050`<br><br>* `24000`<br><br>* `32000`<br><br>* `44100`<br><br>* `48000`<br><br>* `64000`<br><br>* `88200`<br><br>* `96000`<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The supported sample rates vary by format; for details, see <a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=zh#9a1124e1">Sample rate support for different audio containers</a>.</div><br> |
|ac |int |No |1 |Number of audio channels.<br><br>Matches the specified source audio by default, range: 1 to 8.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Supported channel counts vary by format. For details, see <a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=zh#6b82ba91">Supported audio container parameters</a>.</div><br> |
|ss |int |No |0 |Start time of the transcoded spliced audio.<br><br>Unit is milliseconds. Values:<br><br><br>* `0` (default): start from the beginning.<br><br>* `Greater than 0`: start from `ss` milliseconds. |
|t |int |No |0 |Duration of the transcoding for the concatenated audio.<br><br>Unit is milliseconds, valid values:<br><br><br>* `0` (default): lasts until the end position.<br><br>* `Greater than 0`: lasts for `t` milliseconds. |
|af |String |No |fltp |Sampling format.<br><br>The options are as follows:<br><br><br>* `fltp`<br><br>* `s16`<br><br>* `s16p`<br><br>* `s32`<br><br>* `s32p`<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Different formats support different sampling formats. For details, see <a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=zh#6b82ba91">Audio container parameter support</a>.</div><br> |
|x\-tos\-save\-bucket |String |No |dGVzdGJrdA== |The bucket for storing the transcoded audio files. If not set, it defaults to the bucket of the source audio file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, only same\-region storage for transcoded files is supported, meaning the bucket for transcoded audio files must be in the same region as the source audio file's bucket.</div><br> |
|x\-tos\-save\-object |String |Yes |dGVzdG9iag== |Name of the transcoded audio file, which needs to be Base64 encoded. |


<span id="4f92bd58"></span>
## Response headers

The response contains common headers. For more information, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="ef4545b2"></span>
## Response body elements


|**Field name** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Status |String |OK |Status code. |


<span id="dce26f64"></span>
## Sample request

```TypeScript
POST /example.wav?x-tos-async-process HTTP/1.1
Host: bucketname.tos-cn-beijing.volces.com
Date: GMT Date
Authorization: authorization string
 
x-tos-async-process=audio/convert,f_mp3,ab_128000&x-tos-save-bucket=bkt&x-tos-save-object=test.mp3
```


<span id="7a0748ba"></span>
## Sample response

```TypeScript
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
