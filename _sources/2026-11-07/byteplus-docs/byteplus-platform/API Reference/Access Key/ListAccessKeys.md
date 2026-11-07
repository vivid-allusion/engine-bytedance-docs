---
title: "ListAccessKeys"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-listaccesskeys"
---

Gets a list of AccessKeys that belongs to the admin account or a specified IAM user.

The admin account is able to get a list of AccessKeys that belongs to itself or any of its IAM users. According to the permission granted to an IAM user, they are able to get a list of AccessKeys that belong to themselves or other IAM users.

<span id="98166a92"></span>
## Method

HTTP GET

<span id="363432b3"></span>
## Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`ListAccessKeys` |
|Version |String |Yes |`2018-01-01` |
|UserName |String |No |The name of the IAM user for which to get an AccessKey list.<br><br>***Note***: If you want to get a list of AccessKeys that belong to the admin account, leave this parameter empty. |


<span id="9c53ae50"></span>
## Response parameter


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|AccessKeyMetadata |[AccessKeyMetadata](https://docs.byteplus.com/en/byteplus-platform/reference/accesskeymeta) |A list containing the metadata about all the returned AccessKeys. |
