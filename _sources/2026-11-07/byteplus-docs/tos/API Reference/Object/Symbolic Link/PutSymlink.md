---
title: "PutSymlink"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Putsymlink"
---

<span id="c76b46e7"></span>
## **Introduction**

Use the PutSymlink interface to create a symbolic link for an existing object in TOS, allowing quick access to the object.

<span id="5b75a6fe"></span>
## Precautions


* The PutSymlink interface charges for request numbers based on the storage type of the symbolic link object. For details, see [Requests](https://docs.byteplus.com/docs/tos/docs-request-fee).

* When creating a soft link using the PutSymlink API, the existence of the target object and access permissions to it are not checked. However, when calling the [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject), [HeadObject](https://docs.byteplus.com/docs/tos/reference-headobject), and other APIs to retrieve soft link information, the system will check whether the account has read permissions for both the soft link and the target object, as well as whether the target object exists.

* Symbolic links and target objects support being in different storage buckets within the same region but do not support being in storage buckets in different regions.

* Secondary symbolic links are not supported. You can use the PutSymlink interface to create secondary links, but you cannot access the target object through the secondary soft link.


For more precautions about the PutSymlink interface, please see [Create symbolic link](https://docs.byteplus.com/docs/tos/Create-Symbolic-link).

<span id="b9b19cbf"></span>
## **Request syntax**

```JSON
PUT /ObjectName?symlink HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Wed, 29 May 2024 08:37:23 GMT
Authorization: authorization string
x-tos-symlink-target: TargetObjectName
x-tos-symlink-bucket: TargetBucketName
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the request message style, <code>ObjectName</code> is used to specify the name of the soft link, while <code>Host</code>'s <code>bucketname</code> is used to specify the bucket name where the soft link is stored.</div>


<span id="0a858d10"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|symlink |Query |String |Yes |\- |Represents the special identifier for the PutSymlink request. |
|x\-tos\-symlink\-target |Header |String |Yes |test\-object |The target object name pointed by the symbolic link.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The target object name needs to be URL encoded, adhering to the <code>application/x-www-form-urlencoded</code> standard.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The target object pointed to by the symbolic link cannot be another symbolic link.</div><br> |
|x\-tos\-symlink\-bucket |Header |String |No |test\-bucket |If not set, it indicates that the symbolic link and its target object are in the same bucket. |
|x\-tos\-forbid\-overwrite |Header |String |No |false |If there is an object with the same name in the bucket, whether a soft link is allowed to overwrite that object, the values are explained as follows:<br><br><br>* `true`: Do not overwrite objects with the same name.<br><br>* `false`: Allow overwriting objects with the same name.<br><br><br>Default is `false`, which means if the parameter `x-tos-forbid-overwrite` is not set, it allows overwriting objects with the same name.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the bucket containing the symbolic link is in a state of enabled or suspended version control, the <code>x-tos-forbid-overwrite</code> parameter is ineffective, allowing overwriting of objects with the same name.</div><br> |
|x\-tos\-acl |Header |String |No |private |Access permissions for soft links; valid settings include:<br><br><br>* `Private`: Private<br><br>* `Public-read`: Public read.<br><br>* `Public-read-write`: Public read\-write.<br><br>* `Authenticated-read`: Authenticated user read.<br><br>* `Bucket-owner-read`: Bucket owner read.<br><br>* `bucket-owner-full-control`: Bucket owner full control.<br><br>* `bucket-owner-entrusted`: Controlled by the bucket policy, the bucket owner has full permissions.<br><br>* `default`: Inherits the bucket ACL, meaning the object’s ACL policy is consistent with the bucket ACL policy.<br><br><br>Defaults to `private`. |
|x\-tos\-storage\-class |Header |String |No |STANDARD |The storage type for symbolic links is defined as follows:<br><br><br>* `STANDARD`: Standard Storage.<br><br>* `IA`: Infrequent Access Storage.<br><br>* `INTELLIGENT_TIERING`: Intelligent Tiering.<br><br>* `ARCHIVE_FR`: Flashback Archive.<br><br>* `ARCHIVE`: Archive.<br><br>* `COLD_ARCHIVE`: Cold Archive.<br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive.<br><br><br>If not set, it will default to the storage type of the bucket it is in.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Storage types like Infrequent Access Storage, Flashback Archive and Archive are subject to minimum quantification limits. Objects smaller than 64 KiB will be charged based on a minimum of 64 KiB for storage capacity. If the storage capacity of a symbolic link object is less than 64 KiB, to avoid unnecessary costs, it is advisable to set the storage type of the symbolic link object to standard storage.</div><br> |
|x\-tos\-tagging |Header |String |No |Key1=Value1&Key2=Value |The object tag information for a symbolic link, formatted as `{Key}={Value}`, supports setting multiple tags simultaneously. Use `&` to separate multiple tags.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The key and value of an object tag need to be URL encoded, following the application/x\-www\-form\-urlencoded standard.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If a tag does not use <code>=</code> to set its value, TOS will consider the value of the tag to be an empty string.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For more information on restrictions regarding object tags, please refer to <a href="https://docs.byteplus.com/docs/tos/docs-managing-file-labels">Managing file tags</a>.</div><br> |
|x\-tos\-meta\-\* |Header |String |No |x\-tos\-meta\-key:value |Custom metadata for soft links. |


<span id="1b2f8e10"></span>
## **Request body elements**

There is no message element in this request.

<span id="42a81062"></span>
## **Response headers**

This request returns the common response message headers. For common response headers, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|x\-tos\-version\-id |String |5840E600C6FBD446792D |Version number of the soft link. If no version number exists, this header will not appear in the response message. |


<span id="4784c8ae"></span>
## **Response body elements**

There is no message element in this request response.

<span id="1f064c4f"></span>
## **Sample request**

```JSON
PUT /link-to-abc?symlink HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Wed, 29 May 2024 08:37:23 GMT
Authorization: authorization string
x-tos-symlink-target: abc
x-tos-symlink-bucket: target-bucket
```


<span id="a6a43f90"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
Date: Wed, 29 May 2024 08:41:23 GMT
Server: TosServer
Content-Length: 0
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a443223
Etag: "47bce5c74f589f4867dbd57e9****"
```
