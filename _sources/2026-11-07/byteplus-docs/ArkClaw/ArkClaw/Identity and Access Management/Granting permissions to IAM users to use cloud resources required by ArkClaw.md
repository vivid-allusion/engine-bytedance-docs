---
title: "Granting permissions to IAM users to use cloud resources required by ArkClaw"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Granting_permissions_to_IAM_users_to_use_cloud_resources_required_by_ArkClaw"
---

While a root user has full resource access, sharing credentials in complex access scenarios can create inconvenience and security risks. Therefore, when resources are shared among multiple users, you can use the IAM feature to create IAM users or user groups and grant them specific permissions for cloud resource access as the root user. This enables multi\-identity management and fine\-grained permission control.

This topic describes how to create IAM users or user groups as the root user and grant the minimum permissions required for ArkClaw to access cloud resources to IAM users or user groups based on needs. This helps achieve delegated management, improve management efficiency, and maintain account security.

<span id="x2vOXb8q"></span>
## Procedure

You can create users and directly grant permissions to them, or grant user group\-associated permissions to them by adding them to a user group.


<Tabs>
<Tab zoneid="YHuerpn7" title="Grant permissions to IAM user directly">
<TabTitle>Grant permissions to IAM user directly</TabTitle>

1. Log in to the  as the root user or an authorized account, and create an IAM user. 

2. Assign permission policies related to cloud products required by ArkClaw to the target IAM user. 

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To allow your IAM user to only access the ArkClaw console and view information about the created ArkClaw, assign the <code>ArkClawXReadOnlyAccess</code> permission.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To allow your IAM user to create and manage ArkClaw, assign the <code>ArkClawXFullAccess </code>permission.   </div>
   

3. Log in to the platform as the IAM user.

   * **Method 1:** 

      On the user list page of the, copy the IAM user login link for the current account and open it to log in directly.

   * **Method 2:** 

      Access the platform. Then, click "IAM user" at the lower right of the "Log in now" button to navigate to the user login page. First, enter the account name or ID of the root user, and then enter the IAM username and password for login.


</Tab>
<Tab zoneid="aeqsPwqV" title="Grant permissions to IAM user by adding IAM user to user group">
<TabTitle>Grant permissions to IAM user by adding IAM user to user group</TabTitle>

1. Log in to the  as the root user or an authorized account, and create a user group. 

2. Assign permission policies related to cloud products required by ArkClaw to the target user group. 

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To allow your IAM user to only access the ArkClaw console and view information about the created ArkClaw, assign the <code>ArkClawXReadOnlyAccess</code> permission.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To allow your IAM user to create and manage ArkClaw, assign the <code>ArkClawXFullAccess </code>permission.   </div>
   

3. Create an IAM user. 

4. Add the IAM user to the user group. 

5. Log in to the platform as the IAM user.

   * **Method 1:** 

      On the user list page of the, copy the IAM user login link for the current account and open it to log in directly.

   * **Method 2:** 

      Access the platform. Then, click "IAM user" at the lower right of the "Log in now" button to navigate to the user login page. First, enter the account name or ID of the root user, and then enter the IAM username and password for login.


</Tab>
</Tabs>
