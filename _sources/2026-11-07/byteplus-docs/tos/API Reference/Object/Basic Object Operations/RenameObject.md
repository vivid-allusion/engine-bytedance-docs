---
title: "RenameObject"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Renameobject"
---

<span id="f6aa0a05"></span>
## **Description**

Use the RenameObject interface to rename objects.

<span id="712f4d88"></span>
## Prerequisites

RenameObject functionality enabled. For specific operations, please refer to [Use RenameObject](https://docs.byteplus.com/docs/tos/Use-renameobject) or [PutBucketRename](https://docs.byteplus.com/docs/tos/Putbucketrename).

<span id="cbfd0f65"></span>
## **Precautions**


|**Category** |**Precautions** |
|---|---|
|Constraints and limitations |The RenameObject feature is mutually exclusive with the version control feature. If version control is enabled or paused on your bucket, the RenameObject feature cannot be used. |
|Renamed content |The RenameObject interface modifies the object's name and updates the object's modification time. |
|The renamed object |* The RenameObject feature is only supported for objects uploaded after its activation; it does not support objects uploaded before the feature was enabled. (Tiered buckets are not subject to this restriction).<br><br>* Archive ,Cold Archive,Deep Cold Archive storage type objects can only be renamed using the `RenameObject` feature after they have been restored. For detailed operations, please refer to [Restoring Files](https://docs.byteplus.com/docs/tos/docs-restoring-files).<br><br>* Concurrent renaming of the same object using the RenameObject feature is not supported.<br><br>* RenameObject supports renaming objects created by all types, including those created by Put, Multi\-Upload, Append, Copy, and Rename. After renaming, the Appendable object still retains the same ability to append as the original object. |


<span id="24b7f548"></span>
## **Request syntax**

```JSON
PUT /objectName?name=Name&rename HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="cfd21421"></span>
## **Request parameters and headers**

For common request headers, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|rename |Query |String |Yes |\- |Only the parameter name needs to be set, not the parameter value, representing the special identifier for the RenameObject request. |
|name |Query |String |Yes |dst\-object |Rename objects. |
|x\-tos\-forbid\-overwrite |Header |String |No |false |Whether to allow overwriting objects with the same name, value description as follows:<br><br><br>* `false`: Allow overwriting of objects with the same name.<br><br>* `true`: Prohibit overwriting of objects with the same name.<br><br><br>Defaults to `false`, which means overwriting objects with the same name is allowed by default. |
|x\-tos\-recursive\-mkdir |Header |String |No |true |This parameter is only for tiered buckets, value description as follows:<br><br><br>* `false`: If the parent directory of the target path does not exist, renaming the object is not allowed.<br><br>* `true`: If the parent directory of the target path does not exist, recursively create any non\-existent directory levels.<br><br><br>Defaults to `false`. |


<span id="bcf90e5b"></span>
## **Request body elements**

There are no request elements in this request message.

<span id="ca546fa2"></span>
## **Response headers**

This request returns the common response message headers, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="9926e80a"></span>
## **Response body elements**

There is no message element in this request response.

<span id="a28329ba"></span>
## **Sample request**

```JSON
PUT /src-object?name=dst-object&rename HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="d046aaa9"></span>
## **Sample response**

```JSON
HTTP/1.1 204 No Content
x-tos-id-2: 367be10900210004-a444ed0
x-tos-request-id: 367be10900210004-a444ed0
Date: Fri, 1 Jul 2022 01:00:36 GMT
Server: TosServer
```
