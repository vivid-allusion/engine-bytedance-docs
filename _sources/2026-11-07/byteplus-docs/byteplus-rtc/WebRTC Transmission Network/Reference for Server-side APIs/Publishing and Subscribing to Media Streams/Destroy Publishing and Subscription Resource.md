---
title: "Destroy Publishing and Subscription Resource"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1553593"
---

To destroy a specified publish\-subscribe resource, you can call this API.

If the call is successful, the specified publish\-subscribe resource is deleted, and any PeerConnection established with it is terminated.

<span id="request-description"></span>
## Request Description


* Request method: **DELETE**

* Request address: **Publish\-subscribe resource URL**


> The value of the Location header returned in the response when the resource is created.


<span id="response-result"></span>
## **Response**

<span id="successful-response-example"></span>
### Successful Response Example


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Status |String |`200 OK` |The request was successful. |


<span id="exception-response-example"></span>
### Exception Response Example


|Parameter | |Type |Example Value |Description |
|---|---|---|---|---|
|Status | |String |`404 Not Found` |The requested resource was not found. |
|Header |Content\-Type |String |`text/plain` |The content type of the response body. |
|Body | |String |`Resource Not Exist` |Resource does not exist |


<span id="request-example"></span>
## Request Example

```Plain
curl --location --request DELETE '<location>'
```


<span id="status-code"></span>
## Status Code

See [Status Codes](https://docs.byteplus.com/docs/byteplus-rtc/132486) for more information on status codes.
