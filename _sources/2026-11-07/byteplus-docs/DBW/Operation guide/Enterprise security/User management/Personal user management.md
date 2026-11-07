---
title: "Personal user management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Personal_user_management"
---

This topic describes how to manage DBW roles.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* When you activate Database Workshop, the Volcengine account (primary account) is initialized as an **Administrator** role, namely RootAccount. This account has all function permissions of DBW by default and does not support modification or deletion.

* When you first log in to DBW's User management with a BytePlus IAM user that has the `AdministratorAccess` permission policy, follow the prompts to authorize DBW to access the official IAM configuration. DBW will then automatically initialize the IAM user as an administrator role.

* IAM users who have been added as administrators may not have the `AdministratorAccess` permission policy, but this does not affect the IAM user's normal use of DBW functions.

* An administrator can add multiple normal users.

* Only accounts with the system role of Administrator support adding, editing, and deleting users.

* Users added through the DBW can be set as administrators.

* After setting the daily execution limit and daily query row limit for an IAM user, the remaining execution times and query rows are displayed in the upper right corner of the SQL execution area when the IAM user logs in to the database interaction console.

* When deleting a user, pay attention to the following information:

   * After deleting a user, the user will no longer be able to perform ticket\-related operations. Proceed with caution.

   * Before you delete user, ensure that the user is not bound to an approval node. If bound, unbind the Approval node first; otherwise, the approval process may get stuck. For detailed operations, see [Approval node management](https://docs.byteplus.com/en/docs/DBW/Approval_node_management) and [Approval workflow management](https://docs.byteplus.com/en/docs/DBW/Approval_workflow_management).


<span id=".6ZmQ5Yi26K-05piO"></span>
## Description


|Primary account |IAM user ||
|---|---|---|
||Administrator |Normal user |
|You can add users as DBW roles and grant them operation permissions for DBW roles |You can add users as DBW roles and grant them operation permissions for DBW roles |Adding users as DBW roles and granting them permissions for DBW roles is not supported |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A user has been created. 

<span id=".5re75Yqg55So5oi3"></span>
## Add user


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Corporate security** \> **User management**.

4. On the **User management** page, click **Add user**.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Volcano account** |Select the users you want to add from the drop\-down list. Batch selection of multiple users is supported. Adding by searching for a username is supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For users added in batch, the DBW role, daily execution limit, daily query row limit, and valid period are all the same.</div><br> |
   |**DBW role** |Select a DBW role as needed. The values are as follows:<br><br><br>* **Administrator**: By default, administrators can access all DBW features.<br><br>* **Normal user**: Normal users can access some DBW features.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For details about DBW roles, see <a href="https://docs.byteplus.com/en/docs/DBW/role-description">Role description</a>.</div><br> |
   |**Maximum number of queries per day** |Set the upper limit on the number of execution times for the DBW role per day as needed. The default value is 2,000, and its range is 1 to 999,999,999.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To execute SQL, you must also authorize the user with SQL execution permissions for the database object.</div><br> |
   |**Queries expiration time** |Set the validity period for the maximum number of daily queries. Currently, the options include **Permanent valid**, **Valid for 6 months**, **Valid for 3 months** (default), **Valid for 1 month**, **Valid for 2 weeks**, **Valid for 7 days**, **Valid for the day**, and **Customize**. The default validity period is **Valid for 3 months**. |
   |**Daily query row limit** |Set the upper limit on the number of rows queried daily by the DBW role as needed. The default value is 2,000, and its range is 1 to 999,999,999.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To support SQL query, the SQL query permission of the database object needs to be authorized by the user at the same time.</div><br> |
   |**Query row validity period** |Set the validity period for the daily query row limit. Currently, the options include **Permanent valid**, **Valid for 6 months**, **Valid for 3 months (default)** , **Valid for 1 month**, **Valid for 2 weeks**, **Valid for 7 days**, **Valid for the day**, and **Customize**. The default validity period is **valid for 3 months**. |
   

5. Click **OK**.


<span id=".5o6I5p2D55So5oi3"></span>
## Authorize the user

After the user is added, you can grant the user the operation permissions of the specified instance. The detailed operations are as follows:


* Grant operation permissions for RDS for MySQL instances, databases, tables, and columns to the user. For detailed steps, refer to [Granting operation permissions for RDS for MySQL to the user](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql).

* Grant operation permissions for veDB for MySQL instances, databases, tables, and columns to the user. For detailed steps, refer to [Granting operation permissions for veDB for MySQL to the user](https://docs.byteplus.com/en/docs/DBW/Granting_system_role_operation_permissions).

* Grant operation permissions for RDS for PostgreSQL instances, databases, tables, and columns to the user. For detailed steps, refer to [Granting operation permissions for RDS for PostgreSQL to the user](https://docs.byteplus.com/en/docs/DBW/Granting_operation_permissions_for_system_roles).

* Grant operation permissions for RDS for SQL Server instances, databases, tables, and columns to the user. For detailed steps, refer to [Granting operation permissions for RDS for SQL Server to the user](https://docs.byteplus.com/en/docs/DBW/Granting_operation_permissions_for_system_roles).

* Grant operation permissions for Cache for Redis instances to the user group. For detailed steps, refer to [Granting operation permissions for Cache for Redis to the user](https://docs.byteplus.com/en/docs/DBW/granting_operation_permissions_for_system_roles_for_redis?lang=zh).


<span id=".57yW6L6R55So5oi3"></span>
## Edit user


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **User management**.

   
   <Tabs>
   <Tab zoneid="NeLJom3RcT" title="Edit the specified user">
   <TabTitle>Edit the specified user</TabTitle>
   
   1. On the **User management** page, click **Edit** in the Actions column of the target user.
   
   2. In the **Edit user** control panel, modify the **DBW role**, **Maximum number of queries per day**, **Queries expiration time**, **Daily query row limit**, and **Query row validity period**.
   
   
   </Tab>
   <Tab zoneid="H4XmCJa38A" title="Batch edit users">
   <TabTitle>Batch edit users</TabTitle>
   
   1. On the **User management** page, select the users you want to edit as needed, and click **Edit user** in the bottom menu bar.
   
   2. On the **Edit user** control panel, click **Reset** after **Maximum number of queries per day**, **Queries expiration time**, **Daily query row limit**, or **Query row validity period**, and edit the user as needed.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Batch modification of user DBW roles is not supported currently.   </div>
      
   
   
   </Tab>
   </Tabs>
   

4. Click **OK**.


<span id=".5Yig6Zmk55So5oi3"></span>
## Delete user

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After deleting a user, the user will no longer be able to perform ticket\-related operations. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="tip">If a prompt indicates that the user cannot be deleted when deleting the user, you can hover your mouse over cannot delete to view the reason why the deletion is not possible. Reasons for being unable to delete a user include the following two:</div>


   * <div data-tips="true" data-tips-type="tip">Before deleting a user, ensure that the user is not bound to the approval node. If bound, it is suggested to unbind the approval node first; otherwise, you cannot delete the user. For detailed operations, see <a href="https://docs.byteplus.com/en/docs/DBW/Approval_node_management">Approval node management</a> and <a href="https://docs.byteplus.com/en/docs/DBW/Approval_workflow_management">Approval workflow management</a>.</div>


   * <div data-tips="true" data-tips-type="tip">Before deleting a user, make sure that the user is not the instance's resource role, that is, the instance's DBA or owner. If it is the instance's resource role, it is recommended to modify the instance's resource role first, otherwise the user cannot be deleted. For details, refer to <a href="https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql">Enabling instance security control (RDS for MySQL)</a>, <a href="https://docs.byteplus.com/en/docs/DBW/Enabling_security_control">Enabling instance security control (veDB for MySQL)</a>, <a href="https://docs.byteplus.com/en/docs/DBW/enabling-security-control">Enabling instance security control (RDS for PostgreSQL)</a>, <a href="https://docs.byteplus.com/en/docs/DBW/enabling-security-control_">Enabling instance security control (RDS for SQL Server)</a>, and <a href="https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-redis?lang=zh">Enabling instance security control (Cache for Redis)</a>.</div>


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **User management**.

   
   <Tabs>
   <Tab zoneid="l09qmlQQDC" title="Delete the specified user">
   <TabTitle>Delete the specified user</TabTitle>
   
   1. On the **User management ** page, select  **...** \> **Delete** in the Actions column of the target user.
   
   2. In the **Are you sure you want to delete the selected user?**  dialog box, click **Delete**.
   
   
   </Tab>
   <Tab zoneid="PL0xuG0WxE" title="Batch delete users">
   <TabTitle>Batch delete users</TabTitle>
   
   1. On the **User management** page, select the users you want to delete as needed.
   
   2. Click **Delete user** in the bottom menu bar.
   
   3. In the **Are you sure you want to delete the selected user?**  dialog box, click **Delete**.
   
   
   </Tab>
   </Tabs>
   


<span id=".5p-l55yL55So5oi3"></span>
## View user


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **User management**.

4. On the **User management** page, view the added user information, including **Username**, **Account ID**, **DBW role**, **Daily execution limit**, and **Daily query row limit**.

   * You can also select  **...** \> **Permission details** in the **Actions** column of the target user to view their permissions.

   * You can view your expiration time in the **Daily execution limit** and **Daily query row limit** columns.
