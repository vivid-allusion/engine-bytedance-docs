---
title: "GetBucketLocation"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-getbucketlocation"
---

<span id="b2db2af9"></span>
## **Description**

This API is used to query the region information of the bucket.

<span id="1d7b2185"></span>
## **Request syntax**

```JSON
GET /?location HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="9ba528ef"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="2a00e4d0"></span>
## **Request body elements**

No elements are used.

<span id="5e4fdb73"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="a7c7ff95"></span>
## **Response body elements**


|**Name** |**Type** |**Description** |
|---|---|---|
|Region |String |The bucket region. |
|ExtranetEndpoint |String |The extranet endpoint. |
|IntranetEndpoint |String |The intranet endpoint. |


<span id="2159e83c"></span>
## **Sample request**

```JSON
GET /?location HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 13:53:55 GMT
Authorization: authorization string
```


<span id="86d56e72"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: 643

{
    "Region": "ap-southeast-1",
    "ExtranetEndpoint": "tos-ap-southeast-1.bytepluses.com",
    "IntranetEndpoint": "tos-ap-southeast-1.ibytepluses.com"
}
```
