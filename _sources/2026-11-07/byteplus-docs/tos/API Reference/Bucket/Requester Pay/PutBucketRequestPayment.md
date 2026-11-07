---
title: "PutBucketRequestPayment"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutBucketRequestPayment"
---

## Description

This interface sets the bucket's payment mode.

## Request syntax

```JSON
PUT /?requestPayment HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string 
{
    "Payer": "Requester"
}
```

## Request parameters and headers

This request uses common request headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|requestPayment |Query |String |Yes |\- |Represents the special identifier for PutBucketRequestPayment requests. |

## Request body elements

|**Name** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Payer |String |Yes |Requester |Payment modes for the specified bucket are explained as follows:<br><br><br>* `BucketOwner`: Owner\-paid mode, where the bucket owner covers all charges.<br><br>* `Requester`: Requester\-paid mode, where the requester pays for traffic and request fees during access while the bucket owner pays only for storage and other fees. For details, see [Fee Details](https://docs.byteplus.com/en/docs/tos/Using-requester-pays#fee-description). |

## Response headers

This request returns common response headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

## Response body elements

No elements are used in this response.

## Sample request

```JSON
PUT /?requestPayment HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string 
{
    "Payer": "Requester"
}
```

## Sample response

```JSON
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444ed0        
x-tos-request-id: f91b0c03a01300c1-a444ed0            
Date: Thu, 19 Jun 2025 07:25:27 GMT
server: TosServer
Content-Length: 0
```
