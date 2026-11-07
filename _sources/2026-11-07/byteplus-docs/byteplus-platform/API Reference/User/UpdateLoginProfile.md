---
title: "UpdateLoginProfile"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-updateloginprofile"
---

Updates console login configuration for a specified user.

<span id="4821716f"></span>
## Method

HTTP GET

<span id="3c8ee5cc"></span>
## Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`UpdateLoginProfile` |
|Version |String |Yes |`2018-01-01` |
|UserName |String |Yes |Username. |
|Password |String |No |Password. |
|LoginAllowed |Boolean |No |Whether to allow the user to log in to the BytePlus Console:<br><br><br>* `true`: allow<br><br>* `false`: not allow |
|PasswordResetRequired |Boolean |No |Wether to require the user to reset the password in next login:<br><br><br>* `true`: require<br><br>* `false`: not require |


<span id="5c3e52bd"></span>
## Response parameter


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|User |[LoginProfile](https://docs.byteplus.com/en/byteplus-platform/reference/loginprofile) |A structure conaining the details about the updated console login configuration for the specified user. |
