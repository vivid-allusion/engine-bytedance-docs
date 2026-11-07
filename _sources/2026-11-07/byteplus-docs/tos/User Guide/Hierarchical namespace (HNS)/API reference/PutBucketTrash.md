---
title: "PutBucketTrash"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutBucketTrash"
---

<span id="b07e3974"></span>
## Description

This interface sets the recycle bin function for the hierarchical namespace. Once the recycle bin function is enabled, TOS moves deleted files and directories to the recycle bin directory specified by the rule. At the same time, TOS automatically deletes files and directories in the recycle bin according to the expiration time specified by the rule.

<span id="183046fe"></span>
## Instructions

Currently, this interface only supports use in hierarchical namespaces. For details, see [Recycle Bin](https://docs.byteplus.com/docs/tos/Recycle-bin).

<span id="xwfUfrSf"></span>
## **Request syntax**

```JSON
PUT /?trash HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
Content-Length: ContentLength
Content-MD5: MD5
{
    "Trash": {
        "TrashPath": ".Trash",
        "CleanInterval": 7,
        "Status": "Enabled"
    }
}
```


<span id="dddc4bac"></span>
## **Request parameters and headers**

This request uses common request headers. See [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|trash |Query |String |Yes |\- |Indicates the special identifier for the PutBucketTrash request. |


<span id="8cdfd0aa"></span>
## **Request body elements**


|**name** |**Type** |Required |Sample Value |**Description** |
|---|---|---|---|---|
|BucketTrash |Container |Yes |\- |Recycle bin rule information. |
|TrashPath |String |Yes |.Trash |Recycle bin directory. |
|CleanInterval |Integer |Yes |7 |The number of days after which files or directories are permanently deleted from the recycle bin; must be a positive integer. |
|Status |String |yes |Enabled |set whether the recycle bin is enabled; the values are as follows:<br><br><br>* `Enabled`: enables the recycle bin feature.<br><br>* `Disabled`: disables the recycle bin feature. |


<span id="5bd278ae"></span>
## **Response headers**

This request returns common response headers. See [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="d9f3ab87"></span>
## **Response body elements**

No elements are used in this response.

<span id="baaf3bc8"></span>
## **Sample request**

<span id="57c4b33f"></span>
### **Sample request 1**

Enable the recycle bin function. The recycle bin path is `.Trash` in the root directory, and the expiration delete time is 7 days.

```JSON
PUT /?trash HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
Content-Length: ContentLength
Content-MD5: MD5
{
    "Trash": {
        "TrashPath": ".Trash",
        "CleanInterval": 7,
        "Status": "Enabled"
    }
}
```


<span id="8bf8fcc3"></span>
### **Sample response 1**

None.

<span id="e652787e"></span>
### **Sample request 2**

Disable recycle bin feature.

```JSON
PUT /?trash HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
Content-Length: ContentLength
Content-MD5: MD5
{
    "Trash": {
        "TrashPath": ".Trash",
        "CleanInterval": 7,
        "Status": "Disabled"
    }
}
```


<span id="370dff0b"></span>
### **Sample response 2**

None.
