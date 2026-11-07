---
title: "Network Advisor IAM policy type"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/Network-Advisor-IAM-policy-type"
---

This topic introduces the types of IAM policies and policies related to Network Advisor (NA) to help you quickly understand IAM policies. IAM policies support two types: System default policies and custom policies. You can directly use system default policies to authorize IAM identities. If the system default policy cannot meet your needs, you can use a custom policy for precise authorization to flexibly manage account resources.

## System default policy

The IAM platform has preset default policies for NA. You can directly assign these system default policies to IAM identities (IAM users, user groups, or roles). **System default policies can only be used for authorization and cannot be edited or modified**.

### Network Advisor system default policies

|**System default policy name** |**Description** |**Policy type** |
|---|---|---|
|[NAFullAccess](https://console.byteplus.com/iam/policymanage/System/NAFullAccess?tab=content)<br><br> |IAM identities (IAM users, user groups, or roles) granted this policy will obtain full administrative permissions for NA within the authorized scope, including all create, view, modify, and delete operations. |Policy |
|[NAReadOnlyAccess](https://console.byteplus.com/iam/policymanage/System/NAReadOnlyAccess?tab=content) |An IAM identity (IAM user, user group, or role) granted this policy obtains read\-only access to all NA resources within the authorized scope. If an IAM identity is granted only this permission, it will have read\-only access to NA resources. It cannot perform any operations on NA resources and cannot access other unauthorized products. |Policy |
|[ServiceRoleForNA](https://console.byteplus.com/iam/policymanage/System/ServiceRoleForNA?tab=content) |Used to authorize the NA associated role. NA uses this role to obtain information such as traffic and status data of network products. |Policy |

Details are as follows:

**NAFullAccess**

```JSON

{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "na:*"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}

```

###

**NAReadOnlyAccess**

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "na:*Describe*",
        "na:*Search*",
        "na:*Get*",
        "na:*List*",
        "na:NeptuneCrossTrafficAnalysisWhiteListRegion"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```

##

**ServiceRoleForNA**

```JSON
{
  "Statement" : [
    {
      "Action" : [
        "Volc_Observe:GetMetricData",
        "cloudmonitor:GetMetricData"
      ],
      "Effect" : "Allow",
      "Resource" : [
        "*"
      ]
    }
  ]
}
```

## Custom policy

|Topic |Explanation |
|---|---|
|Custom policy types |Custom policies are divided into identity\-based policies and resource\-based policies, depending on the entity that they are associated. |
|Custom policy syntax |Custom policy syntax defines policy permissions through policy elements. When creating an identity\-based policy and a resource\-based policy, the policy elements differ. |
|Create custom policy |When you use a BytePlus main account or an IAM user with IAM permissions to authorize, and the system default policy cannot meet your requirements, you can granularly define permissions through a custom policy. |
