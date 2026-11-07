---
title: "Pm3u8"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Pm3u8"
---

<span id="eed09456"></span>
## Feature description

Call the Pm3u8 API to obtain download authorization for private m3u8 files.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">HNS buckets do not support the Pm3u8 API at this time.</div>


<span id="4aa92572"></span>
## Prerequisites

The private m3u8 file access feature must be enabled. For details, see [Enabling the Access to Private m3u8 Files](https://docs.byteplus.com/docs/tos/Accessing-private-m3u8-files#enabling-the-access-to-private-m3u8-files).

<span id="1197ee5b"></span>
## Request syntax

```Bash
GET /ObjectName?ci-process=pm3u8&expires=3600 HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Mon, 31 Oct 2016 12:00:00 GMT
Authorization: authorization string
Content-Length: length
```


<span id="ff5f31eb"></span>
## Request parameters and headers


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|---|
|ci\-process |Header |String |Yes |pm3u8 |Data processing type. The value is `pm3u8`. |
|expires |Header |String |Yes |3600 |Relative valid period for private m3u8 file download authorization, in seconds, range is [3600,43200]. |


<span id="37895142"></span>
## Request body elements

No elements are used.

<span id="09e6b24a"></span>
## Response headers

The common response headers returned by this request; see [common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="6210854d"></span>
## **Response body elements**

Returns the content of the private m3u8 file.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Copy the API endpoint address with authentication information into the browser to view the audio and video data corresponding to the m3u8 file.</div>


<span id="825209ea"></span>
## Sample request

```Bash
GET /video.m3u8?ci-process=pm3u8&expires=3600 HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Mon, 31 Oct 2016 12:00:00 GMT
Authorization: authorization string
Content-Length: length
```


<span id="ce23c568"></span>
## Sample response

```Bash
HTTP/1.1 200 OK
Date: Sat, 07 Oct 2023 09:02:23 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: 0
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-MEDIA-SEQUENCE:0
#EXT-X-TARGETDURATION:15
#EXTINF:11.833,
360p_000.ts?X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential=AKTP07S7AdGne3lpuKJDIXgN5ekuHEUIt1XoondtPF2Z1%2F202****%2Fcn-beijing-%2Ftos%2Freque&X-Tos-Date=20250318T091450Z&X-Tos-Expires=3600&X-Tos-Security-Token=nChZVYWpmWFJsU2hNMlVORWM2QWlwM1VB.CioKFlp0clhwbUZPdWFzZkVOWmZLRkZiaFESENberzPBOkh4vA97aDjZPPsQj_DkvgYYz8HnvgYgpKqAgAgoBDCLg1M6K1NlcnZpY2VSb2xlZm9yVE9TRGF0YVByb2Nlc3MvdG9zZGF0YXByb2Nlc3NCA3Rvc1IOdG9zZGF0YXByb2Nlc3NYA3oDdG9z.Ldyx5hHF_3FPU2L8C2_5hxPqYAqfH74qPdU6BEJTOQY6OCuBy8hducDHUYM8UxFctUOvJQ20t5vi****&X-Tos-Signature=663562f6dfb18069a816b3a6fe1a9674d8919679bd2131e4a71711d39354****&X-Tos-SignedHeaders=host
#EXTINF:10.917,
360p_001.ts?X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential=AKTP07S7AdGne3lpuKJDIXgN5ekuHEUIt1XoondtPF2Z1%2F2025****%2Fcn-beijing-%2Ftos%2Frequest&X-Tos-Date=20250318T091450Z&X-Tos-Expires=3600&X-Tos-Security-Token=nChZVYWpmWFJsU2hNMlVORWM2QWlwM1VB.CioKFlp0clhwbUZPdWFzZkVOWmZLRkZiaFESENberzPBOkh4vA97aDjZPPsQj_DkvgYYz8HnvgYgpKqAgAgoBDCLg1M6K1NlcnZpY2VSb2xlZm9yVE9TRGF0YVByb2Nlc3MvdG9zZGF0YXByb2Nlc3NCA3Rvc1IOdG9zZGF0YXByb2Nlc3NYA3oDdG9z.Ldyx5hHF_3FPU2L8C2_5hxPqYAqfH74qPdU6BEJTOQY6OCuBy8hducDHUYM8UxFctUOvJQ20t5vi3BK****&X-Tos-Signature=88d094acf7f74c6c819dbfa77549afea6242e3f501e31ab9379e7dc6c963****&X-Tos-SignedHeaders=host
```
