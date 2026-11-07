---
title: "Granting operation permissions for system roles"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Granting_operation_permissions_for_system_roles"
---

Database Workshop (DBW) supports unified management of database instances and collaborative management through multiple roles, such as system roles and ticket approval roles. This simplifies and standardizes database management and improves enterprise security efficiency. This topic describes how to grant operation permissions for DBW system roles on the Database Workshop (DBW) console.

<span id="K9HJ3KSS"></span>
## Prerequisites

The instance has enabled security control. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/MongoDB_Enabling_security_control).

<span id="h6G9hYgs"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **User management**.

4. On the **User management** page, select the authorization target as needed:

   * Authorize personal users

      * Authorize permissions for specified users:

         1. On the **User management** page, click **Personal user management**.

         2. On the **Personal user management** sub\-tab, click **Permission management** in the **Actions** column of the target user, and select the permissions to be granted.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9d5f7a11897ef6d7e153d33ec0d5bef2.png) </span>

      * Batch authorize user permissions:

         1. On the **User management** page, click **Personal user management**.

         2. On the **Personal user management** sub\-tab, select the users to be authorized as needed. Click **Batch Authorize** in the bottom menu bar, and select the permissions to be authorized.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e379cd5c6909dc05bec6245f5b6fe994.png) </span>

   * Authorize user groups

      1. On the **User management** page, click **User group management**.

      2. On the **User group management** sub\-tab, click **Permission management** in the **Actions** column of the target user group, and select the permissions to be granted.

      3. In the displayed control panel, configure the following information.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3"><strong>Document Database for MongoDB</strong> currently only supports Authorize instance.         </div>
         

         
         |**Authorization type** |**Parameter** |**Description** |
         |---|---|---|
         |**Authorize instance** |**Database instance** |Select **Document Database for MongoDB**. |
         ||**Authorization method** |Select an authorization method as required. You can select instances to be authorized by **Directly select** or **Select based on the project it belongs to**. |
         ||**Authorize instance** |Check the instance to be authorized from the drop\-down list. Multiple selections are supported. |
         ||**Permission type** |Check the permission type as needed. Currently, the following options are supported.<br><br><br>* **SQL change**: Refers to operations that add, modify, and delete data in the database.<br><br>* **SQL query**: Refers to the operation of retrieving the required data from the database.<br><br>* **Structural change**: Represents operations that can modify, add, or delete a database structure.<br><br>* **Operation and maintenance read\-only**: Refers to read\-only permissions for operation and maintenance management capabilities, such as viewing real\-time sessions and database audit logs.<br><br>* **Operation and maintenance read/write**: Refers to full permissions for operation and maintenance management capabilities, such as Kill sessions. |
         ||**Effective time** |Select the validity period of the authorization from the drop\-down list, with options including **1 month** (default), **3 months**, **6 months**, and **1 year**. Additionally, custom days can be set as the validity period, with a default of 1 day and a range of [1, 365]. |
         

      4. Click **OK**.
