---
title: "Set Publishing Configurations"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/161924"
---

To dynamically control media streams for a publishing resource, you can use this API to set its publishing status. This allows you to programmatically enable or disable the audio and video streams.

<span id="prerequisites"></span>
## Prerequisites

Before calling this API, you must have created the corresponding publishing resource, and the resource still exists.

> To create a publishing resource, see [Create Publishing Resource](https://docs.byteplus.com/docs/byteplus-rtc/132482).


<span id="request-description"></span>
## Request Description


* Request Method: **POST**

* Request URL: **Publishing Resource URL**


> This URL is the `Location` value returned in the response when you successfully create the resource.


<span id="request-parameters"></span>
## Request Parameters

<span id="body"></span>
### Body


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|MuteAudio |Bool |No |`false` |Whether to publish audio data.<br><br><br>* `true`: Do not publish audio data.<br><br>* `false`: Publish audio data.<br><br><br>The default is `false`. |
|MuteVideo |Bool |No |`false` |Whether to publish video data.<br><br><br>* `true`: Do not publish video data.<br><br>* `false`: Publish video data.<br><br><br>The default is `false`. |


<span id="response-results"></span>
## Response Results

<span id="successful-response-example"></span>
### Successful Response Example


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Status |String |`200 OK` |The API request was successful |


<span id="exceptional-response-example"></span>
### Exceptional Response Example


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Status |String |`404 Not Found` |An unknown error occurred while processing the request |
|Header: Content\-Type |String |`text/plain` |The type of the returned content |
|Body |String |`Resource Not Exist` |The resource does not exist |


<span id="request-example"></span>
## Request Example

```Plain Text
curl --location --request POST '<location>' --data-raw '{"MuteAudio":true,"MuteVideo":true}'
```


<span id="status-codes"></span>
## Status Codes

For more information, see [Status Codes](https://docs.byteplus.com/docs/byteplus-rtc/132486).
