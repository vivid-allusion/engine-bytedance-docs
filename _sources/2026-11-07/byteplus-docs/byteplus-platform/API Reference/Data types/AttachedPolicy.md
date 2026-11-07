---
title: "AttachedPolicy"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-attachedpolicy"
---

This data type includes information about the policy added to users or roles. It is used as a response element in the following methods:


* [ListAttachedUserPolicies](https://docs.byteplus.com/byteplus-platform/reference/listattacheduserpolicies)

* [ListAttachedRolePolicies](https://docs.byteplus.com/byteplus-platform/reference/listattachedrolepolicies)


<span id="8c3f2a3c"></span>
## Structure


|**Parameter** |**Type** |**Description** |
|---|---|---|
|PolicyTrn |String |The resource name of the policy. |
|PolicyName |String |Policy name. |
|PolicyType |String |Policy type: `System` |
|AttachDate |String |The time when the policy was attached to users or roles. |
|Description |String |Policy description. |
