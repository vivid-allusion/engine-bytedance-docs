---
title: "ListBuckets"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-listbuckets"
---

<span id="5e05ed78"></span>
## **Description**

This API is used to query all buckets owned by the requesting user.

<span id="dc292f35"></span>
## **Request syntax**

```Plain
GET / HTTP/1.1
Host: tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="c81a40fd"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="38a75901"></span>
## **Request body elements**

No elements are used.

<span id="aa384b30"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="736fbfc5"></span>
## **Response body elements**

The response is a list of buckets owned by the user.


|**Name** |**Type** |**Description** |
|---|---|---|
|Buckets |Array |A list of buckets that you own. |
|Name |String |The bucket name. |
|CreationDate |String |The creation time of the bucket. |
|Location |String |The bucket region. |
|ExtranetEndpoint |String |The extranet endpoint. |
|IntranetEndpoint |String |The intranet endpoint. |
|Owner |Object |The bucket owner. |
|ID |String |The account ID. |


<span id="03081b55"></span>
## **Sample request**

```Plain
GET / HTTP/1.1
Host: tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 13:53:55 GMT
Authorization: authorization string
```


<span id="78d882e3"></span>
## **Sample response**

```Plain
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: 643

{
    "Buckets": [
        {
            "CreationDate": "2021-08-19T09:16:05.000Z",
            "Name": "buckettest001",
            "Location": "ap-southeast-1",
            "ExtranetEndpoint": "tos-ap-southeast-1.bytepluses.com",
            "IntranetEndpoint": "tos-ap-southeast-1.ibytepluses.com"
        },
        {
            "CreationDate": "2021-05-06T02:27:04.000Z",
            "Name": "lynch-peking-bucket",
            "Location": "ap-southeast-1",
            "ExtranetEndpoint": "tos-ap-southeast-1.bytepluses.com",
            "IntranetEndpoint": "tos-ap-southeast-1.ibytepluses.com"
        },
        {
            "CreationDate": "2021-08-19T03:58:02.000Z",
            "Name": "lynch-peking-bucket1",
            "Location": "ap-southeast-1",
            "ExtranetEndpoint": "tos-ap-southeast-1.bytepluses.com",
            "IntranetEndpoint": "tos-ap-southeast-1.ibytepluses.com"
        }
    ],
    "Owner": {
        "ID": "AccountID"
    }
}
```
