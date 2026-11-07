---
title: "UpdateAccessKey"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-updateaccesskey"
---

Updates a specified AccessKey.

The admin account is able to update the AccessKeys that belongs to itself or any of its IAM users. According to the permission granted to an IAM user, they are able to update the AccessKeys that belong to themselves or other IAM users.

<span id="3d448beb"></span>
## Method

HTTP GET

<span id="57c90f11"></span>
## Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`UpdateAccessKey` |
|Version |String |Yes |`2018-01-01` |
|AccessKeyId |String |Yes |AccessKey ID. |
|Status |String |Yes |AccessKey status: `active` |


<span id="4074c90d"></span>
## Response parameter

None.
