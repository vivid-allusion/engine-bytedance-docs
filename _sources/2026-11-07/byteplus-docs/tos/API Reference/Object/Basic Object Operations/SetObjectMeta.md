---
title: "SetObjectMeta"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-setobjectmeta"
---

<span id="100e4971"></span>
## Introduction

This API is used to update the metadata of an uploaded object. TOS enables you to send specific request headers to modify object metadata. When you download the object or perform a HEAD request, these values are set in the HTTP headers and returned to the client. The supported headers are `Cache-Control`, `Content-Disposition`, `Content-Encoding`, `Expires`, `Content-Type`, and `Content-Language`.

This API replaces object metadata in its entirety, and any unspecified metadata fields will be cleared.

<span id="a09aa7d0"></span>
## **Request syntax**

```JSON
POST /ObjectName?metadata HTTP/1.1
Host:  bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
<Optional Additional Header>
```


<span id="1171519e"></span>
## **Request parameters and headers**

For common request headers, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|metadata |Query |String |Yes |\- |Identifies a SetObjectMeta request. |
|versionId |Query |String |No |57AF1A32CECB56721267 |Version ID of the object. Use this to update the metadata of a specific version of the object. |
|Content\-Type |Header |String |No |text/plain |Object content type. |
|Cache\-Control |Header |String |No |no\-cache, no\-store, must\-revalidate |Specifies the caching behavior when the object is downloaded. |
|Expires |Header |String |No |Mon, 04 Jul 2022 02:57:31 GMT |Specifies the cache expiration time as defined in RFC 2616. |
|Content\-Disposition |Header |String |No |attachment; filename=123.txt |Specifies the default filename of the object when downloaded. |
|Content\-Encoding |Header |String |No |gzip |Specifies the content encoding of the object when downloaded. |
|Content\-Language |Header |String |No |en\-US |Specifies the content language of the object when downloaded. |
|x\-tos\-meta\-\* |Header |String |No |x\-tos\-meta\-key: value |When creating an object, you can specify custom metadata through HTTP request headers prefixed with "x\-tos\-meta\-" to tailor object management. Your custom metadata will appear in the response headers when others retrieve this object or query the object metadata. |
|x\-tos\-object\-expires |Header |String |No |3 |Add expiration time to objects, or modify the expiration time of objects. After expiration, TOS will automatically delete the object. The expiration time is calculated from the Last\-Modified time of the object, in days.<br><br>After setting the expiration time for an object, TOS will start the deletion task at midnight after the expiration time is reached. For example, if the last modified time of an object is 2024\-09\-26 12:00, and the expiration time is 3 days, the object will expire at 2024\-09\-30 00:00.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The expiration time of an object takes priority over the deletion rule based on its lifecycle. For example, if an object is set to expire in 5 days and a lifecycle rule specifies that the object should be deleted after 3 days, the expiration time will take precedence. Therefore, the object will be deleted after 5 days according to its expiration time.</div><br> |


<span id="29cb2cee"></span>
## **Request body elements**

No elements are used.

<span id="1087fe13"></span>
## **Response headers**

For common response headers, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="f7250c2d"></span>
## **Response body elements**

No elements are used.

<span id="6a6db83b"></span>
## **Sample request 1**

This request adds the following metadata to the object: `Content-Type: application/x-www-form-urlencoded` and `x-tos-meta-test: meta-test`.

```JSON
POST /ObjectName?metadata HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 GMT
Authorization: authorization string
Content-Type: application/x-www-form-urlencoded
x-tos-meta-test: meta-test
```


<span id="afe86c3a"></span>
## **Sample response 1**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444ed0
x-tos-request-id: f91b0c03a01300c1-a444ed0
Date: Fri, 30 Jul 2021 08:05:36 GMT
server: TosServer
Content-Length: 0
```


<span id="f26d69d9"></span>
## **Sample request 2**

This request updates the `x-tos-meta-test: meta_test` metadata of the object with a value `meta_modify` while leaving another existing entry `Content-Type: application/x-www-form-urlencoded` as is.

```JSON
POST /ObjectName?metadata HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 GMT
Authorization: authorization string
Content-Type: application/x-www-form-urlencoded
x-tos-meta-test: meta_modify
```


<span id="0c2fcbdc"></span>
## **Sample response 2**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: 92ab6a0bb2ff0006-a444ed0
x-tos-request-id: 92ab6a0bb2ff0006-a444ed0
Date: Fri, 30 Jul 2021 08:05:36 GMT
server: TosServer
Content-Length: 0
```
