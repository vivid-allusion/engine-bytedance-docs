---
title: "GetBucketTrash"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetBucketTrash"
---

<span id="b07e3974"></span>
## Description

This interface is used to retrieve the Recycle Bin rules for hierarchical namespaces.

<span id="183046fe"></span>
## Usage

This interface currently only supports hierarchical namespaces. For details, see [Recycle Bin](https://docs.byteplus.com/docs/tos/Recycle-bin).

<span id="MDn5n5qK"></span>
## Request syntax

```JSON
GET /?trash HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="dddc4bac"></span>
## Request parameters and headers

This request uses common request headers. See [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|trash |Query |String |Yes |\- |Represents a special identifier for the GetBucketTrash request. |


<span id="8cdfd0aa"></span>
## Request body elements

No elements are used.

<span id="5bd278ae"></span>
## Response headers

The common response headers returned by this request. See [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="d9f3ab87"></span>
## Response body elements


|**Name** |**Type** |Required |Sample value |**Description** |
|---|---|---|---|---|
|BucketTrash |Container |Yes |\- |Recycle Bin rule information. |
|TrashPath |String |Yes |.Trash |Full path of the Recycle Bin. |
|CleanInterval |Integer |Yes |7 |The number of days after a file or directory moves to the Recycle Bin before it is permanently deleted. Must be a positive integer. |
|Status |String |Yes |Enabled |Set whether Recycle Bin is enabled. The values are explained as follows:<br><br><br>* `Enabled`: Enables the Recycle Bin function.<br><br>* `Disabled`: Disables the **recycle bin** function. |


<span id="baaf3bc8"></span>
## Sample request

```JSON
GET /?trash HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Mon, 14 Apr 2021 01:17:29 GMT  
Authorization: authorization string
```


<span id="f2a7d445"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: ***
{
    "Trash": {
        "TrashPath": ".Trash",
        "CleanInterval": 7,
        "Status": "Enabled"
    }
}
```


If no recycle bin rules are set, the default rule is returned, as shown in the example below.

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: ***
{
    "Trash": {
        "TrashPath": ".Trash",
        "CleanInterval": 7,
        "Status": "Disabled"
    }
}
```
