---
title: "ArkClaw IAM policies"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_IAM_policies"
---

This topic describes the types of IAM policies and those related to ArkClaw to help you quickly understand IAM policies. Two IAM policy types are supported: system default policies and custom policies. You can use system default policies to grant IAM identities directly. If the system default policies can not meet your needs, you can use custom policies to grant permissions precisely and manage resources flexibly.

<span id="WaWEsEUJ"></span>
## System default policies

<span id="COB0CEq1"></span>
### ArkClaw system default policies

The IAM platform has default ArkClaw\-related policies preset, with details in the following table.

You can directly assign these system default policies to IAM entities (IAM users, user groups, or roles). **System default policies are for authorization only and can not be edited or modified**.


|System default policy name |Description |
|---|---|
|ArkClawXFullAccess |Once granted this policy, IAM identities (IAM users, user groups, and roles) gain management permissions for ArkClaw within the permission scope (global permission or project\-level permission). For example, IAM identities can create, change, and view resources. |
|ArkClawXReadOnlyAccess |Once granted this policy, IAM identities (IAM users, user groups, and roles) gain read\-only permissions for ArkClaw within the permission scope (global permission or project\-level permission). An IAM identity granted with this policy can only view ArkClaw\-related resources, but not perform any management on them or view other unauthorized cloud products. |


<span id="4xvAMIFF"></span>
### Details of ArkClaw system default policies

<span id="iryNfESd"></span>
#### Details of the ArkClawXFullAccess policy

```json
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "arkclawx:*",
        "ark:ListSubscribeTrade",
        "ark:CreateSubscribeTrade",
        "ark:EstimateSubscribePrice",
        "ark:ListApiKeys",
        "ark:GetRawApiKey",
        "ark:ListFoundationModels"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```


<span id="jbzJQ6X7"></span>
#### Details of the ArkClawXReadOnlyAccess policy

```json
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "arkclawx:Describe*",
        "arkclawx:Get*",
        "arkclawx:List*",
        "ark:ListSubscribeTrade",
        "ark:ListApiKeys",
        "ark:GetRawApiKey",
        "ark:ListFoundationModels"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Custom policies

For details, refer to [Creating custom policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-3).
