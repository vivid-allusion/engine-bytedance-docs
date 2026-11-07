---
title: "AccessKeyMeta"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-accesskeymeta"
---

This data type includes the metadata of AccessKey but does not include the information about the secret AccessKey. It is used as a response element in method [ListAccessKeys](https://docs.byteplus.com/byteplus-platform/reference/listaccesskeys).

<span id="3b494bfa"></span>
## Structure


|**Parameter** |**Type** |**Length (character)**  |**Format** |**Description** |
|---|---|---|---|---|
|AccessKeyId |String |[20,32] |AKLT[a\-zA\-Z0\-9\-_]+ |AccessKey ID. |
|UserName |String |[1,64] |[\w+=,.@\-]+ |If the AccessKey belongs to an IAM user, the value of the field is the username; if the Accesskey belongs to the admin account, the field is empty. |
|CreateDate |DateTime |20 |20180801T210558Z<br><br>Conforms to the ISO8601 standard. |The time when the AccessKey was created. |
|UpdateDate |DateTime |20 |20180801T210558Z<br><br>Conform to the ISO8601 standard. |The time when the AccessKey was updated. |
|Status |String |6 or 8 |active/inactive |AccessKey status. Valid values are: `active` |
