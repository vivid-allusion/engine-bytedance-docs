---
title: "Granting AgentKit permissions to IAM users"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Granting_AgentKit_permissions_to_IAM_users"
---

This topic describes how to grant global permissions or project\-level permissions for AgentKit resources to IAM users. You can authorize IAM users directly, or add IAM users to a user group and authorize the user group. Members in the user group will inherit the permissions of the user group.

<span id="dbo0u9Ku"></span>
## Procedure


1. Log in to the [IAM console](https://console.byteplus.com/iam/identitymanage/user) using your account.

2. Enter the IAM user or user group authorization page.

   
   <Tabs>
   <Tab zoneid="7FgAeIav" title="IAM user">
   <TabTitle>IAM user</TabTitle>
   
   1. In the left navigation pane, select "User management \> User".
   
   2. (Optional) If an IAM user has not been created, [create an IAM user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user) first.
   
   3. Click "Authorize" in the "Actions" column of the target user to enter the authorization page.
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_89114088912017492cda987478939276.png) </span>
   
   
   </Tab>
   <Tab zoneid="aLqWZbY9" title="User group">
   <TabTitle>User group</TabTitle>
   
   1. In the left navigation pane, select "User management \> User group".
   
   2. (Optional) If a user group has not been created, [create a user group](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-project) first.
   
   3. (Optional) If an IAM user has not been created, [create an IAM user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user) first.
   
   4. (Optional) Add the target [IAM user to the corresponding user group](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-user-group).
   
   5. Click "Authorize" in the "Actions" column of the target user group to enter the authorization page.
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a96bb3b8b2bcb5af015c9da5874c337d.png) </span>
   
   
   </Tab>
   </Tabs>
   

3. Configure permissions for the IAM user or user group.

   1. Configure the AgentKit system permission **AgentKitDeveloperAccess (recommended) and** service\-dependent permissions **.**  [Learn more](https://docs.byteplus.com/en/docs/agentkit/AgentKit_IAM_policy_types)

      **AgentKitDeveloperAccess:**  An IAM identity (IAM user, user group, or role) granted this policy obtains development permissions for all AgentKit features within the authorized scope (global or project\-level permissions).

      This permission level is higher than read\-only access but lower than full access:

               * Compared with the read\-only permission, AgentKitReadOnlyAccess supports resource creation, configuration, update, testing, and release.

               * Compared with the full management permission, AgentKitFullAccess provides only development and runtime capabilities, excluding high\-risk platform\-level management operations.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c903993ec2bae07dfa8f787b810def60.png) </span>

   2. Click "Submit" to complete authorization.

      * IAM user

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_add894c349625f28c79b73173ec26c44.png) </span>

      * User group

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c6c5b353b47f4893a03a7c35ea10c0d0.png) </span>

   3. (Optional) If you want an IAM user or user group to access only AgentKit resources in a specific project, you need to limit the AgentKit permission (AgentKitDeveloperAccess) to the specific project and configure service\-dependent permissions. Otherwise, skip this step.

      1. Restrict an IAM user or user group to access only AgentKit resources in a specific project.

         1. Go to the "Policy" tab of the IAM user or user group, and click "Modify project limits" in the "Actions" column of the AgentKitDeveloperAccess policy.

            * IAM user

               <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1ccb2e0bf36843519c7733bdfa868193.png) </span>

               <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_74ad78676c58e47bfb1aa26fd8010559.png) </span>

            * User group

               <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_058404b31c6fe38b3e56da06488dacbd.png) </span>

         2. In the **Scope of action** section, select **Designated projects**, and select the target project (such as project1) from the drop\-down list.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d9f2ecf9ecceea9ae6d10b59a5ec413b.png) </span>

         3. Click "Confirm" to complete the operation.

            * IAM user

               <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b26dabe82bdcc591d589227e1eb38210.png) </span>

            * User group

               <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_80dc9c409bd591c7bd0c6a6061d68e7d.png) </span>

      2. Configure service\-dependent permissions.

         1. Click "Authorize" and configure the following dependent permissions.

            * BytePlus Ark: ArkGlobalInitAccess.

            * Agent identity and permission management platform: IDLimitedAccess.

            * IAM: IAMFullAccess.

            * (Optional) To monitor the performance, accuracy, and reliability of AgentKit resources in real time: configure the Application Performance Management Plus permission APMPlusServerWithoutProjectAccess.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ea535efd5b1f170028d891c102fa8575.png) </span>

         2. Click "Submit" to complete authorization.

            * IAM user

               <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ca0b82a79fca61c22bc4908897fd5564.png) </span>

            * User group

               <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4bd72a34e5b3500c1d7a3fd1ed2c4c45.png) </span>

4. Log in to the [AgentKit console](https://console.byteplus.com/agentkit) as the IAM user.
