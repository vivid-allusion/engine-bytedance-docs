---
title: "Granting operation permissions for system roles"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql"
---

Database Workshop (DBW) supports unified management of database instances and collaborative management through multiple roles, such as system roles and ticket approval roles. This simplifies and standardizes database management and improves enterprise security efficiency. This topic describes how to grant operation permissions for DBW system roles on the Database Workshop (DBW) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The instance has enabled security control. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **User management**.

4. On the **User management** page, select the authorization target as needed:

   * Authorize personal users

      * Authorize permissions for specified users:

         1. On the **User management** page, click **Personal user management**.

         2. On the **Personal user management** sub\-tab, click **Permission management** in the **Actions** column of the target user, and select the permissions to be granted.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b243d74411aaf0b25455f8891764630c.png) </span>

      * Batch authorize user permissions:

         1. On the **User management** page, click **Personal user management**.

         2. On the **Personal user management** sub\-tab, select the users to be authorized as needed. Click **Batch Authorize** in the bottom menu bar, and select the permissions to be authorized.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7286a4793ac2859c4ca4aadeb0470cc3.png) </span>

   * Authorize user groups

      1. On the **User management** page, click **User group management**.

      2. On the **User group management** sub\-tab, click **Permission management** in the **Actions** column of the target user group, and select the permissions to be granted.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_12eba489369920f42de544dcc7853772.png) </span>

5. In the displayed control panel, configure the following information.

   
   |**Authorization type** |**Parameter** |**Description** |
   |---|---|---|
   |**Authorize instance** |**Database instance** |Select **RDS for MySQL**. |
   ||**Authorization method** |Select an authorization method as required. You can select instances to be authorized by **Directly select** or **Select based on the project it belongs to**. |
   ||**Authorize instance** |Check the instance to be authorized from the drop\-down list. Multiple selections are supported. |
   ||**Permission type** |Check the permission type as needed. Currently, the following options are supported.<br><br><br>* **SQLchange**: Refers to operations that add, modify, and delete data in the database. SQL statement types include `CREATE`, `ALTER`, `DROP`, `UPDATE`, `INSERT`and `DELETE`.<br><br>* **SQL** **query**: Refers to the operation of retrieving the required data from the database. SQL statement types include `SELECT`, and `SHOW`.<br><br>* **Structural change**: Represents operations that can modify, add, or delete a database structure. SQL statement types include `ALTER TABLE`, `CREATE INDEX`, and `DROP INDEX`.<br><br>* **Operation and maintenance read\-only**: Refers to read\-only permissions for operation and maintenance management capabilities, such as viewing real\-time sessions and slow SQL analysis lists.<br><br>* **Operation and maintenance read/write**: Refers to full permissions for operation and maintenance management capabilities, such as Kill sessions and creating SQL rate limiting tasks. |
   ||**Effective time** |Select the validity period of the authorization from the drop\-down list, with options including **1 month** (default), **3 months**, **6 months**, and **1 year**. Additionally, custom days can be set as the validity period, with a default of 1 day and a range of [1, 365]. |
   |**Authorize database**<br><br> |**Database instance** |Select **RDS for MySQL**. |
   ||**Authorize instance** |Check the instance to be authorized from the drop\-down list. |
   ||**Authorize database** |Check the database to be authorized from the drop\-down list.  |
   ||**Permission type** |Check the permission type as needed. Currently, the following options are supported.<br><br><br>* **SQL** **change**: Refers to operations that add, modify, or delete data in the database. SQL statement types include `CREATE`, `ALTER`, `DROP`, `UPDATE`, `INSERT`and `DELETE`.<br><br>* **SQL** **query**: Refers to the operation of retrieving required data from the database. SQL statement types include `SELECT`, and `SHOW`.<br><br>* **Structural change**: Represents operations that can modify, add, or delete a database structure. SQL statement types include `ALTER TABLE`, `CREATE INDEX`, and `DROP INDEX`. |
   ||**Effective time** |Select the validity period of the authorization from the drop\-down list, with options including **1 month** (default), **3 months**, **6 months**, and **1 year**. Additionally, custom days can be set as the validity period, with a default of 1 day and a range of [1, 365]. |
   |**Authorize table** |**Database instance** |Select **RDS for MySQL**. |
   ||**Authorize instance** |Check the instance to be authorized from the drop\-down list. |
   ||**Authorize database** |Check the database to be authorized from the drop\-down list. |
   ||**Authorize table** |Select the tables to be authorized from the drop\-down list. Multiple selections are supported. |
   ||**Permission type** |Check the permission type as needed. Currently, the following options are supported.<br><br><br>* **SQL** **change**: Refers to operations that add, modify, or delete data in the database. SQL statement types include `CREATE`, `ALTER`, `DROP`, `UPDATE`, `INSERT`and `DELETE`.<br><br>* **SQL** **query**: Refers to the operation of retrieving required data from the database. SQL statement types include `SELECT`, and `SHOW`.<br><br>* **Structural change**: Represents operations that can modify, add, or delete a database structure. SQL statement types include `ALTER TABLE`, `CREATE INDEX`, and `DROP INDEX`. |
   ||**Effective time** |Select the validity period of the authorization from the drop\-down list, with options including **1 month** (default), **3 months**, **6 months**, and **1 year**. Additionally, custom days can be set as the validity period, with a default of 1 day and a range of [1, 365]. |
   |**Authorize column** |**Database instance** |Select **RDS for MySQL**. |
   ||**Authorize instance** |Check the instance to be authorized from the drop\-down list.  |
   ||**Authorize database** |Check the database to be authorized from the drop\-down list. |
   ||**Authorize table** |Select the table to be authorized from the drop\-down list. |
   ||**Authorize column** |Select columns to be authorized from the drop\-down list. Multiple selections are supported. After selecting the instance, database, table, and column as needed, click **Add** to include the column permissions in user permissions. |
   ||**Permission type** |Check the permission type as needed. Currently, the following options are supported.<br><br><br>* **SQL** **change**: Refers to operations that add, modify, or delete data in the database. SQL statement types include `CREATE`, `ALTER`, `DROP`, `UPDATE`, `INSERT`and `DELETE`.<br><br>* **SQL** **query**: Refers to the operation of retrieving required data from the database. SQL statement types include `SELECT`, and `SHOW `.<br><br>* **Structural change**: Represents operations that can modify, add, or delete a database structure. SQL statement types include `ALTER TABLE`, `CREATE INDEX`, and `DROP INDEX`. |
   ||**Effective time** |Select the validity period of the authorization from the drop\-down list, with options including **1 month** (default), **3 months**, **6 months**, and **1 year**. Additionally, custom days can be set as the validity period, with a default of 1 day and a range of [1, 365]. |
   

6. Click **OK**.


<span id=".5p-l55yL55So5oi35p2D6ZmQ"></span>
## View user permissions


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **User management**.

4. On the **User management** page, select  **...** \> **Permission details** in the Actions column of the target user.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a8347f52b45de2738e4d331d5ff01d9e.png) </span>

5. In the **Permission details** dialog box, view the permissions of the current user, including instances, tables, databases, and columns.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also release unnecessary permissions on the target permission tab.   </div>
   

You can also view all permissions of the current account on the My permission page. For detailed steps, refer to [Viewing my permissions](https://docs.byteplus.com/en/docs/DBW/Viewing_my_permissions).
