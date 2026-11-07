---
title: "Which operations update an object's LastModifyTime?"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Which-operations-update-the-lastmodifytime"
---

LastModifyTime indicates the last modification time of the object. Some operations on the object may update its LastModifyTime.

The following table lists operations that update an object's LastModifyTime.


|**Specific operations** |**Related interfaces** |
|---|---|
|Rename directories or files |[RenameObject](https://docs.byteplus.com/docs/tos/Renameobject)<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">HNS buckets support renaming directories or files through the RenameObject interface by default. FNS buckets require enabling the RenameObject feature first to support renaming files via the RenameObject interface, but do not support renaming directories.</div><br> |
|Append to file |[ModifyObject](https://docs.byteplus.com/docs/tos/Modifyobject)<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only HNS buckets support the ModifyObject interface.</div><br> |
|Overwrite files with the same name |Upload files with the same name via [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject) |
||Copy files with the same name through [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject) |


&nbsp;
