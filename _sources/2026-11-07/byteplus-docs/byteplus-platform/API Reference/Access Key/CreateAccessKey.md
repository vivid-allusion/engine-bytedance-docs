---
title: "CreateAccessKey"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-createaccesskey"
---

Creates a new pair of AccessKey ID (AK) and secret AccessKey (SK) for the admin account or a user.

Method

HTTP GET

Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`CreateAccessKey` |
|Version |String |Yes |`2018-01-01` |
|UserName |String |No |Username. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If <code>UserName</code> is specified, the AK/SK created will belong to the specified user.</div>


* <div data-tips="true" data-tips-type="tip">If <code>UserName</code> is not specified, the AK/SK created will belong to the admin account.</div>



<span id="78695325"></span>
## Response parameter


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|AccessKey |[AccessKey](https://docs.byteplus.com/en/byteplus-platform/reference/accesskey) |A structure containing the details about the new AccessKey. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If the AK/SK is created for a user, the <code>UserName</code> parameter in the structure returned is NOT empty.</div>


* <div data-tips="true" data-tips-type="tip">If the AK/SK is created for the admin account, the <code>UserName</code> parameter in the structure returned is empty.</div>
