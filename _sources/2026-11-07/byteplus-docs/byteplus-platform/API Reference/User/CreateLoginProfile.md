---
title: "CreateLoginProfile"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-createloginprofile"
---

Sets up console login configuration for a specified user.

<span id="25fe5f49"></span>
## Method

HTTP GET

<span id="ae79664d"></span>
## Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`CreateLoginProfile` |
|Version |String |Yes |`2018-01-01` |
|UserName |String |Yes |Username. |
|Password |String |Yes |Password. |
|LoginAllowed |Boolean |No |Whether to allow the user to log in to the BytePlus Console:<br><br><br>* `true`: allow<br><br>* `false`: not allow |
|PasswordResetRequired |Boolean |No |Wether to require the user to reset the password:<br><br><br>* `true`: require<br><br>* `false`: not require |


<span id="f5e54a03"></span>
## Response parameter


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|User |[LoginProfile](https://docs.byteplus.com/en/byteplus-platform/reference/loginprofile) |A structure conaining the details about the console login configuration for the specified user. |
