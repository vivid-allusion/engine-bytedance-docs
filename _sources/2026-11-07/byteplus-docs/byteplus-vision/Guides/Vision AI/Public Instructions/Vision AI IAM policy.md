---
title: "Vision AI IAM policy"
product: "Vision AI"
product_code: "byteplus-vision"
source: "https://docs.byteplus.com/en/docs/byteplus-vision/vision-ai-iam-policy"
---

# Overview

BytePlus Vision AI exposes its capabilities—such as OmniHuman, DreamActor, Dreamina 4.6, Flash Avatar, and Clone Avatar—through OpenAPI endpoints under the cv service (for example, https://cv.byteplusapi.com). Every API request must be authenticated. IAM lets you decide **which identities** can call **Vision AI actions**, instead of sharing the primary account's AccessKey with everyone.

When you sign up for a BytePlus account, that account is the admin account and owns all Vision AI resources. The admin account has full access permissions. To allow other staff or applications to use Vision AI without exposing the primary account credentials, create IAM users (sub\-accounts), user groups, or roles, then attach policies that grant just the Vision AI permissions they need.

For the general introduction to IAM, refer to [IAM overview](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-3).

# IAM policy types for Vision AI

By default, a newly created IAM user, user group, or role has **no permissions** on Vision AI resources. Before an identity can call Vision AI actions, you must attach the CVFullAccess policy to it. BytePlus IAM supports two policy types: **system default policies** and **custom policies**.

## System default policies

The IAM console ships with preset policies for Vision AI. Attach these policies to IAM users, user groups, or roles to grant commonly needed permission sets.

|**Policy name** |**Description** |**Supported operations** |
|---|---|---|
|[CVFullAccess](https://console.byteplus.com/iam/policymanage/System/CVFullAccess) |Vision AI read and write policy |Call all Vision AI actions, including submitting tasks (OmniHuman, DreamActor, Dreamina, Flash Avatar, Clone Avatar), querying task results, and canceling tasks. |

Check the IAM console under **Policies** and filter by the cv service.

* Details of the system default policies

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "cv:*",
        "cv_console:*"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```

> **Tip**

## > **Recommendation:** BytePlus recommends that you use the system default policy CVFullAccess whenever possible. It is maintained and updated by BytePlus to cover all current Vision AI API and console actions, ensuring compatibility with new features as they are released. Create custom policies only when the default policies cannot meet your business requirements.

## Custom policies

If the default policies cannot meet your business requirements—for example, you want a user to **call APIs** but **cannot access the** Vision AI **console**. A custom policy is a JSON document described in [What is the policy syntax?](https://docs.byteplus.com/en/docs/byteplus-platform/docs-what-is-the-policy-syntax).

A Vision AI custom policy uses these elements:

|**Element** |**Description** |
|---|---|
|Statement |The main and required element. Contains one or more individual permission statements. |
|Effect |Required. Allow or Deny. |
|Action |The Vision AI API action, in the form cv:{Action}.  |
|Resource |The Vision AI resource the action covers, in TRN format: trn:cv:{region}:{account}:{resourceType}/{id}. |

### Common Vision AI actions

|**Action** |**Description** |
|---|---|
|cv:\* |Vision AI API actions. |
|cv_console:\* |Vision AI Console actions. |

### Custom policy examples

**Example 1: Access to Vision AI API**

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "cv:*"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```

**Example 2: Access to Vision AI Console**

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "cv_console:*"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```

# Granting Vision AI permissions to an IAM user

1. **Create the IAM user.**  In the BytePlus console, go to **IAM** \> **Identity management** \> **User** and click **Add user**. Enter a username, set a console password or create an AccessKey as needed, then click **OK**.

2. **Attach a policy.**  On the user detail page, click **Add permission**. Choose the system default policy (such as [CVFullAccess](https://console.byteplus.com/iam/policymanage/System/CVFullAccess)) or a custom policy you created, then confirm.

3. **Distribute credentials.**  If the user will call the API programmatically, create an AccessKey for that user and share the AK/SK securely. If the user will use the console, share the login URL and password.

4. **Verify.**  The IAM user calls a Vision AI action—for example, submitting an OmniHuman 2.0 task—with their own AccessKey.
