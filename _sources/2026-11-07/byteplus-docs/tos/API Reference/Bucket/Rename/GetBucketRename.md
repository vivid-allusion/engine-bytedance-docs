---
title: "GetBucketRename"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Getbucketrename"
---

<span id="45e0b5ee"></span>
## Description

Call the GetBucketRename interface to check if the bucket has the RenameObject feature enabled.

<span id="c679900e"></span>
## **Request syntax**

```JSON
GET /?rename HTTP/1.1 
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="188318e2"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|rename |Query |String |Yes |\- |Only the parameter name needs to be set, not the parameter value, representing the special identifier for the GetBucketRename request. |


<span id="dcbc055e"></span>
## **Request body elements**

This request does not use message elements.

<span id="b75ebe2f"></span>
## **Response headers**

This request returns the common response message headers. For common response headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="ce9eb8e8"></span>
## **Response body elements**


|**Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|RenameEnable |Bool |Yes |The bucket has the RenameObject feature enabled. The values are as follows:<br><br><br>* `true`: This bucket has the RenameObject feature enabled.<br><br>* `false`: This bucket does not have the RenameObject feature enabled. |


<span id="6a0e12b0"></span>
## **Sample request**

```JSON
GET /?rename HTTP/1.1 
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="452348e1"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
Date: Sat, 07 Oct 2023 09:02:23 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: ContentLength

{ 
    "RenameEnable":true
}
```
