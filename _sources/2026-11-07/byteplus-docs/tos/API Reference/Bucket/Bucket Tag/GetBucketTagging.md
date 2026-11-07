---
title: "GetBucketTagging"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Getbuckettagging"
---

<span id="5f5d2e50"></span>
## Description

This interface is used to obtain the tagging information of a specified bucket.

<span id="6ab04577"></span>
## Precautions

Only the owner of the bucket and users with GetBucketTagging permission can retrieve bucket tags.

<span id="8fb95d0f"></span>
## **Request syntax**

```JSON
GET /?tagging HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="b3e86376"></span>
## **Request parameters and headers**

For common request headers, see [Common parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|tagging |Query |String |Yes |\- |Represents the special identifier of the GetBucketTagging request. |


<span id="c3d5775d"></span>
## **Request body elements**

This request does not use message elements.

<span id="89e2e2c8"></span>
## **Response headers**

The response includes a common response message header, please see [Common parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="7ecc5a81"></span>
## **Response body elements**


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|TagSet |Object |Yes |\- |Bucket tag set information. |
|Tags |Array |Yes |\- |Bucket tag list information. |
|Key |String |Yes |owner |The value of the tag Key. For specific setting rules, please refer to [Setting bucket tags](https://docs.byteplus.com/docs/tos/Set-bucket-tag). |
|Value |String |Yes |zhangsan |Value of the label. For specific setting rules, please see [Setting bucket tags](https://docs.byteplus.com/docs/tos/Set-bucket-tag). |


<span id="a61caddb"></span>
## **Request example**

```JSON
GET /?tagging HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="fbc5b8e9"></span>
## Response example

```JSON
HTTP/1.1 200 OK
Date: Sat, 07 Oct 2023 09:02:23 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: 262

{
        "TagSet": {
                "Tags": [{
                        "Key": "key1",
                        "Value": "value1"
                }, {
                        "Key": "key2",
                        "Value": "value2"
                }]
        }
}
```
