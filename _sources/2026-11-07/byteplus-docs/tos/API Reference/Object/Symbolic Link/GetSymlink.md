---
title: "GetSymlink"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Getsymlink"
---

<span id="6d4172f3"></span>
## **Description**

Call the GetSymlink interface to obtain symlink object information.

<span id="ee6ad1de"></span>
## **Request syntax**

```JSON
GET /ObjectName?symlink HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: SignatureValue
```


<span id="a9e7fc9a"></span>
## **Request parameters and headers**

This request uses common request message headers, please see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Parameter Type** |**Is it mandatory?**  |**Example Value** |**Description** |
|---|---|---|---|---|---|
|symlink |Query |String |Is |\- |represents the special identifier for the GetSymlink request. |
|versionId |Query |String |No |5840E600C6FBD446792D |The version number of the soft link object. |


<span id="b2d12f22"></span>
## **Request body elements**

This request does not involve request message elements.

<span id="3fdbb188"></span>
## **Response headers**

The common response message headers returned by this request, please see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Parameter Type** |**Example Value** |**Description** |
|---|---|---|---|
|Last\-Modified |String |Thu, 06 Jun 2024 09:45:58 GMT |Last update time of the symbolic link. |
|x\-tos\-version\-id |String |5840E600C6FBD446792D |Version number of the symbolic link. If no version number exists, this header will not appear in the response message. |
|x\-tos\-symlink\-target |String |test\-object |Target file that the symbolic link points to. |
|x\-tos\-symlink\-bucket |String |test\-bucket |The target file pointed to by the symlink belongs to the bucket. |


<span id="4e01d364"></span>
## **Response body elements**

There is no message element in this request response.

<span id="0ce8a5c4"></span>
## **Sample request**

```JSON
GET /link-to-abc?symlink HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Wed, 29 May 2024 08:39:35 GMT
Authorization: authorization string
```


<span id="b7b13c56"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
Date: Wed, 29 May 2024 08:42:35 GMT
Server: TosServer
Content-Length: 0
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Etag: "47bce5c74f589f4867dbd57e9****"
Last-Modified: Wed, 03 Apr 2024 08:12:47 GMT
x-tos-symlink-target: test-object
x-tos-symlink-bucket: test-bucket
```
