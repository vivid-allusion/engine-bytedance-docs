---
title: "Cross-service authorization"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Cross-service_authorization"
---

Before you use ArkClaw, BytePlus authorizes cross\-service access for your account to allow ArkClaw to access other services it depends on (for example, Coding Plan subscription status, and ModelArk API\-Key list).

This topic describes the cross\-service access authorization for ArkClaw.

<span id="fILk52Ch"></span>
## **Authorization information**

BytePlus IAM supports policy management. The platform authorizes an ArkClaw account by attaching the `ServiceRoleForArkClawX `role to the account and then attaching the `ServicePolicyForArkClawX` policy to that role to access other services. ​The statement for the `ServicePolicyForArkClawX` policy is as follows:

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ark:ListSubscribeTrade",
        "ark:ListApiKeys",
        "ark:GetRawApiKey",
        "ark:CreateApiKey"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more information about IAM roles and policies, see <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-roles-management">Role management</a> and <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-policy-management">Policy management</a>.</div>
