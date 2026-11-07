---
title: "Using HBase with sub-accounts"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Using_HBase_with_sub-accounts"
---

A user is an identity for access control, created by a master account or a user with permissions. After a policy is granted to a user, they can log in to the console or use an Access Key to call APIs to access cloud resources. Each admin account can create multiple sub\-accounts and grant different permissions to different sub\-accounts to manage the access rights of different identities under the account to cloud resources. This article introduces the relevant content of using HBase services through sub\-accounts.

<span id=".6YCC55So5Zy65pmv"></span>
## Applicable scenarios


* **Independent resource management scenarios**: Create different sub\-accounts for different businesses and access resources belonging to different businesses through sub\-accounts.

* **Security issues**: Using the AK/SK of the sub\-account to call the Open API interface can effectively avoid the risk of leakage of the master account AK/SK.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permission description

<span id=".562W55Wl566h55CG"></span>
### Policy management

IAM supports two types of policies: system\-preset policies and custom policies. For more information, see [About policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-policies).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To access the HBase service, a sub\-account requires at least the management or read\-only permissions for HBase, VPC, and Cloud Monitor from the system preset policies.</div>


* <div data-tips="true" data-tips-type="tip">Cloud Monitor can only add this permission for sub\-accounts at the global level, not as project permission.</div>


* **System preset policy**: collections of common permissions created and managed by BytePlus, which are coarse\-grained. System default policies can only be used for authorization and cannot be edited or modified.

   
   |Associated Service |Policy name |Description |
   |---|---|---|
   |All IAM\-enabled products on BytePlus |AdministratorAccess |Includes management permissions for all IAM\-supported products, such as ECSFullAccess, VPCFullAccess, IAMFullAccess, and CloudMonitorFullAccess.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">sub\-accounts with the <code>AdministratorAccess</code> permission will have management permissions for all BytePlus products within the authorized scope (project or global). Authorize with caution.</div><br> |
   |Table Storage for HBase |HBaseFullAccess |Full management permissions for Table Storage for HBase. Adding this permission grants the user read and write permissions for Table Storage for HBase within the policy scope, including creating, deleting, and modifying instance configurations. |
   ||HBaseReadOnlyAccess |Read\-only access permissions for Table Storage for HBase. This permission allows the user to view HBase instances within the policy scope. |
   |Virtual private cloud |VPCFullAccess |Full management permissions for Virtual Private Cloud (VPC). This permission grants the user read and write access to VPC within the policy scope, including creating VPC and associating VPC or subnets to HBase instances. |
   ||VPCReadOnlyAccess |ead\-only access to private networks (VPC). After adding this permission, the user can view the private network and subnet information of HBase instances within the policy scope. |
   |Cloud Monitor |CloudMonitorFullAccess |Full management permissions for Cloud Monitor. Adding this permission grants users read and write permissions to monitor and alert on HBase instances within the policy scope, such as viewing instance monitoring data and adding alert policies. |
   ||CloudMonitorReadOnlyAccess |Read\-only access to Cloud Monitor. Adding this permission allows the user to view monitoring data for HBase instances within the policy scope. |
   |Tag service (Optional) |TagFullAccess |This policy allows you to manage tag\-related services in your account, such as querying by tag. <br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To allow a sub\-account to see existing tags from the main account in the key and value drop\-down lists when tagging an HBase instance, you must grant this permission at the <strong>global</strong> scope. Without it, the drop\-down lists will be empty for the sub\-account.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">sub\-accounts can add new tags to instances even without the <code>TagFullAccess</code> permission. For details on adding tags, see <a href="https://docs.byteplus.com/en/docs/HBase/Associating_or_adding_tag">Associating or adding tag</a>.</div><br> |
   

* **Custom policy**: a fine\-grained set of permissions for resource management that you create manually. If system\-defined policies do not meet your requirements, you can create custom policies to define permissions with fine\-grained control. For details, see [Creating a user custom policy](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-custom-policy).


<span id=".5L2c55So6IyD5Zu0"></span>
### Scope

After selecting a policy, you can specify its scope for sub\-accounts:


* **Global permissions**: once added, the permission policy applies to all projects in the account, including any future projects.

* **Project permissions**: after adding project permissions, the user's policy only applies to resources within the specified project.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [HBase console](https://console.byteplus.com/db/hbase) using the primary account and click **IAM** in the personal center in the upper right corner.

2. In **IAM** \> **User management**  **\> User** page, click **Creste new user**.

3. On the **Create user** page,  enter the basic information.

4. In the **Permission settings** wizard, configure permission policies and scopes for the user.

   
   |Granted permission type |Permission policy |
   |---|---|
   |Management permissions |To grant sub\-account management permissions for HBase, you need to grant the following permissions.<br><br><br>* Add `CloudMonitorFullAccess` as global permission.<br><br>* `VPCFullAccess` and `HBaseFullAccess` can be added as global permissions (administrative permissions for all projects) or project permissions (administrative permissions for specified projects). |
   |Read\-only permissions |To grant sub\-accounts read\-only permissions for HBase, grant them the following permissions.<br><br><br>* Add `CloudMonitorReadOnlyAccess` as global permission.<br><br>* `VPCReadOnlyAccess` and `HBaseFullAccess` can be added as global permissions (read\-only access to all projects) or project\-level permissions (read\-only access to specific projects). |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After a sub\-account is created, you can modify its permission policy at any time. For details, see <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-user-management">Managing users</a>.   </div>
