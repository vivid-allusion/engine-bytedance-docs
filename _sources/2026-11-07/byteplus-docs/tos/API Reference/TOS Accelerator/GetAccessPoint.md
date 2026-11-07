---
title: "GetAccessPoint"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetAccessPoint"
---

<span id="8b5f7d7c"></span>
## Description

`CreateAccessPoint` interface creates an access point for the specified bucket. Each access point associates with a specific bucket and provides a unique domain name to access the data in that bucket. You can configure network sources and independent access control policies for different access points.

<span id="5a7249fb"></span>
## Request syntax

```JSON
PUT /accesspoint/{AccessPointName} HTTP/1.1
Host:{BucketName}.tos-cn-beijing.volces.com
Date: GMT Date
Authorization: authorization string
x-tos-account-id: AccountId

{
    "Bucket": "string",
    "BucketAccountId": "string",
    "NetworkOrigin": "string",
    "VpcId": "string"
}
```


<span id="c08062c0"></span>
## Request parameters and headers 

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/docs/tos/reference-common-parameters).


|Field name | Location |Type |Required |Example value |Description |
|---|---|---|---|---|---|
|AccessPointName |Path |String |Yes |ap\-test |Name of the access point. Must be unique within the same account and region. |
|x\-tos\-account\-id |Header |String |Yes |200\*\*\*\*\*\*\*\* |Your BytePlus account ID. |


<span id="e55e0cc5"></span>
## Request body elements


|Field name | Location |Type |Required |Example value |Description |
|---|---|---|---|---|---|
|Bucket |Body |String |Yes |bkt01 |Name of the bucket associated with the access point. You can specify buckets outside this account. |
|BucketAccountId |Body |String |No |200\*\*\*\*\*\*\*\*\* |The account ID of the target bucket. This parameter is optional if accessing a bucket under the current account name. |
|NetworkOrigin |Body |String |Yes |internet |Network sources allowed to access this endpoint. The options are as follows:<br><br><br>* `internet`: allows access from the internet and VPC networks.<br><br>* `vpc`: only allows access from specified VPC networks. |
|VpcId |Body |String |No |vpc\-\*\*\*\*\*\*\*\* |Specify the VPC network ID allowed for access.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when the <code>NetworkOrigin</code> parameter value is <code>vpc</code>.</div><br> |


<span id="65003361"></span>
## Response headers

The response contains common headers. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/tos/reference-common-parameters).

<span id="1dc037c3"></span>
## Response body elements


|**Field name** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|AccessPointTrn |String |trn:tos:cn\-beijing:200\*\*\*\*\*\*\*\*accesspoint/ap\-test |Unique resource identifier of the access point. |
|Alias |String |ap\-test\-5007a2f0bcb595f63e2215c\*\*\*\*\-tosalias |Alias of the access point. When creating an access point, TOS automatically generates a globally unique alias for it. |


<span id="acd6104f"></span>
## Sample request

```JSON
PUT /accesspoint/ap-test HTTP/1.1
Host:{BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 06:45:39 GMT
Authorization: TOS4-HMAC-SHA256 Credential=AKLT**********/20210730/cn-beijing/tos/request, SignedHeaders=host;x-tos-account-id;x-tos-date, Signature=...
x-tos-account-id: 200********
Content-Type: application/json; charset=utf-8
Content-Length: 77

{
    "Bucket": "bkt01",
    "NetworkOrigin": "internet"
}
```


<span id="8a4d2f88"></span>
## Sample response

```JSON
{
    "AccessPointTrn": "trn:tos:cn-beijing:200********:accesspoint/ap-test",
    "Alias": "ap-test-5007a2f0bcb595f63e2215c****-tosalias"
}
```
