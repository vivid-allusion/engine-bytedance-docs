---
title: "CreateUser"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-createuser"
---

Creates a user.

<span id="3d7eb8b7"></span>
## Method

HTTP GET

<span id="c7b1d0da"></span>
## Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`CreateUser` |
|Version |String |Yes |`2018-01-01` |
|UserName |String |Yes |Username. |
|DisplayName |String |No |User's display name, which is used for receiving messages. |
|MobilePhone |String |No |Phone number with a county calling code. For example: `+65 80000000`. |
|Email |String |No |User's email. |
|Description |String |No |User description. |


<span id="5668a2b4"></span>
## Response parameter


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|User |[User](https://docs.byteplus.com/en/byteplus-platform/reference/user) |A structure containing the details about the newly created user. |
