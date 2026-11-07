---
title: "Destroy Publishing Resource"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/132483"
---

To terminate a publishing stream and clean up associated resources, you can call this API to destroy a specific publishing resource.

A successful call also destroys the corresponding subscription resource with the same `StreamID` and disconnects any active `PeerConnection`s.

<span id="request-description"></span>
## Request Description


* Request Method: **DELETE**

* Request URL: **Publishing Resource URL**


> Publishing Resource URL: Obtained from the `Location` in the response when the publishing resource is successfully created.


<span id="response"></span>
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
|Status |String |`404 Not Found` |The requested resource was not found. |
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
