---
title: "GetPolicy"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-getpolicy"
---

Get the information about a specified policy.

<span id="84478ae1"></span>
## Method

HTTP GET

<span id="05b9981c"></span>
## Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`GetPolicy` |
|Version |String |Yes |`2018-01-01` |
|PolicyName |String |Yes |Policy name. |
|PolicyType |String |Yes |Policy type: `System` |


Response parameter


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|Policy |[Policy](https://docs.byteplus.com/en/byteplus-platform/reference/policy) |A structure containing the details about the specified policy. |
