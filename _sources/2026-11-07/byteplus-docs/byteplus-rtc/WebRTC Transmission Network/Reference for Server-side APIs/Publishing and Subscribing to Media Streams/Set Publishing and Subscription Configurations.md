---
title: "Set Publishing and Subscription Configurations"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1553594"
---

Call this interface to set the publish\-subscribe status, including whether to publish/subscribe to audio and whether to publish/subscribe to video.

<span id="notes"></span>
## Notes

<span id="prerequisites"></span>
### Prerequisites

You can only call this interface after creating a publish\-subscribe resource and before it is destroyed.

> To create publish\-subscribe resources, see [Create Publishing and Subscription Resource](https://docs.byteplus.com/docs/byteplus-rtc/docs-1553592). For the life cycle of publish\-subscribe resources, see [Publish Resource and Subscription Resource](https://docs.byteplus.com/docs/byteplus-rtc/132443).


<span id="request-description"></span>
## Request Description


* Request method: **POST**

* Request address: **Publish\-subscribe resource URL**


> The `Location` URL returned in the response from a successful resource creation request.


<span id="request-parameters"></span>
## Request Parameters

<span id="header"></span>
### Header


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Content\-Type |String |Yes |`application/json` |Request content type. Fixed value: `application/json` |


<span id="body"></span>
### Body


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Pub |object |No |\- |Configuration for publishing streams. |
|Sub |object |No |\- |Configuration for subscribing to streams. |


Pub  


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|MuteAudio |Bool |No |`false` |Whether to publish audio data.<br><br><br>* `true`: Do not publish audio data.<br><br>* `false`: Publish audio data.<br><br>   The default value is `false`. |
|MuteVideo |Bool |No |`false` |Whether to publish video data.<br><br><br>* `true`: Do not publish video data.<br><br>* `false`: Publish video data.<br><br>   The default value is `false`. |


Sub  


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|MuteAudio |Bool |No |`false` |Whether to subscribe to audio data.<br><br><br>* `true`: Do not subscribe to audio data.<br><br>* `false`: Subscribe to audio data.<br><br>   The default value is `false`. |
|MuteVideo |Bool |No |`false` |Whether to subscribe to video data.<br><br><br>* `true`: Do not subscribe to video data.<br><br>* `false`: Subscribe to video data.<br><br>   The default value is `false`. |


<span id="response-result"></span>
## Response

<span id="successful-response-example"></span>
### Successful Response Example


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Status |String |`200 OK` |The request was successful. |


<span id="exception-response-example"></span>
### Exception Response Example


|Parameter ||Type |Example Value |Description |
|---|---|---|---|---|
|Status ||String |`404 Not Found` |The requested resource was not found. |
|Header |Content\-Type |String |`text/plain` |The content type of the response. |
|Body ||String |`Resource Not Exist` |Resource does not exist |


<span id="request-example"></span>
## Request Example

```Plain
curl --location --request POST '<location>' --data-raw '{"Pub":{"MuteAudio":true,"MuteVideo":true},"Sub":{"MuteAudio":true,"MuteVideo":true}}'
```


<span id="status-code"></span>
## Status Code

For more information on status codes, see [Status Codes](https://docs.byteplus.com/docs/byteplus-rtc/132486).
