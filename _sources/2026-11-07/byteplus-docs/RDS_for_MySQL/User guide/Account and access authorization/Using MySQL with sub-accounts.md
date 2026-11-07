---
title: "Using MySQL with sub-accounts"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/using_mysql_as_sub-user"
---

Each admin account can create multiple sub\-accounts and grant different permissions to different sub\-accounts to manage the access rights of different identities under the account to cloud resources. This article introduces the relevant content of using MySQL services through sub\-accounts.

<span id="applicable-scenarios"></span>
## Applicable scenarios

**Independent resource management scenarios**: Create different sub\-accounts for different businesses and access resources belonging to different businesses through sub\-accounts.

**Security issues**: Using the AK/SK of the sub\-account to call the Open API interface can effectively avoid the risk of leakage of the master account AK/SK.

<span id="background-information"></span>
## Background information

<span id="policy"></span>
### Policy

Policy is a description of permissions. IAM users, user groups or roles must be granted permissions through associated policies. For sub\-accounts using MySQL, you can add system preset policies or custom policies to sub\-accounts as needed.


* System Preset Policy



|Associated Service |Policy Name |Policy Type |Description |
|---|---|---|---|
|RDS for MySQL |RDSMySQLFullAccess |System Preset Policy |Full management permissions for RDS for MySQL. After adding this permission, the user will have read and write permissions for RDS for MySQL within the scope of the policy, such as creating, deleting, and editing instances.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div><br><br><br><div data-tips="true" data-tips-type="tip">If the user only obtains this permission, he cannot use all the functions of the MySQL instance. If you need to use private network related functions, you need to obtain <code>VPCFullAccess</code> or <code>VPCReadOnlyAccess</code> permissions; if you need to use the monitoring and alarm functions, you need to obtain <code>CloudMonitorFullAccess</code> or <code>CloudMonitorReadOnlyAccess</code> permissions; if you need to use the autonomous service function, you need to obtain <code>DbwFullAccess</code> permissions.</div><br> |
||RDSMySQLReadOnlyAccess |System Preset Policy |Read\-only access to the RDS for MySQL. After adding this permission, the user can view the MySQL instance within the policy scope. |
|Private network |VPCFullAccess |System Preset Policy |Full management permissions for private networks (VPC). After adding this permission, the user will have read and write permissions for private networks within the policy scope, such as creating private networks, binding private networks or subnets to MySQL instances, etc. |
||VPCReadOnlyAccess |System Preset Policy |Read\-only access to private networks (VPC). After adding this permission, the user can view the private network and subnet information of MySQL instances within the policy scope. |
|CloudMonitor |CloudMonitorFullAccess |System Preset Policy |Full management permissions for CloudMonitor. After adding this permission, the user will have read and write permissions for the monitoring alarms of the MySQL instance within the policy scope, such as viewing the monitoring data of the instance, adding alarm policies for the instance, etc. |
||CloudMonitorReadOnlyAccess |System Preset Policy |Read\-only access permission for CloudMonitor. After adding this permission, the user can view the monitoring data of the MySQL instance within the policy scope.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div><br><br><br><div data-tips="true" data-tips-type="tip">If the sub\-account needs to view the monitoring information, you need to add this permission for the sub\-account globally.</div><br> |
|Database Workbench |DbwFullAccess |System Preset Policy |Full management permissions for the Database Workbench (DBW). After adding this permission, the user will have read and write permissions for the Database Workbench within the policy scope, such as using the data interaction platform function and the observation diagnosis function.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div><br><br><br><div data-tips="true" data-tips-type="tip">sub\-accounts with <code>DBWFullAccess</code> permission will have management permissions for MySQL instances within the scope of authorization (project or global), and are not subject to <code>MYSQLFullAccess</code>. Please authorize with caution.</div><br> |
|Billing Center |BillingCenterFullAccess |System Preset Policy |Full read and write permissions for the billing center, including management permissions for all pages of the billing center and related OpenAPIs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div><br><br><br><div data-tips="true" data-tips-type="tip">sub\-accounts can unsubscribe instances only after <code>BillingCenterFullAccess</code> permission is granted globally.</div><br> |



* Custom Policy In addition to using the system preset policies listed in the table above to authorize sub\-accounts, you can also define more specific control policies through custom policies. For more details about custom policies,. see [Policy Overview](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-policies).


<span id="scope"></span>
### Scope

After selecting a policy, you can specify the scope of the policy for the user as needed.


* **Global**: The permission policy obtained by the user will take effect globally.

* **Specified Project**: The permission policy obtained by the user will take effect in the specified project.


<span id="operation-steps"></span>
## Operation steps


1. Log in to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql) with the main user account, and click **Access Control** in the Personal Center in the upper right corner.

2. On the **Access Control**\>**Identity Management**\>**User** page, click **New User**.

3. On the **Create User** page, finish the operation to create a user according to \- [Creating a user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">After selecting the method to create a user, you need to add permission policies for the user and set the scope of the policy during the creation process. For more information about permission selection, see [Background Information](#Background Information).</div>



4. (Optional) Create an AK/SK for the sub\-account. For details on creating an AK/SK,. see [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).
