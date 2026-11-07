---
title: "Owner errors"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-owner"
---

Below are owner related error codes.


|**Error** |**Message** |**HTTP Status Code** |
|---|---|---|
|AddAccountOwnerConflict |Identity `%s` already be the Owner of Account `%v`. |409 |
|AddPolicyOwnerConflict |Identity `%s` already be the Owner of Policy `%v`. |409 |
|RemoveAccountOwnerConflict |Identity `%s` not be the Owner of Account `%v`. |409 |
|RemovePolicyOwnerConflict |Identity `%s` not be the Owner of Policy `%v`. |409 |
