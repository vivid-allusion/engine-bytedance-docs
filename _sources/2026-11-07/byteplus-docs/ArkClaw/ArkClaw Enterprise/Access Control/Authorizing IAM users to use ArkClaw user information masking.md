---
title: "Authorizing IAM users to use ArkClaw user information masking"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Authorizing_IAM_users_to_use_ArkClaw_user_information_masking"
---

By default, only **BytePlus root users** can enable or disable the user information masking toggle in the ArkClaw console. For IAM users requiring access to this feature, you can create a custom policy that includes the `arkclaw:UpdateSpaceIdentityConfig` permission in the BytePlus console and attach the permission policy to the IAM users or user groups. This allows them to enable or disable ArkClaw user information masking. This topic describes how to create a custom permission policy and attach it to the target IAM users or user groups.

<span id="sLB3rvD1"></span>
## Prerequisites


* An IAM user has been created. For user group\-based authorization, a user group has been created. For details, see [Managing users](https://docs.byteplus.com/en/docs/6257/64977) and [Managing user groups](https://docs.byteplus.com/en/docs/6257/104988).

* The target IAM user has been granted access to ArkClaw. For details, see [Authorizing IAM users to use ArkClaw](https://docs.byteplus.com/en/docs/ArkClaw/Authorizing_an_IAM_user_to_use_ArkClaw_Enterprise).

* You have one of the following identities:

   * A BytePlus root user account.

   * An IAM user that meets both the following conditions:

      * Having been granted management access to the IAM console by the root user. For details, see [Authorizing IAM users to use ArkClaw](https://docs.byteplus.com/en/docs/ArkClaw/Authorizing_an_IAM_user_to_use_ArkClaw_Enterprise).

      * Having been attached the `arkclaw:UpdateSpaceIdentityConfig` custom permission policy by the root user.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Only root users possess full permissions and can grant IAM users access to various cloud services. When an IAM user is granted IAM management permissions by the root user, that IAM user can attach custom permission policies to other IAM users. The prerequisite for an IAM user to add the <code>arkclaw:UpdateSpaceIdentityConfig</code> permission to other IAM users is that the IAM user already has this permission.      </div>
      

<span id="KKNZJ3BG"></span>
## Procedure

You can authorize IAM users to use the ArkClaw Enterprise user information masking feature directly. Alternatively, you can first authorize a user group to use this ArkClaw Enterprise feature and then add target IAM users to the user group, allowing the IAM users to inherit the permissions of the user group.


<Tabs>
<Tab zoneid="5onA6fLb" title="Authorizing IAM users directly">
<TabTitle>Authorizing IAM users directly</TabTitle>

1. Log in to the [IAM console](https://console.byteplus.com/iam/identitymanage/user) as a root user or an IAM user with the required permissions.

2. In the left\-side navigation pane, click "Permission policy".

3. On the "Permission policy" page, click "Create Policy".

4. On the "Create Policy" page, provide a policy name and description.

   * **Policy name** (Required): In the "Policy name" text box, enter a custom policy name that meets the on\-screen naming requirements. For this example, the name is `UpdateSpaceIdentityConfig`.

   * **Description** (Optional): In the "Description" text box, enter a compliant description of the custom policy as needed to distinguish it from other policies.

5. Click the "JSON editor" tab. In the editor, enter the following policy content. Click "Submit".

   ```JSON
   {
    "Statement": [
    {
    "Effect": "Allow",
    "Action": [
    "arkclaw:UpdateSpaceIdentityConfig"
    ],
    "Resource": [
    "*"
    ]
    }
    ]
   }
   ```
   

&nbsp;

6. In the left\-side navigation pane, select "User management" \> "User".

7. In the search box, enter the name of the target IAM user and press "Enter". Click "Authorize" in the Actions column for the target IAM user.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1d07f0f51c2ddf1260406fc90629a404.png) </span>

8. On the "Add authorization" page, search for the policy name keyword "`UpdateSpaceIdentityConfig`" and select the `UpdateSpaceIdentityConfig` policy.

9. Select "No" for "Limit to project resources".

10. Click "Submit". Authorization takes effect immediately.

11. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise) with the IAM user account and use the ArkClaw Enterprise user information masking feature.


</Tab>
<Tab zoneid="Qav30PbF" title="Authorizing an IAM user group">
<TabTitle>Authorizing an IAM user group</TabTitle>

1. Log in to the [IAM console](https://console.byteplus.com/iam/identitymanage/user) as a root user or an IAM user with the required permissions.

2. In the left\-side navigation pane, click "Permission policy".

3. On the "Permission policy" page, click "Create Policy".

4. On the "Create Policy" page, provide a policy name and description.

   * **Policy name** (Required): In the "Policy name" text box, enter a custom policy name that meets the on\-screen naming requirements. For this example, the name is `UpdateSpaceIdentityConfig`.

   * **Description** (Optional): In the "Description" text box, enter a compliant description of the custom policy as needed to distinguish it from other policies.

5. Click the "JSON editor" tab. In the editor, enter the following policy content. Click "Submit".

   ```JSON
   {
    "Statement": [
    {
    "Effect": "Allow",
    "Action": [
    "arkclaw:UpdateSpaceIdentityConfig"
    ],
    "Resource": [
    "*"
    ]
    }
    ]
   }
   ```
   

&nbsp;

6. In the left\-side navigation pane, select "User management" \> "User group".

7. In the search box, enter the name of the target user group and press "Enter". Click "Authorize" in the Actions column for the target user group.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_df7cc074850b7d8fea80cdfd01efee8b.png) </span>



&nbsp;

8. On the "Add authorization" page, search for the policy name keyword "`UpdateSpaceIdentityConfig`" and select the `UpdateSpaceIdentityConfig` policy.

9. Select "No" for "Limit to project resources".

10. Click "Submit". Authorization takes effect immediately.

11. On the "User group" page, find the target user group and click "Add User" in the Actions column to add users to the user group.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_89b13f549bbff6ba1618e0ab1d4bfe37.png) </span>

12. In the "Add User" panel, search for the target IAM user, select the target IAM user, and click "OK".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_79bf1beb77fa092ae780fe33ecdf0bb4.png) </span>

13. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise) with the IAM user account and use the ArkClaw Enterprise user information masking feature.


</Tab>
</Tabs>
