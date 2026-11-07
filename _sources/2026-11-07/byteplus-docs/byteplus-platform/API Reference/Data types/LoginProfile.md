---
title: "LoginProfile"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-loginprofile"
---

This data type includes the information about the console login configuration for an IAM user. It is used as a response element in the following methods:


* [CreateLoginProfile](https://docs.byteplus.com/byteplus-platform/reference/createloginprofile)

* [GetLoginProfile](https://docs.byteplus.com/byteplus-platform/reference/getloginprofile)

* [UpdateLoginProfile](https://docs.byteplus.com/byteplus-platform/reference/updateloginprofile)


<span id="e343251e"></span>
## Structure


|**Parameter** |**Type** |**Description** |
|---|---|---|
|UserName |String |Username. |
|LoginAllowed |Boolean |Whether the user is allow to log in to the BytePlus Console:<br><br><br>* `true`: allowed<br><br>* `false`: not allowed |
|PasswordResetRequired |Boolean |Whether to require the user to reset the password in next login:<br><br><br>* `true`: require<br><br>* `false`: not require |
|LastLoginDate |String |The time of the previous login. |
|LastLoginIp |String |The IP of the previous login. |
