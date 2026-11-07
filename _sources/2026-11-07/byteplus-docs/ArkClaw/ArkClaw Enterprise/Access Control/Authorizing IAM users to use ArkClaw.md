---
title: "Authorizing IAM users to use ArkClaw"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Authorizing_an_IAM_user_to_use_ArkClaw_Enterprise"
---

This topic describes how a root user can assign least\-privilege permissions for ArkClaw Enterprise cloud resources to IAM users or groups for separate access control, operational efficiency, and enhanced security.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This permission configuration applies only to administrators managing ArkClaw Enterprise resources. Regular employees using ArkClaw Enterprise require neither BytePlus accounts nor this permission configuration.</div>


<span id="eL7FQwfK"></span>
## Prerequisites

An IAM user has been created. For user group\-based authorization, a user group has been created. For details, see [Managing users](https://docs.byteplus.com/en/docs/6257/64977) and [Managing user groups](https://docs.byteplus.com/en/docs/6257/104988).

<span id="0OWfM6IY"></span>
## Usage notes

While a root user has full resource access, sharing credentials in complex access scenarios can create inconvenience and security risks. Therefore, when resources are shared among multiple users, you can use the IAM feature to create IAM users or user groups and grant them specific permissions for cloud resource access as the root user. This enables multi\-identity management and fine\-grained permission control.


* A root user or IAM user with the global permission for the `ArkClawFullAccess` policy can view and manage all ArkClaw spaces within the account. For information about how to grant global access, see [Scenario 1: Grant global permissions](https://docs.byteplus.com/en/docs/ArkClaw/Authorizing_an_IAM_user_to_use_ArkClaw_Enterprise?TagIDs=512,2,522,502&lang=en#gCqFqjTK).

* In multi\-space scenarios, to allow different IAM users to manage different spaces, grant them the `ArkClawFullAccess` policy for the owning project of the space and global permissions for the `ArkClawSpaceGlobalAccess`, `APMPlusServerReadOnlyAccess`, `TLSReadOnlyAccess`, `ClawSentryUserAccess`, and `PCCFullAccess` policies. For details on project permissions, see [Scenario 2: Grant project permissions](https://docs.byteplus.com/en/docs/ArkClaw/Authorizing_an_IAM_user_to_use_ArkClaw_Enterprise?TagIDs=512,2,522,502&lang=en#5qQx0Wfg).



|Policy name |Description |
|---|---|
|ArkClawFullAccess |The ArkClaw Enterprise read/write access policy that grants access and management permissions for ArkClaw Enterprise resources. |
|ArkClawReadOnlyAccess |The ArkClaw Enterprise resource view policy that grants read\-only access to ArkClaw Enterprise resources. It does not grant management permissions. |


<span id="6BrnyhGl"></span>
## Procedure

You can authorize IAM users to access or manage ArkClaw Enterprise directly. Alternatively, you can first authorize a user group to access or manage ArkClaw Enterprise and then add target IAM users to the user group. This allows the IAM users to inherit the permissions of the user group.

<span id="gCqFqjTK"></span>
### Scenario 1: Grant global permissions


<Tabs>
<Tab zoneid="C86489Pl" title="Authorizing IAM users directly">
<TabTitle>Authorizing IAM users directly</TabTitle>

1. Log in to the [IAM console](https://console.byteplus.com/iam/identitymanage/user) as a root user or an IAM user with the required permissions.

2. In the left\-side navigation pane, select "User management" \> "User".

3. In the search box, enter the name of the target IAM user, press the "Enter" key, and click "Authorize" in the Actions column for the target IAM user.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1d07f0f51c2ddf1260406fc90629a404.png) </span>

4. On the "Add authorization" page, search for the policy name keyword "ArkClaw" and select the `ArkClawFullAccess` policy.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e0e8d59869fbbdfc0d52c45dfca051f6.png) </span>

5. Click "Submit". Authorization takes effect immediately.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fa243a0a1227aaa0fc0b8952be1e1031.png) </span>

6. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise) with the IAM user account. Then, manage and use ArkClaw Enterprise resources.


</Tab>
<Tab zoneid="rc2RIHvB" title="Authorizing an IAM user group">
<TabTitle>Authorizing an IAM user group</TabTitle>

1. Log in to the [IAM console](https://console.byteplus.com/iam/identitymanage/user) as a root user or an IAM user with the required permissions.

2. In the left\-side navigation pane, select "User management" \> "User group".

3. In the search box, enter the name of the target user group, press the "Enter" key, and click "Authorize" in the Actions column for the target user group.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_df7cc074850b7d8fea80cdfd01efee8b.png) </span>

4. On the "Add authorization" page, search for the policy name keyword "ArkClaw" and select the `ArkClawFullAccess` policy.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8f12f90681382549cecca1f2cdef37e2.png) </span>

5. Click "Submit". Authorization takes effect immediately.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_86efbbffac9e4a14fc7046bc8492bde3.png) </span>

6. On the "User group" page, find the target user group and click "Add User" in the Actions column to add users to the user group.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_89b13f549bbff6ba1618e0ab1d4bfe37.png) </span>

7. In the "Add User" panel, search for the target IAM user, select the target IAM user, and click "OK".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_79bf1beb77fa092ae780fe33ecdf0bb4.png) </span>

8. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise) with the IAM user account. Then, manage and use ArkClaw Enterprise resources.


</Tab>
</Tabs>


<span id="5qQx0Wfg"></span>
### Scenario 2: Grant project permissions


<Tabs>
<Tab zoneid="bLzU2KRu" title="Authorizing IAM users directly">
<TabTitle>Authorizing IAM users directly</TabTitle>

1. Log in to the [IAM console](https://console.byteplus.com/iam/identitymanage/user) as a root user or an IAM user with the required permissions.

2. In the left\-side navigation pane, select "User management" \> "User".

3. Attach the required policies to the IAM user.

   1. In the search box, enter the name of the target IAM user, press the "Enter" key, and click "Authorize" in the Actions column for the target IAM user.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1d07f0f51c2ddf1260406fc90629a404.png) </span>

   2. On the "Add authorization" page, search for the policy name "ArkClawFullAccess" and select `ArkClawFullAccess` in the result list. Repeat the step to select the following policies: `ArkClawSpaceGlobalAccess`, `APMPlusServerReadOnlyAccess`, `TLSReadOnlyAccess`, `ClawSentryUserAccess`, and `PCCFullAccess`.

   3. Select "No" for "Limit to project resources". Click "Submit". The authorization takes effect immediately.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fa243a0a1227aaa0fc0b8952be1e1031.png) </span>

4. Configure project permissions for the `ArkClawFullAccess` policy attached to the IAM user.

   1. In the left navigation pane of the [IAM console](https://console.byteplus.com/iam/identitymanage/user), select "User management" \> "User".

   2. In the user list, search for the target user by username, user ID, display name, or other information, and click the username.

   3. On the "Policy" tab of the user details page, find the `ArkClawFullAccess` policy and click "Modify project limits" in the Actions column.

   4. For "Scope of action", select "Designated projects". In the drop\-down list, select the project where the target space is located, and click "Confirm".

5. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise) with the IAM user account. Then, manage and use ArkClaw Enterprise resources.


</Tab>
<Tab zoneid="C0fU7dl8" title="Authorizing an IAM user group">
<TabTitle>Authorizing an IAM user group</TabTitle>

1. Log in to the [IAM console](https://console.byteplus.com/iam/identitymanage/user) as a root user or an IAM user with the required permissions.

2. In the left\-side navigation pane, select "User management" \> "User group".

3. Attach the required policies to the user group.

   1. In the search box, enter the name of the target user group, press the "Enter" key, and click "Authorize" in the Actions column for the target user group.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_df7cc074850b7d8fea80cdfd01efee8b.png) </span>

   2. On the "Add authorization" page, search for the policy name "ArkClawFullAccess" and select `ArkClawFullAccess` in the result list. Repeat the step to select the following policies: `ArkClawSpaceGlobalAccess`, `APMPlusServerReadOnlyAccess`, `TLSReadOnlyAccess`, `ClawSentryUserAccess`, and `PCCFullAccess`.

   3. Select "No" for "Limit to project resources". Click "Submit". The authorization takes effect immediately.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_86efbbffac9e4a14fc7046bc8492bde3.png) </span>

4. Configure project permissions for the `ArkClawFullAccess` policy attached to the user group.

   1. In the left navigation pane of the [IAM console](https://console.byteplus.com/iam/identitymanage/user), select "User management" \> "User group".

   2. In the user group list, search for the target user group by its group name, display name, or other information, and click the name of the user group.

   3. On the "Policy" tab of the user group details page, find the `ArkClawFullAccess` policy and click "Modify project limits" in the Actions column.

   4. For "Scope of action", select "Designated projects". In the drop\-down list, select the project where the target space is located, and click "Confirm".

5. Add IAM users to the user group.

   1. On the "User group" page, find the target user group and click "Add User" in the Actions column to add IAM users to the user group.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_89b13f549bbff6ba1618e0ab1d4bfe37.png) </span>

   2. In the "Add User" panel, search for the target IAM user, select the target IAM user, and click "OK".

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_79bf1beb77fa092ae780fe33ecdf0bb4.png) </span>

6. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise) with the IAM user account. Then, manage and use ArkClaw Enterprise resources.


</Tab>
</Tabs>


<span id="EWPKyvSA"></span>
### 

&nbsp;
