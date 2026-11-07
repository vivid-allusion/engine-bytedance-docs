---
title: "Create Publishing Resource"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/132482"
---

Before publishing your local audio and video stream to WTN, you should create a publishing resource. For more information about publishing resources, refer to [Publish Resource and Subscription Resource](https://docs.byteplus.com/docs/byteplus-rtc/132443).

<span id="usage"></span>
## Usage

<span id="api-behavior"></span>
### API Behavior

Call this API to send an SDP Offer to the WTN server. If the call is successful, the WTN server will create a publishing resource, and the publishing client will receive an SDP Answer from the WTN server.

<span id="subscription-authentication"></span>
### Subscription Authentication

When creating a publishing resource, you can decide whether to enable subscription authentication. For specific settings, refer to [Authentication](https://docs.byteplus.com/docs/byteplus-rtc/132442).

<span id="precautions"></span>
## Precautions

<span id="after-creating-publishing-resource"></span>
### After Creating Publishing Resource


* If you do not establish a connection within 30 seconds of creating the publishing resource, it is deleted. You must then create a new one.

* If you have already established a connection but are disconnected from the publishing resource due to network issues or other reasons for more than 30 seconds, the publishing resource will be deleted.


<span id="re-publishing"></span>
### Re\-publishing

If you create a publishing resource with an AppID and StreamID that are already in use, the existing resource is terminated. Clients can no longer connect to the old resource, and any active connections are dropped.

<span id="request-instructions"></span>
## Request Instructions


* Request Method: **POST**

* Request URL: `<Domain name>/pub/<AppID>/<StreamID>`


> For the ` ` value, see [API Request Domain names](https://docs.byteplus.com/en/docs/byteplus-rtc/wtn-domain).


<span id="request-parameters"></span>
## Request Parameters

<span id="path"></span>
### Path


|<div style="text-align: center"><br>Parameter</div><br> |<div style="text-align: center"><br>Type</div><br> |<div style="text-align: center"><br>Required</div><br> |<div style="text-align: center"><br>Example Value</div><br> |Description |
|---|---|---|---|---|
|<div style="text-align: center"><br>AppID</div><br> |<div style="text-align: center"><br>String</div><br> |<div style="text-align: center"><br>Yes</div><br> |<div style="text-align: center"><br><code>Your_AppId</code></div><br> |Application ID. Obtained from the console. |
|<div style="text-align: center"><br>StreamID</div><br> |<div style="text-align: center"><br>String</div><br> |<div style="text-align: center"><br>Yes</div><br> |<div style="text-align: center"><br><code>Stream123</code></div><br> |A custom stream identifier. It can be up to 64 characters long and can only contain numbers and letters. |


<span id="header"></span>
### Header


|<div style="text-align: center"><br>Parameter</div><br> |<div style="text-align: center"><br>Type</div><br> |<div style="text-align: center"><br>Required</div><br> |<div style="text-align: center"><br>Example Value</div><br> |Description |
|---|---|---|---|---|
|Content\-Type |String |<div style="text-align: center"><br>Yes</div><br> |<div style="text-align: center"><br><code>application/sdp</code></div><br> |Request content type. The value must be `application/sdp` |
|<div style="text-align: center"><br>Authorization</div><br> |String |<div style="text-align: center"><br>Yes</div><br> |<div style="text-align: center"><br><code>{TokenType} {Token}</code></div><br> |Authorization information.<br><br><br>* `TokenType`: Fixed value: `Bearer`.<br><br>* `Token`: See authentication algorithm. |
|Feedback\-<br><br>Info |String |No |/ |Information about the media server node.<br><br>If the created `PeerConnection` returns `RTCPeerConnection.connectionState == failed`, which means the ICE connection failed, you can call this API again to create a publishing resource. Populate this field with the `Feedback-Info` from the header and the `ClientID` from the query of the previous response. The server will automatically switch to a different media server node. For more information, see [Building a Basic Application](https://docs.byteplus.com/docs/byteplus-rtc/132450). |


<span id="query"></span>
### Query


|<div style="text-align: center"><br>Parameter</div><br> |<div style="text-align: center"><br>Type</div><br> |<div style="text-align: center"><br>Required</div><br> |<div style="text-align: center"><br>Example Value</div><br> |Description |
|---|---|---|---|---|
|<div style="text-align: center"><br>BusinessID</div><br> |<div style="text-align: center"><br>String</div><br> |<div style="text-align: center"><br>No</div><br> |<div style="text-align: center"><br>www\-byteplus\-com</div><br> |A custom identifier used to uniquely identify a business within the same AppID.<br><br><br>* Must be unique within the same AppId.<br><br>* Maximum length of 64 characters.<br><br>* Allowed characters: numbers, letters, `_`, `-`, `@`, and `.`. |
|<div style="text-align: center"><br>SessionID</div><br> |<div style="text-align: center"><br>String</div><br> |<div style="text-align: center"><br>No</div><br> |<div style="text-align: center"><br><code>Session123</code></div><br> |Client\-generated ID for log troubleshooting. |
|<div style="text-align: center"><br>MuteAudio</div><br> |<div style="text-align: center"><br>Bool</div><br> |<div style="text-align: center"><br>No</div><br> |<div style="text-align: center"><br><code>false</code></div><br> |Whether to publish audio data.<br><br><br>* `true`: Do not send audio data.<br><br>* `false`: Send audio data.<br><br><br>The default is `false`. |
|<div style="text-align: center"><br>MuteVideo</div><br> |<div style="text-align: center"><br>Bool</div><br> |<div style="text-align: center"><br>No</div><br> |<div style="text-align: center"><br><code>false</code></div><br> |Whether to publish video data.<br><br><br>* `true`: Do not send video data.<br><br>* `false`: Send video data.<br><br><br>The default is `false`. |
|<div style="text-align: center"><br>ClientIP</div><br> |<div style="text-align: center"><br>String</div><br> |<div style="text-align: center"><br>No</div><br> |<div style="text-align: center"><br><code>123.112.69.85</code></div><br> |The client's public IP address (IPv4 or IPv6). The WTN server uses this address to allocate the optimal media server node for the client.<br><br>Defaults to the source IP address of the HTTP request. |


<span id="body"></span>
### Body


|<div style="text-align: center"><br>Parameter</div><br> |<div style="text-align: center"><br>Type</div><br> |<div style="text-align: center"><br>Required</div><br> |<div style="text-align: center"><br>Example Value</div><br> |Description |
|---|---|---|---|---|
|<div style="text-align: center"><br>data\-raw</div><br> |<div style="text-align: center"><br>String</div><br> |<div style="text-align: center"><br>Yes</div><br> |<div style="text-align: center"><br><code><SDP Offer></code></div><br> |The SDP Offer to send to the server. |


<span id="response-results"></span>
## Response Results

<span id="successful-response-example"></span>
### Successful Response Example


|<div style="text-align: center"><br>Parameter</div><br> ||<div style="text-align: center"><br>Type</div><br> |Example Value |Description |
|---|---|---|---|---|
|<div style="text-align: center"><br>Status</div><br> ||<div style="text-align: center"><br>String</div><br> |`201 Created` |API request successful |
|<div style="text-align: center"><br>Header</div><br><br><br><div style="text-align: center"><br>^^</div><br> |<div style="text-align: center"><br>Content\-Type</div><br><br><br><div style="text-align: center"><br>Location</div><br> |<div style="text-align: center"><br>String</div><br><br><br><div style="text-align: center"><br>String</div><br> |`application/sdp`<br><br>`https://xxxx.com`<br><br>Information about the media server node.<br><br>If the created `PeerConnection` returns `RTCPeerConnection.connectionState == failed`, which means the ICE connection failed, you can call this API again to create a publishing resource. Populate this field with the `Feedback-Info` from the header and the `ClientID` from the query of the previous response. The server will automatically switch to a different media server node. For more information, see Building a Basic Application.<br><br>When using this parameter, you do not need to be concerned with its contents. Directly pass the `Feedback-Info` value returned from the previous request.<br><br>Information about the media server node.<br><br>If the created `PeerConnection` returns `RTCPeerConnection.connectionState == failed`, which means the ICE connection failed, you can call this API again to create a publishing resource. Populate this field with the `Feedback-Info` from the header and the `ClientID` from the query of the previous response. The server will automatically switch to a different media server node. For more information, see Building a Basic Application.<br><br>When using this parameter, you do not need to be concerned with its contents. Directly pass the `Feedback-Info` value returned from the previous request.<br><br>Information about the media server node.<br><br>If the created `PeerConnection` returns `RTCPeerConnection.connectionState == failed`, which means the ICE connection failed, you can call this API again to create a publishing resource. Populate this field with the `Feedback-Info` from the header and the `ClientID` from the query of the previous response. The server will automatically switch to a different media server node. For more information, see Building a Basic Application.<br><br>When using this parameter, you do not need to be concerned with its contents. Directly pass the `Feedback-Info` value returned from the previous request.<br><br>Information about the media server node.<br><br>If the created `PeerConnection` returns `RTCPeerConnection.connectionState == failed`, which means the ICE connection failed, you can call this API again to create a publishing resource. Populate this field with the `Feedback-Info` from the header and the `ClientID` from the query of the previous response. The server will automatically switch to a different media server node. For more information, see Building a Basic Application.<br><br>When using this parameter, you do not need to be concerned with its contents. Directly pass the `Feedback-Info` value returned from the previous request. |Type of content returned<br><br>Publishing resource URL |
|<div style="text-align: center"><br>Body</div><br> ||<div style="text-align: center"><br>String</div><br> |`<SDP Answer>` |Received SDP Answer from the server |


<span id="exception-response-example"></span>
### Exception Response Example


|<div style="text-align: center"><br>Parameter</div><br> ||<div style="text-align: center"><br>Type</div><br> |Example Value |Description |
|---|---|---|---|---|
|<div style="text-align: center"><br>Status</div><br> ||<div style="text-align: center"><br>String</div><br> |`400 Unknown Request` |Unknown request exception |
|<div style="text-align: center"><br>Header</div><br> |<div style="text-align: center"><br>Content\-Type</div><br> |<div style="text-align: center"><br>String</div><br> |`text/plain` |Type of content returned |
|<div style="text-align: center"><br>Body</div><br> ||<div style="text-align: center"><br>String</div><br> |`Resource Not Exist` |Resource does not exist |


<span id="sample-code"></span>
## Sample Code

```Plain Text
curl --location --request POST 'https://wtn.rtcplus.com/pub/<AppID>/<StreamID>' \
--header 'Authorization: Bearer <Token>' \
--header 'Content-Type: application/sdp' \
--data-raw '<SDP Offer>'
```


<span id="sample-response"></span>
## Sample Response

```Plain Text
<SDP Answer>
```


<span id="status-code"></span>
## Status Code

See [Status Codes](https://docs.byteplus.com/docs/byteplus-rtc/132486). for more information.
