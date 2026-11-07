---
title: "Set Subscription Configurations"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/161925"
---

Call this API to set the subscription status, including:


* Whether to subscribe to audio;

* Whether to subscribe to video;

* Whether to subscribe to simulcast streams.


<span id="prerequisites"></span>
## Prerequisites

Before calling this API, you must have created the corresponding subscription resources, and these resources must still exist.

> For information on creating subscription resources, refer to [Create Subscription Resource](https://docs.byteplus.com/docs/byteplus-rtc/132484).

> For the lifecycle of subscription resources, refer to [Publish Resource and Subscription Resource](https://docs.byteplus.com/docs/byteplus-rtc/132443).


<span id="request-description"></span>
## Request Description


* Request Method: **POST**

* Request URL: **Subscription Resource URL**


> Subscription Resource URL: This URL is obtained from the `Location` header in the response when the subscription resource is successfully created.


<span id="request-parameters"></span>
## Request Parameters

<span id="body"></span>
### Body


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|MuteAudio |Bool |No |`false` |Whether to subscribe to audio data.<br><br><br>* `true`: Do not subscribe to audio data;<br><br>* `false`: Subscribe to audio data.<br><br><br>The default value is `false`. |
|MuteVideo |Bool |No |`false` |Whether to subscribe to video data.<br><br><br>* `true`: Do not subscribe to video data;<br><br>* `false`: Subscribe to video data.<br><br><br>The default value is `false`. |
|RID |String |No |`High` |The RTP Stream ID of the simulcast media stream published using the WebRTC protocol.<br><br>Use this parameter to subscribe to a specific stream from multiple simulcast streams. If you do not specify this parameter, the service subscribes to the highest quality simulcast stream by default.<br><br><br>* If the publisher's RID changes, the original subscriber will be disconnected and must re\-subscribe to receive the newly published stream;<br><br>* If the publisher publishes a new media stream with the same RID, the original subscriber will not be disconnected and can receive the newly published stream without re\-subscribing. |


<span id="response-results"></span>
## Response Results

<span id="successful-response-example"></span>
### Successful Response Example


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Status |String |`200 OK` |The API request was successful |


<span id="exceptional-response-example"></span>
### Error Response Example


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Status |String |`404 Not Found` |The requested resource was not found. |
|Header: Content\-Type |String |`text/plain` |The type of the returned content |
|Body |String |`Resource Not Exist` |The resource does not exist |


<span id="request-example"></span>
## Request Example

```Plain Text
curl --location --request POST '<location>' --data-raw '{"MuteAudio":true,"MuteVideo":true,"RID":"High"}'
```


<span id="status-codes"></span>
## Status Codes

For more information, see [Status Codes](https://docs.byteplus.com/docs/byteplus-rtc/132486).
