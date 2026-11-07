---
title: "PutBucketPolicy"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-putbucketpolicy"
---

<span id="7773386c"></span>
## **Description**

This API is used to modify or create a bucket policy. Calling this API overwrites the existing bucket policy.

<span id="6499c3ac"></span>
## Note


* The number of bucket policies is unlimited, but the JSON\-serialized policy text for a single bucket must not exceed 20 KB in size.

* This API must be called by the bucket owner or subaccounts of the bucket owner with the PutBucketPolicy permission for the bucket. For detailed instructions on how to achieve access control using bucket policies, see [Bucket Authorization Policy Management](https://docs.byteplus.com/en/tos/docs/overview_5).


<span id="e68e2431"></span>
## **Request syntax**

```JSON
PUT /?policy HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
{
    "Version": "2012-10-17",
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


<span id="a8aaeece"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|policy |Query |String |Yes |\- |Identifies a PutBucketPolicy request. |


<span id="e7bc3710"></span>
## **Request body elements**

The request body should be a JSON string containing the desired bucket policy. For more information, see [Bucket Policy Templates and Parameters](https://docs.byteplus.com/en/tos/docs/templates-and-parameters).

<span id="ffc2518d"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="6090f325"></span>
## **Response body elements**

No elements are used.

<span id="676217cb"></span>
## **Sample request 1**

**Granting permission to a TOS account**

This sample request grants bucket read\-only permission to account "210004xxxx".

```JSON
PUT /?policy HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Bucket Read-Only",
            "Effect": "Allow",
            "Principal": [
                "210004xxxx"
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


<span id="a23f7105"></span>
## **Sample response 1**

```JSON
HTTP/1.1 204 No Content
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
```


<span id="2a53334a"></span>
## **Sample request 2**

**Granting permission to an IAM user under a TOS account**

This sample request grants bucket read\-only permission to the IAM user "testuser" under account "210004xxxx".

```JSON
PUT /?policy HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
{
    "Version": "2012-10-17",
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


<span id="577fa0a4"></span>
## **Sample response 2**

```JSON
HTTP/1.1 204 No Content
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
```
