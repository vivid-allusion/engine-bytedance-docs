---
title: "Which Operations will Update the LastAccessTime of an Object?"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Which-operations-update-the-lastaccesstime"
---

LastAccessTime represents the last access time of an object, and some operations on an object may update the object's LastAccessTime.

The following table enumerates the LastAccessTime operations that update objects.


|**Specific operation** |**Involved interface** |
|---|---|
|Upload or overwrite objects |* [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject)<br><br>* [PostObject](https://docs.byteplus.com/docs/tos/reference-postobject)<br><br>* [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload)<br><br>* [FetchObject](https://docs.byteplus.com/docs/tos/Fetchobject)<br><br>* [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject) |
|Download object |[GetObject](https://docs.byteplus.com/docs/tos/reference--getobject) |
|Modify object ACL |[CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject) |
|Modify the object storage type |[CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject) |
