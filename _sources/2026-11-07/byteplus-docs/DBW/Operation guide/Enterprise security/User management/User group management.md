---
title: "User group management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/User_group_management"
---

Database Workshop (DBW) provides user group management. By assigning BytePlus sub\-users to user groups, you can uniformly assign permissions and settings to all members of the group.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* After setting the daily execution limit and daily query row limit for DBW system role users, the remaining execution times and query rows are displayed in the upper right corner of the SQL execution area when the DBW system role users log in to the database interaction console.

* When deleting a user group, if the users in the user group have modified personal user permissions, have been added as approval nodes of the approval workflow, or have been set as the Instance DBA or Owner of the instance, the personal user will not be deleted when the user group is deleted.

* When you synchronize user group information, only the user group information of users who add BytePlus account is synchronized according to the project they belong to.

* Within a single region, a tenant can add up to 200 user groups.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

BytePlus sub\-users have been created. 

<span id=".5Yib5bu655So5oi357uE"></span>
## Create user group


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Corporate security** \> **User management**.

4. On the **User management** page, click **User group management**.

5. On the **User group management** tab, click **Add user group**.

6. In the **Add user group** panel, configure the following parameter information.

   
   |**Type** |**Parameter** |**Description** |
   |---|---|---|
   |**User group information** |**User group name** |Customize the user group name, which can contain up to 128 characters. |
   ||**Description** |(Optional) Customize remarks for the user group, which can contain up to 256 characters. It is recommended that the description be related to the business. |
   ||**Add BytePlus account** |Select a way to add a BytePlus account as needed. The following two methods are supported:<br><br><br>* **Directly select**: Select the sub\-users to add from the drop\-down list.<br><br>* **Select based on the project it belongs to**: Select the project to which the sub\-user to be added belongs from the drop\-down list.  |
   ||**Select IAM user group** |Select the IAM user group as needed. You can also select all users under the project that are not in the user group. |
   ||**Change synchronization policy** |Check whether to synchronize user changes in the project as needed. You can **not synchronize** or **periodically synchronize**. If you select periodic synchronization, user changes will be synchronized from the project at 0:00 (GMT+0) every day. For example, if users or user groups are added or removed from the project, the users in the DBW user group will follow the user changes in the project at 0:00 every day. |
   |**Role and SQL window permissions** |**DBW role** |Select a DBW role as required. You can select **Administrator** or **Normal user**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For detailed information about DBW roles, see <a href="https://docs.byteplus.com/en/docs/DBW/role-description">Role description</a>.</div><br> |
   ||**Maximum number of queries per day** |Set the upper limit of the number of daily executions of the DBW role as required. The default value is 20000, and the value range is 1~999999999.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To execute SQL, the SQL execution permission of the database object must be authorized for the user.</div><br> |
   ||**Queries expiration time** |Set the validity period for the maximum number of daily queries. Currently, the options include **Permanent valid**, **Valid for 6 months**, **Valid for 3 months** (default), **Valid for 1 month**, **Valid for 2 weeks**, **Valid for 7 days**, **Valid for the day**, and **Customize**. The default validity period is **Valid for 3 months**. |
   ||**Daily query row limit** |Set the upper limit on the number of rows queried daily for the DBW role as needed. The default value is 20000, and the value range is 1~999999999.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To query SQL, the SQL query permission of the database object must be authorized for the user.</div><br> |
   ||**Query row validity period** |Set the validity period for the daily query row limit. Currently, the options include **Permanent valid**, **Valid for 6 months**, **Valid for 3 months (default)** , **Valid for 1 month**, **Valid for 2 weeks**, **Valid for 7 days**, **Valid for the day**, and **Customize**. The default validity period is **valid for 3 months**. |
   

7. Click **OK**.


<span id=".5o6I5p2D55So5oi357uE"></span>
## Authorize user groups

After a user group is created, you can grant the user group operation permissions for the specified instance. The detailed operations are as follows:


* Grant operation permissions for RDS for MySQL instances, databases, tables, and columns to the user group. For detailed steps, refer to [Granting operation permissions for RDS for MySQL to user groups](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql).

* Grant operation permissions for veDB for MySQL instances, databases, tables, and columns to the user group. For detailed steps, refer to [Granting operation permissions for veDB for MySQL to user groups](https://docs.byteplus.com/en/docs/DBW/Granting_system_role_operation_permissions).

* Grant operation permissions for RDS for PostgreSQL instances, databases, tables, and columns to the user group. For detailed steps, refer to [Granting operation permissions for RDS for PostgreSQL to user groups](https://docs.byteplus.com/en/docs/DBW/Granting_operation_permissions_for_system_roles).

* Grant operation permissions for RDS for SQL Server instances, databases, tables, and columns to the user group. For detailed steps, refer to [Granting operation permissions for RDS for SQL Server to user groups](https://docs.byteplus.com/en/docs/DBW/Granting_operation_permissions_for_system_roles).

* Grant operation permissions for Cache for Redis instances to the user group. For detailed steps, refer to [Granting operation permissions for Cache for Redis to the user](https://docs.byteplus.com/en/docs/DBW/granting_operation_permissions_for_system_roles_for_redis?lang=en).


<span id=".57yW6L6R55So5oi357uE"></span>
## Synchronize user group

DBW provides a one\-click synchronization function for user groups, which supports real time synchronization of user changes from the project, such as adding or reducing users or user groups in the project. After synchronizing user group information, the users in the DBW user group will also be consistent with the users in the project.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Corporate security** \> **User management**.

4. On the **User management** page, click **User group management**.

5. On the **User group management** tab, click **Synchronize user group information**.

6. In the dialog box, click **OK**.


<span id=".57yW6L6R55So5oi357uE"></span>
## Edit user group


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Corporate security** \> **User management**.

4. On the **User management** page, click **User group management**.

5. On the **User group management** tab, click **Edit** in the **Actions** column of the target user group.

6. In the editing user control panel, configure **User group information** and **Role and SQL window permissions**. For more parameter information, see Create user group.

7. Click **OK**.


<span id=".5Yig6Zmk55So5oi357uE"></span>
## Delete user group

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After the deletion, the personal users automatically created under the user group will continue to be reserved, but their permissions will be revoked.</div>


* <div data-tips="true" data-tips-type="tip">When deleting a user group, if the personal users in the user group have not performed the following operations, they will be deleted together with the user group:</div>


   * <div data-tips="true" data-tips-type="tip">Permissions have not been modified separately.</div>


   * <div data-tips="true" data-tips-type="tip">Not added as an approval node.</div>


   * <div data-tips="true" data-tips-type="tip">Not set as an instance DBA or instance Owner.</div>


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Corporate security** \> **User management**.

4. On the **User management** page, click **User group management**.

5. On the **User Group Management** tab, in the **Actions** column of the target user, choose  **...**  \> **Delete**.

6. In the **Confirm Deletion** dialog box, click **Delete**.


<span id=".5p-l55yL55So5oi357uE"></span>
## View user group


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Corporate security** \> **User management**.

4. On the **User management** page, click **User group management**.

5. On the **User Group Management** tab, view the created user group information, including **User group name**, **User group ID**, **Number of users included**, **Description**, **DBW role**, **Daily execution limit**, **Daily query row limit**, and other information.

   1. You can also select  **...**  in the **Actions** column of the target user group. To view **Permission Details**, see the permission information for the user group.

   2. You can view your expiration time in the **Daily Execution Limit** and **Daily Query Row Limit** columns.
