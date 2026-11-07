---
title: "GetBucketPolicy"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-getbucketpolicy"
---

<span id="3423aa7c"></span>
## **Description**

This API is used to get the bucket policy of a specified bucket.

<span id="c201dae4"></span>
## Note


* This API must be called by the bucket owner or subaccounts of the bucket owner with the GetBucketPolicy permission for the bucket. For detailed instructions on how to achieve access control using bucket policies, see [Bucket authorization policy management](https://docs.byteplus.com/en/tos/docs/overview_5).

* If the specified bucket policy does not exist and this API is called to get the bucket policy, the server returns the `404 NoSuchBucketPolicy` error.


<span id="e8546e90"></span>
## **Request syntax**

```JSON
Get /?policy HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="ed96ca1a"></span>
## **Request parameters and headers**

For common request headers, see [Common parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|policy |Query |String |Yes |\- |Identifies a GetBucketPolicy request. |


<span id="d8716a55"></span>
## **Request body elements**

No elements are used.

<span id="1436f9b6"></span>
## **Response headers**

For common response headers, see [Common parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="ec9f0516"></span>
## **Response body elements**

The response body should be a JSON string containing the desired bucket policy. For more information, see [Bucket policy templates and parameters](https://docs.byteplus.com/en/tos/docs/templates-and-parameters).

<span id="bd4214a7"></span>
## **Sample request**

```JSON
GET /?policy HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="8673c60b"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: 212
{
    "Version": "1.0",
    "Statement": [
        {
            "Sid": "Bucket Read-Only",
            "Effect": "Allow",
            "Principal": [
                "210004xxxx/testuser"
            ],
            "Action": [
                "tos:Get*",
                "tos:List*"
            ],
            "Resource": [
                "trn:tos:::bucketname",
                "trn:tos:::bucketname/*"
            ]
        }
    ]
}
```
