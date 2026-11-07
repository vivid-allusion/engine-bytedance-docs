---
title: "PutBucketRename"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Putbucketrename"
---

<span id="b4b92df9"></span>
## **Description**

Call the `PutBucketRename` API to enable the `RenameObject` feature for the bucket. Once enabled, you can use the `RenameObject` API to rename objects.

<span id="bb38ce5a"></span>
## Precautions

Using the PutBucketRename interface to enable the RenameObject feature is mutually exclusive with the version control feature. If your bucket has already enabled or paused the version control feature, the PutBucketRename interface cannot be used.

<span id="41158432"></span>
## **Request syntax**

```JSON
PUT /?rename HTTP/1.1 
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
Content-Length: ContentLength

{ 
    "RenameEnable":true
}
```


<span id="e4ca8c4c"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|rename |Query |String |Yes |\- |Only need to set the parameter name, no need to set the parameter value, representing a special identifier for the PutBucketRename request. |


<span id="6521100d"></span>
## **Request body elements**


|**Name** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|RenameEnable |Bool |Yes |true |Should the RenameObject feature be enabled, set to `true` to enable it.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you want to disable the RenameObject feature, you can use the DeleteBucketRename interface. For more details, please refer to <a href="https://docs.byteplus.com/en/docs/tos/Deletebucketrename">DeleteBucketRename</a>.</div><br> |


<span id="dc0b3ba3"></span>
## **Response headers**

This request returns the common response message headers. For common response headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="2f6af7e7"></span>
## **Response body elements**

There is no message element in this request response.

<span id="9017162e"></span>
## **Sample request**

```JSON
PUT /?rename HTTP/1.1 
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
Content-Length: ContentLength

{ 
    "RenameEnable":true
}
```


<span id="c930c58c"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
Date: Sat, 07 Oct 2023 09:02:23 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: 0
```
