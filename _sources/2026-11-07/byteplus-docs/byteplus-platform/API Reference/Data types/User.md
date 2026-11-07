---
title: "User"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-user"
---

This data type includes information about IAM users. It is used as a response element in the following methods:


* [CreateUser](https://docs.byteplus.com/byteplus-platform/reference/createuser)

* [GetUser](https://docs.byteplus.com/byteplus-platform/reference/getuser)

* [UpdateUser](https://docs.byteplus.com/byteplus-platform/reference/updateuser)

* [ListUsers](https://docs.byteplus.com/byteplus-platform/reference/listusers)


<span id="0913c50e"></span>
## Structure


|**Parameter** |**Type** |**Description** |
|---|---|---|
|Trn |String |The resource name of the user. For example, `trn:iam::user/anyuser`. |
|CreateDate |String |The time when the user was created. For example, `20150123T123318Z`. |
|UpdateDate |String |The time when the user was updated. For example, `20150123T123318Z`. |
|UserName |String |Username. |
|DisplayName |String |User's display name. |
|MobilePhone |String |User's phone number. |
|MobilePhoneIsVerify |Boolean |Whether the phone number has been verified:<br><br><br>* `true`: verified<br><br>* 'false`: not verified \| |
|Email |String |User's email. |
|EmailIsVerify |Boolean |Whether the email has been verified:<br><br><br>* `true`: verified<br><br>* 'false`: not verified \| |
|Description |String |User description. |
