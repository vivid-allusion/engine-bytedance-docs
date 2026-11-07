---
title: "Granting system role operation permissions"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Granting_system_role_operation_permissions"
---

Database Workshop (DBW) supports unified management of database instances and enables collaborative management through multiple roles such as system roles and ticket approval roles, simplifying and standardizing database management operations, and enhancing enterprise security efficiency. This topic explains how to grant system role operation permissions in the Database Workbench DBW console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

If you need to authorize a user, you must enable security control for the instance. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Enterprise security** \> **User management**.

4. On the **User management** page, select the authorization target as needed:

   * Authorize individual users

      * Authorize specific user permissions:

         1. On the **User management** page, click **Individual user management**.

         2. On the **Individual user management** sub\-tab, click **Permission management** under the **Actions** column of the target user, and select the permissions to be authorized.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63479b8e1950423af7ceb0f697a88b19.png) </span>

      * Batch authorize user permissions:

         1. On the **User management** page, click **Individual user management**.

         2. On the **Individual user management** sub\-tab, select the users to be authorized as needed, click **Batch authorize** in the bottom menu bar, and select the permissions to be authorized.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ddc88c3becc7f3adda753f0a08124209.png) </span>

   * Authorize user groups

      1. On the **User management** page, click **User group management**.

      2. On the **User group management** subtab, click **Permission management** under the **Actions** column of the target user group to select the permissions to be granted.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b434e7e4e6f70d13693170c3ee52fee5.png) </span>

5. On the opened control panel, configure the following information.

   
   |**Authorization type** |**Parameter** |**Description** |
   |---|---|---|
   |**Authorization instance** |**Database instance** |Select **NDB** ** for MySQL**. |
   ||**Authorization method** |Choose the authorization method as needed, supporting two ways: **Direct selection** and **Selection based on the project** to choose the instances to be authorized. |
   ||**Authorized instance** |Check the instances that require authorization from the dropdown list. Multiple selections are supported. |
   ||**Permission type** |Select the permission types as needed. Currently, the following options are supported:<br><br><br>* **SQL** **change**: Refers to operations that add, modify, or delete data in the database. SQL statement types include `CREATE`, `ALTER`, `DROP`, `UPDATE`, `INSERT`, and `DELETE`.<br><br>* **SQL** **query**: Refers to the operation of retrieving required data from a database. SQL statement types include `SELECT`, `SHOW`.<br><br>* **Structural change**: Refers to the operation of modifying, adding, or deleting database structures. SQL statement types include `ALTER TABLE`, `CREATE INDEX`, `DROP INDEX`.<br><br>* **Ops read\-only**: Refers to read\-only permissions for operational management capabilities, such as viewing real\-time sessions and slow SQL analysis lists.<br><br>* **Ops read\-write**: Refers to full permissions for operational management capabilities, such as killing sessions and creating SQL throttling tasks. |
   ||**Validity period** |Select the validity period of the authorization from the dropdown list, with options including **1 month** (default), **3 months**, **6 months**, and **1 year**. Additionally, custom days can be set as the validity period, defaulting to 1 day, with a value range of [1, 365]. |
   |**Authorization database** |**Database instance** |Select **NDB** ** for MySQL**. |
   ||**Authorization instance** |Select the instances to be authorized from the dropdown list. |
   ||**Authorization database** |Select the databases to authorize from the dropdown list, multiple selections are supported. |
   ||**Permission type** |Check the permission types as needed, currently supporting the following options:<br><br><br>* **SQL** **modification**: Refers to operations that add, modify, or delete data in the database. SQL statement types include `CREATE`, `ALTER`, `DROP`, `UPDATE`, `INSERT`, and `DELETE`.<br><br>* **SQL** **query**: Refers to the operation of retrieving the required data from a database. SQL statement types include `SELECT`, `SHOW`.<br><br>* **Schema change**: Refers to the operation of modifying, adding, or deleting the database structure. SQL statement types include `ALTER TABLE`, `CREATE INDEX`, `DROP INDEX`. |
   ||**Validity period** |Select the validity period of the authorization from the dropdown list, including **1 month** (default), **3 months**, **6 months**, and **1 year**. Additionally, you can set a custom number of days as the validity period, with a default of 1 day and a range of [1, 365]. |
   |**Authorization table** |**Database instance** |Select **NDB** ** for MySQL**. |
   ||**Authorization instance** |Select the instances to authorize from the dropdown list. |
   ||**Authorization database** |Check the database to be authorized from the dropdown list. |
   ||**Authorization table** |Check the tables to be authorized from the dropdown list. Multiple selections are supported. |
   ||**Permission type** |Select the permission types as needed. The following options are currently supported:<br><br><br>* **SQL** **change**: Refers to operations that add, modify, or delete data in the database. SQL statement types include `CREATE`, `ALTER`, `DROP`, `UPDATE`, `INSERT`, and `DELETE`.<br><br>* **SQL** **query**: refers to the operation of retrieving the required data from the database. SQL statement types include `SELECT`, `SHOW`.<br><br>* **Schema change**: refers to the operation of modifying, adding, or deleting the database structure. SQL statement types include `ALTER TABLE`, `CREATE INDEX`, `DROP INDEX`. |
   ||**Validity period** |Select the validity period of the authorization from the dropdown list, including **1 month** (default), **3 months**, **6 months**, and **1 year**. Additionally, you can set a custom number of days as the validity period, with a default of 1 day and a range of [1, 365]. |
   |**Authorization column** |**Database instance** |Select **NDB** ** for MySQL**. |
   ||**Authorize instance** |Select the instances to be authorized from the dropdown list. |
   ||**Authorize database** |Check the database to be authorized from the dropdown list. |
   ||**Authorization table** |Check the tables to be authorized from the dropdown list. |
   ||**Authorization column** |Check the columns to be authorized from the dropdown list. Multiple selections are supported. After selecting the instance, database, table, and columns as needed, click **Add** to include the column permissions in the user permissions. |
   ||**Permission type** |Select the permission type as needed. The following options are currently supported:<br><br><br>* **SQL** **modification**: Refers to operations that add, modify, or delete data in a database. SQL statement types include `CREATE`, `ALTER`, `DROP`, `UPDATE`, `INSERT`, and `DELETE`.<br><br>* **SQL** **query**: Refers to the operation of retrieving the required data from a database. SQL statement types include `SELECT`, `SHOW`.<br><br>* **Structural modification**: Refers to operations that modify, add, or delete the structure of a database. SQL statement types include `ALTER TABLE`, `CREATE INDEX`, `DROP INDEX`. |
   ||**Validity period** |Select the validity period for authorization from the dropdown list. Options include **1 month** (default), **3 months**, **6 months**, and **1 year**. Additionally, you can set a custom number of days as the validity period, with a default of 1 day and a range of [1, 365]. |
   

6. Click **OK**.


<span id=".5p-l55yL55So5oi35p2D6ZmQ"></span>
## View User Permissions


1. Log on to the [DBW Console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Enterprise security** \> **User management**.

4. On the **User management** page, select  **...**  under the operation column of the target user. \> **Permission details**.

5. In the upper right corner of the **Permission details** dialog, switch the database type to **NDB** ** for MySQL** as needed to view all permissions owned by the target user, including instance, database, table, and column permissions.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">On the target permissions tab, you can also release unnecessary permissions as needed.</div>


You can also view all permissions under the current account on the My Permissions page. For detailed steps, refer to [Viewing my permissions](https://docs.byteplus.com/en/docs/DBW/Viewing_my_permissions).
