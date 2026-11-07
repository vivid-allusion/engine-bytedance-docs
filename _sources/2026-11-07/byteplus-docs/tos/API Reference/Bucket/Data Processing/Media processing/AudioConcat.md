---
title: "AudioConcat"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/AudioConcat"
---

<span id="a180eac4"></span>
## Description

This interface is used for concatenating audio segments. You can use the audio segment synthesis feature to combine multiple audio clips into one and convert it to the required format.

<span id="4fa4202b"></span>
## Notes


* Audio segment concatenation only supports asynchronous processing (x\-oss\-async\-process mode).

* You must have the necessary permissions for `PostDataProcess` data processing.

* Supports concatenation of up to 11 audio segments. After all segments are concatenated, the total duration must not exceed 1 hour.


<span id="ab3b6e8f"></span>
## Request syntax

```HTTP
// Perform audio splicing on the file example.wav.
POST /example.wav?x-tos-async-process HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 28 Oct 2024 06:40:10 GMT
Authorization: <authorization string>

x-tos-async-process=audio/concat,f_aac,ac_2,ar_44100,ab_96000/pre,o_cHJlLm1wMw==/sur,o_c3VyXzEuYWFj,ss_4000,t_10000/sur,o_c3VyXzIuYWFj,ss_10000&x-tos-save-object=b3V0cHV0LmFhYw
```


<span id="0f91f283"></span>
## Request parameters and headers 

For common request headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|---|
|x\-tos\-async\-process |Query |String |Yes |\- |Special identifier representing audio segment concatenation requests |


<span id="2a64f58c"></span>
## Request body elements

<span id="f9e73802"></span>
### Concatenation parameters

Concatenate according to the order of `pre` and `sur` in the request string, as follows:


* `/pre`: the audio file to prepend.

* `/sur`: the audio file to append.



|**Name** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|ss |int |No |0 |Start time for stitching prefix or suffix audio.<br><br>Unit is milliseconds; values:<br><br><br>* `0` (default): Start from the beginning.<br><br>* `Greater than 0`: Start from `ss` milliseconds. |
|t |int |No |0 |Duration of prefix or suffix audio splicing.<br><br>Unit is milliseconds; values:<br><br><br>* `0` (default): Continues until the end position.<br><br>* `Greater than 0`: Continues for `t` milliseconds. |
|o |String |Yes |\- |Object under the current Bucket.<br><br>Must be encoded using Base64 URL\-safe method. |


<span id="75551361"></span>
### Transcoding parameters


|**Name** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|ss |int |No |0 |Transcoding start time of the spliced audio.<br><br>Unit is milliseconds; values:<br><br><br>* `0` (default): Start from the beginning.<br><br>* `Greater than 0`: Start from `ss` milliseconds. |
|t |int |No |0 |Duration of transcoding for the spliced audio.<br><br>Unit is milliseconds; values:<br><br><br>* `0` (default): Continues until the end position.<br><br>* `Greater than 0`: Lasts for `t` milliseconds. |
|f |String |Yes |wav |Audio container.<br><br>Options:<br><br><br>* `wav`<br><br>* `mp3`<br><br>* `aac`<br><br>* `flac`<br><br>* `oga`<br><br>* `ac3`<br><br>* `opus` |
|ar |int |No |8000 |Audio sample rate.<br><br>Defaults to match the specified source audio; values:<br><br><br>* `8000`<br><br>* `11025`<br><br>* `12000`<br><br>* `16000`<br><br>* `22050`<br><br>* `24000`<br><br>* `32000`<br><br>* `44100`<br><br>* `48000`<br><br>* `64000`<br><br>* `88200`<br><br>* `96000`<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Sampling rates supported vary by format. For details, see <a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=en#9a1124e1">Support for different audio container sample rates</a>.</div><br> |
|ac |int |No |1 |Number of audio channels.<br><br>Defaults to the source audio setting. Valid range: 1 to 8.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The number of channels supported varies by format. See <a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=en#6b82ba91">Support for different audio container parameters</a> for details.</div><br> |
|ab |int |No |1000 |Audio bit rate (bitrate).<br><br>Unit is bits per second (bps), range: 1000~10000000. |
|abopt |String |No |0 |Audio bitrate options.<br><br>The values are:<br><br><br>* `0` (default): Always use the target audio bitrate.<br><br>* `1`: If any source audio bitrate in the splice list is less than the `ab` parameter, use the smallest source audio bitrate in the splice list.<br><br>* `2`: If any source audio bitrate in the splice list is less than the `ab` parameter, return failure.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter must be set together with the <code>ab</code> parameter.</div><br> |
|sf |String |No |fltp |Sampling format.<br><br>Options:<br><br><br>* `fltp`<br><br>* `s16`<br><br>* `s16p`<br><br>* `s32`<br><br>* `s32p`<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The supported sampling formats vary by format. For details, see <a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=en#6b82ba91">Support for different audio container parameters</a>.</div><br> |


<span id="6b82ba91"></span>
#### **Support for different audio container parameters**


|**Container format** |**Encoding format** |**Sampling rate** |**Sampling format** |**Number of channels** |**Bit rate** |
|---|---|---|---|---|---|
|mp3 |mp3 |Partially supported |fltp/s16p/s32p |1 or 2 |Supported |
|aac |aac |Supported |fltp |1, 2, 4, 5, 6, or 8 |Supported |
|flac |flac |Supported |s16/s32/s16p/s32p |1, 2, 4, 5, 6, or 8 |Not supported |
|oga |vorbis |Supported |fltp |2 |Not supported |
|ac3 |ac3 |Partially supported |fltp |1, 2, 3, 4, 5, or 6 |Supported |
|opus |opus |Partially supported |s16 |1 or 2 |Supported |
|wav |pcm_s16le |Supported |s16 |1 or 2 |Not supported |


<span id="9a1124e1"></span>
#### **Support for different audio container sample rates**


|**Container format** |**mp3** |**aac** |**flac** |**oga** |**ac3** |**opus** |**wav** |
|---|---|---|---|---|---|---|---|
|8000 |Y |Y |Y |Y |N |Y |Y |
|11025 |Y |Y |Y |Y |N |N |Y |
|12000 |Y |Y |Y |Y |N |N |Y |
|16000 |Y |Y |Y |Y |N |Y |Y |
|22050 |Y |Y |Y |Y |N |N |Y |
|24000 |Y |Y |Y |Y |N |Y |Y |
|32000 |Y |Y |Y |Y |Y |N |Y |
|44100 |Y |Y |Y |Y |Y |N |Y |
|48000 |Y |Y |Y |Y |Y |Y |Y |
|88200 |N |Y |Y |Y |N |N |Y |
|96000 |N |Y |Y |Y |N |N |Y |


<span id="45de9113"></span>
## Response headers

The response contains common headers. For more information, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="ef4545b2"></span>
## Response body elements


|**Name** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|status |String |OK |Status code. |


<span id="dce26f64"></span>
## Sample request

```HTTP
POST /example.wav?x-tos-async-process HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 28 Oct 2024 06:40:10 GMT
Authorization: <authorization string>

x-tos-async-process=audio/concat,f_aac,ac_2,ar_44100,ab_96000/pre,o_cHJlLm1wMw==/sur,o_c3VyXzEuYWFj,ss_4000,t_10000/sur,o_c3VyXzIuYWFj,ss_10000&x-tos-save-object=b3V0cHV0LmFhYw
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
