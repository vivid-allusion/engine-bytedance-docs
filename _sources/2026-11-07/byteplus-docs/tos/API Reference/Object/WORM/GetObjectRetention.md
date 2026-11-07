---
title: "GetObjectRetention"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Getobjectretention"
---

<span id="e082025f"></span>
## **Function Description**

This interface is used to obtain the retention policy information of an object.

<span id="f202c465"></span>
## Precautions

When versioning is enabled for a storage bucket, if no version number is specified, the retention policy information for the latest version object will be retrieved by default.

<span id="0b5a9c60"></span>
## **Request syntax**

```JSON
GET /objectname?retention HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="32a71d6b"></span>
## **Request parameters and headers**

The public message header used by this request. See [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |Required |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|retention |Query |String |Yes |\- |A special identifier representing the GetObjectRetention request. |
|versionId |Query |String |No |57AF1A32CECB56721267 |The version number of the object. |


<span id="2fb2fca9"></span>
## **Request body elements**

This request does not use message elements.

<span id="ef525baf"></span>
## **Response headers**

This request returns public response message headers.

<span id="95bd0f74"></span>
## **Response body elements**


|**Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Mode |String |COMPLIANCE |The retention policy mode can only be set to `COMPLIANCE`, which means compliance mode. In this mode, no user can delete or overwrite locked objects during the retention period. |
|RetainUntilDate |String |2025\-01\-01T00:00:00Z |Retention period, the deadline by which an object cannot be deleted or overwritten. |


<span id="e1fac471"></span>
## **Sample request**

```JSON
GET /objectname?retention HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="4f9e249d"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444ed0
x-tos-request-id: f91b0c03a01300c1-a444ed0
Date: Fri, 30 Jul 2021 06:45:39 GMT
server: TosServer
Content-Length: 62

{
    "Mode": "COMPLIANCE",
    "RetainUntilDate": "2025-07-22T00:00:00Z"
}
```
