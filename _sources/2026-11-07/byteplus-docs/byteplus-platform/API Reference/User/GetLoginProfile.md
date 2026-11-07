---
title: "GetLoginProfile"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-getloginprofile"
---

Gets the console login configuration for a specified user.

<span id="d8d46611"></span>
## Method

HTTP GET

<span id="f1595b63"></span>
## Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`GetLoginProfile` |
|Version |String |Yes |`2018-01-01` |
|UserName |String |Yes |Username. |


Response parameter


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|User |[LoginProfile](https://docs.byteplus.com/en/byteplus-platform/reference/loginprofile) |A structure conaining the details about the console login configuration for the specified user. |
