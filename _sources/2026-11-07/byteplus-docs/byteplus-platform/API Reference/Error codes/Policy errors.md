---
title: "Policy errors"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-policy-1"
---

Below are policy related error codes.


|**Error** |**Message** |**HTTP Status Code** |
|---|---|---|
|PolicyNotExist |Policy '%s' does not exist or is not attachable. |404 |
|PolicyAlreadyExist |Policy '%s' already exists |409 |
|InvalidPolicyName |Invalid PolicyName '%s', err: '%s' |400 |
|InvalidPolicyType |Invalid PolicyType '%s', err: '%s' |400 |
|MissingPolicyDocument |Missing policy document |400 |
|InvalidPolicyDocumentJson |Policy document has invalid json structure, err: '%s' |400 |
|MissingPolicyStatement |N/A |400 |
|MissingEffectField |N/A |400 |
|InvalidEffectField |Invalid Effect in policy document, err: '%s' |400 |
|MissingActionField |N/A |400 |
|InvalidActionField |Invalid Action in policy document, err: '%s' |400 |
|MissingPrincipalField |N/A |400 |
|InvalidPrincipalField |Invalid Principal in policy document, err: '%s' |400 |
|PolicyDeleteConflict |Cannot delete policy '%s' which attached to role(s) |409 |
|PolicyAttachConflict |Policy '%s' already be attached to '%s' |409 |
|PolicyDetachConflict |Policy '%s' not be attached to '%s' |409 |
|InvalidPolicyScope |Invalid Scope %s, err: %s |400 |
|InvalidPolicyEntityFilter |Invalid EntityFilter %s, err: %s |400 |
