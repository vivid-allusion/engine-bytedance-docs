---
title: "How do I fix the \"AccessDenied Code:403\" error?"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/How_to_handle_an_AccessDenied_Code_403_issue"
---

## Issue description

When an IAM user first logs in to CR, an insufficient permissions error may appear. Example error message:

* Error code: `AccessDenied Code:403` Error messages are similar.

* Error description: `User is not authorized to perform: cr:SetUser on resource:trn cn-****:instance/****`.

## Solution

Before using CR, an IAM user must be granted the required resource management permissions by the root user.

* System policies: These are created by BytePlus. You can use them, but you cannot modify them. BytePlus maintains policy version updates. For details, see [Adding system policies](https://docs.byteplus.com/en/docs/cr/Adding_system_policies).

* Custom policies: You can create, update, and delete them yourself. You maintain policy version updates. For details, see [Adding custom policies](https://docs.byteplus.com/en/docs/cr/Adding_custom_policies).
