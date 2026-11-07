---
title: "Destroy Subscription Resource"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/132485"
---

<span id="destroy-the-specified-subscription-resource"></span>
## Destroy a Subscription Resource

Call this API to destroy the specified subscription resource.

Destroying a subscription resource has no impact on the corresponding publishing resource.

<span id="precautions"></span>
## Precautions

A successful call disconnects the `PeerConnection` to this subscription resource.

<span id="request-description"></span>
## Request Description


* Request Method: **DELETE**

* Request URL: **Subscription Resource URL**


> Subscription Resource URL: The URL from the `Location` header in the response to a successful resource creation request.


<span id="response-results"></span>
## Response

<span id="successful-response-example"></span>
### Successful Response Example


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Status |String |`200 OK` |The API request was successful |


<span id="exceptional-response-example"></span>
### Error Response Example


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Status |String |`404 Not Found` |The specified resource was not found. |
|Header: Content\-Type |String |`text/plain` |The type of the returned content |
|Body |String |`Resource Not Exist` |The resource does not exist |


<span id="request-example"></span>
## Request Example

```Plain Text
curl --location --request DELETE '<location>'
```


<span id="status-codes"></span>
## Status Codes

For more information, see [Status Codes](https://docs.byteplus.com/docs/byteplus-rtc/132486).
