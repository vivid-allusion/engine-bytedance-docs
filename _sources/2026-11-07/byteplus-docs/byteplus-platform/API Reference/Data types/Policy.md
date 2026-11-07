---
title: "Policy"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-policy"
---

This data type includes information about policies. It is used as a response element in the following methods:


* [CreatePolicy](https://docs.byteplus.com/byteplus-platform/reference/createpolicy)

* [GetPolicy](https://docs.byteplus.com/byteplus-platform/reference/getpolicy)

* [UpdatePolicy](https://docs.byteplus.com/byteplus-platform/reference/updatepolicy)

* [ListPolicies](https://docs.byteplus.com/byteplus-platform/reference/listpolicies)


<span id="6ab945f7"></span>
## Structure


|**Parameter** |**Type** |**Description** |
|---|---|---|
|PolicyTrn |String |The resource name of the policy. |
|PolicyName |String |Policy name. |
|PolicyType |String |Policy type: `System` |
|CreateDate |String |The time when the policy was created. |
|UpdateDate |String |The time when the policy was updated. |
|Description |String |Policy description. |
|PolicyDocument |String |Policy document. |


<span id="92646961"></span>
## PolicyDocument

BytePlus IAM offers identity\-based policies. The JSON\-formatted PolicyDocument determines how to implement the rule defined in a policy. The required elements for PolicDocument are described below.


|**Name** |**Description** |
|---|---|
|Statement |The `Statement` element is the main and required element of a policy. It can contain an individual statement only or an array of individual statements. |
|Effect |The `Effect` element is required. It indicates the result of the statement. Its valid values are `Allow` or `Deny`. |
|Action |The `Action` element describes the specific action. It has the same meaning as the Action element in cloud service API. Therefore, when describing the Action, element, it is necessary to describe the specific cloud service in the prefix `{service}:{action}`. `*` and `?` are supported when describing the `Action` element. |
|Resource |The `Resource` element specifies the resource that the Action element covers. It is described in TRN format: `trn: {service}:{region}:{account}: {resourceType}/{id}`. |


The sample PolicyDocument is as follows:

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iam:*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```
