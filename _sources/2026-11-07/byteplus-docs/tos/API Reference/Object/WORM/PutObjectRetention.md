---
title: "PutObjectRetention"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Putobjectretention"
---

<span id="3eca8397"></span>
## **Function Description**

This interface is used to create or modify the retention policy of an object.

<span id="ec5c2281"></span>
## Prerequisites

Before creating an object retention policy using the PutObjectRetention API, you must first enable the object lock feature. For detailed instructions, see [Set Object Retention Period](https://docs.byteplus.com/docs/tos/Configure-retention-policy#f5d62294).

<span id="2fd13a14"></span>
## Precautions


* When versioning is enabled for a storage bucket, if no version number is specified, a retention policy will be applied to the latest version of the object.

* The object retention period can only be extended and cannot be shortened.


<span id="5e6eca89"></span>
## **Request syntax**

```JSON
PUT /objectname?retention HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string

{   
    "Mode": "COMPLIANCE",
    "RetainUntilDate": "2025-07-22T00:00:00Z"
}
```


<span id="477ffc71"></span>
## **Request parameters and headers**

The public message header used by this request. See [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |Required |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|retention |Query |String |Yes |\- |A special identifier representing a PutObjectRetention request. |
|versionId |Query |String |No |57AF1A32CECB56721267 |The version number of the object. |


<span id="05fa77cb"></span>
## **Request body elements**


|**Name** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Mode |String |Yes |COMPLIANCE |The retention policy mode only accepts `COMPLIANCE` as its value, which represents compliance mode. In this mode, no user can delete or overwrite locked objects during the retention period. |
|RetainUntilDate |String |Yes |2025\-01\-01T00:00:00Z |Retention period, used to specify the deadline by which an object cannot be deleted or overwritten. The time format is YYYY\-MM\-DDTHH:mm:ssZ. |


<span id="0d49277f"></span>
## **Response headers**

This request returns public response message headers.

<span id="6a40d2e4"></span>
## **Response body elements**

There is no message element in the response to this request.

<span id="67b8d4bd"></span>
## **Sample request**

```JSON
PUT /objectname?retention HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 13:59:18 GMT
Authorization: authorization string

{   
    "Mode": "COMPLIANCE",
    "RetainUntilDate": "2025-07-22T00:00:00Z"
}
```


<span id="2d7cba71"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444ed0        
x-tos-request-id: f91b0c03a01300c1-a444ed0            
Date: Fri, 30 Jul 2021 06:45:39 GMT
server: TosServer
Content-Length: 0
```
