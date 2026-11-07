---
title: "DeleteBucketRealTimeLog"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DeleteBucketRealTimeLog"
---

<span id="7616d809"></span>
## Description

This interface is used to disable the log analysis feature.

<span id="541ddca9"></span>
## Precautions

After log analysis is disabled, the log topic will not be deleted automatically. Before disabling associated logs, you should first delete the log topic in the log service to avoid incurring further log charges after the logs are disabled.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Since all buckets within the same region share a single topic, deleting the topic for one bucket will also delete the historical log records of other buckets in the same region. For a detailed explanation, please refer to <a href="https://docs.byteplus.com/docs/tos/Why-cant-the-logging-function-be-used">Why does deleting the log topic of a bucket prevent normal use of the log function for other buckets?</a>.</div>


<span id="7afac30c"></span>
## **Request syntax**

```TypeScript
DELETE /?realtimeLog HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 18 Apr 2025 09:44:39 GMT
Authorization: authorization string
```


<span id="d7b813f1"></span>
## **Request parameters and headers**


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|realtimeLog |Query |String |Yes |\- |Represents the special identifier for the GetBucketRealTimeLog request. |


<span id="c3fff379"></span>
## **Request body elements**

This request does not contain any request message elements.

<span id="4f6ce3c6"></span>
## Response headers

This request returns public response message headers; see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="281994a5"></span>
## **Response body elements**

This request does not have a response message element.

<span id="ecc3ae5e"></span>
## **Sample request**

```TypeScript
DELETE /?realtimeLog HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 18 Apr 2025 09:44:39 GMT
Authorization: authorization string
```


<span id="3ccb7bf7"></span>
## **Sample response**

```TypeScript
HTTP/1.1 204 No Content
Date: Fri, 18 Apr 2025 09:44:39 GMT
Server: TosServer
x-tos-id-2: 7a049d0bb80c000a-a444ed0
x-tos-request-id: 7a049d0bb80c000a-a444ed0
```
