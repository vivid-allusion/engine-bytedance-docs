---
title: "Role errors"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-role-1"
---

Below are role related error codes.


|**Error** |**Message** |**HTTP Status Code** |
|---|---|---|
|RoleNotExist |Role '%s' cannot be found |404 |
|RoleAlreadyExists |Role '%s' already exists. |409 |
|RoleNameAlreadyExists |NewRoleName %s already exists |409 |
|InvalidRoleName |Invalid RoleName '%s', err: '%s' |400 |
|AccountRoleLimitExceeded |Cannot exceed Quota for '%s': '%d' |409 |
|RoleDeleteConflictWithPolicy |Cannot delete role '%s', must detach all policies first |409 |
|RoleDeleteConflictWithUser |Cannot delete role '%s', must remove all users first |409 |
|InvalidTrustPolicyDoc |Invalid TrustPolicy, err: '%s'. |400 |
|InvalidAssociatedAccountType |Invalid AssociatedAccountType `%s`, err: `%s`. |400 |
|RoleConfigAlreadyExists |RoleConfig '%v' already exists. |409 |
