---
title: "ListAccessPoints"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/ListAccessPoints"
---

<span id="eaa6702f"></span>
## Description

The `ListAccessPoints` interface lists the access points under your account that meet the criteria. You can list all access points without any parameters, or specify a bucket name to filter access points linked to that bucket.

<span id="0b8d07de"></span>
## Request syntax

```HTTP
GET /accesspoint?bucket={BucketName}&maxResult={MaxResult}&nextToken={NextToken} HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: GMT Date
Authorization: authorization string
x-tos-account-id: AccountId
```


<span id="2409ea73"></span>
## Request parameters and headers 

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/docs/tos/reference-common-parameters).


|Field name | Location |Type |Required |Example value |Description |
|---|---|---|---|---|---|
|bucket |Query |String |No |bkt01 |Used to filter and specify access points associated with the bucket. If this parameter is provided, the response only returns the list of access points that belong to the bucket. |
|maxResult |Query |Integer |No |100 |Set the maximum number of access points returned per request. The default and maximum value is 1000. |
|nextToken |Query |String |No |token1 |When the previous access point listing result is truncated, TOS returns the `NextToken` field. You can include this field's value in the next request to retrieve the remaining results. |
|x\-tos\-account\-id |Header |String |Yes |200\*\*\*\*\*\*\*\* |Your BytePlus account ID. |


<span id="a8029ecd"></span>
## Request body elements

No elements are used.

<span id="5b1d8827"></span>
## Response headers

The response contains common headers. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/tos/reference-common-parameters).

<span id="c4c11aab"></span>
## Response body elements


|Field name |Type |Example value |Description |
|---|---|---|---|
|IsTruncated |Boolean |true |Indicates whether the returned result is truncated:<br><br><br>* `true`: indicates that there are still partial results not returned.<br><br>* `false`: indicates that all results have been returned. |
|NextToken |String |token |This field appears only when `IsTruncated` is `true`. Its value can be used as the `nextToken` parameter in the next request to retrieve the next page of results. |
|AccessPoints |Array |\- |List of access points. |
| Name |String |ap\-test |Access Point Name.<br><br>Parent node: `AccessPoints`. |
|Alias |String |ap\-test\-\*\*\*\*\*\*\*\* |Access point alias.<br><br>Parent node: `AccessPoints`. |
|Bucket |String |bkt01 |Name of the bucket associated with the access point.<br><br>Parent node: `AccessPoints`. |
|BucketAccountId |String |200\*\*\*\*\*\*\*\* |The account ID that owns the bucket.<br><br>Parent node: `AccessPoints`. |
|AccessPointType |String |Regular |Access point type. The fixed value is `Regular`.<br><br>Parent node: `AccessPoints`. |
|Status |String |enable |Access point status.<br><br>Parent node: `AccessPoints`. |
|NetworkOrigin |String |internet |Allowed network sources.<br><br>Parent node: `AccessPoints`. |
|AccessPointTrn |String |trn:tos:\*\*\*\*\*\*\*\* |TRN of the access point.<br><br>Parent node: `AccessPoints`. |
|Endpoints |Object |\- |The set of domain names for accessing the access point. |
|ExtranetEndpoint |String |ap\-test\-200\*\*\*\*\*\*\*\*tos\-accesspoint.cn\-beijing.volces.com |The extranet endpoint.<br><br>Parent node: `Endpoints`. |
|IntranetEndpoint |String |ap\-test\-200\*\*\*\*\*\*\*\*tos\-accesspoint.cn\-beijing.ivolces.com |VPC network access domain name.<br><br>Parent node: `Endpoints`. |


<span id="ee065025"></span>
## Sample request

```HTTP
GET /accesspoint?bucket=bkt01&maxResult=100&nextToken=token1 HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 06:45:39 GMT
Authorization: TOS4-HMAC-SHA256 Credential=AKLT**********/20210730/cn-beijing/tos/request, SignedHeaders=host;x-tos-account-id;x-tos-date, Signature=...
x-tos-account-id: 200********
```


<span id="1faf124a"></span>
## Sample response

```JSON
{
    "IsTruncated": true,
    "NextToken": "token",
    "AccessPoints": [
        {
            "Name": "ap-test",
            "Alias": "ap-test-5007a2f0bcb595f63e2215cxxxx-tosalias",
            "Bucket": "bkt01",
            "BucketAccountId": "200********",
            "AccessPointType": "Regular",
            "Status": "enable",
            "NetworkOrigin": "internet",
            "AccessPointTrn": "trn:tos:cn-beijing:200********:accesspoint/ap-test",
            "Endpoints": {
                "IntranetEndpoint": "ap-test-5007a2f0bcb595f63e2215c****-tosalias.cn-beijing.ivolces.com",
                "ExtranetEndpoint": "ap-test-5007a2f0bcb595f63e2215c****-tosalias.cn-beijing.volces.com"
    }
        },
        {
            "Name": "ap-test-2",
            "Alias": "ap-test-2-5007a2f0bcb595f63e2215cxxxx-tosalias",
            "Bucket": "bkt01",
            "BucketAccountId": "200********",
            "AccessPointType": "Regular",
            "Status": "enable",
            "NetworkOrigin": "internet",
            "AccessPointTrn": "trn:tos:cn-beijing:200********:accesspoint/ap-test-2",
            "Endpoints": {
                "IntranetEndpoint": "ap-test-2-5007a2f0bcb595f63e2215c****-tosalias.cn-beijing.ivolces.com",
                "ExtranetEndpoint": "ap-test-2-5007a2f0bcb595f63e2215c****-tosalias.cn-beijing.volces.com"
    }
        }
    ]
}
```
