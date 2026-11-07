---
title: "Granting operation permissions for system roles"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/granting_operation_permissions_for_system_roles_for_redis"
---

Database Workshop (DBW) supports unified management of database instances and collaborative management through multiple roles, such as system roles and ticket approval roles. This simplifies and standardizes database management and improves enterprise security efficiency. This topic describes how to grant operation permissions for DBW system roles on the Database Workshop (DBW) console.

<span id="UurYWyuV"></span>
### Prerequisites

The instance has enabled security control. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-redis?lang=zh).

<span id="aKEvTvoa"></span>
### Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **User management**.

4. On the User management page, select the authorization target as needed:

   
   <Tabs>
   <Tab zoneid="uKZFVMiWvn" title="Authorize personal users">
   <TabTitle>Authorize personal users</TabTitle>
   
   * Authorize specific users
   
      On the **Personal user management** tab, click **Permission management** in the **Actions** column of the target user, then select the permissions to authorize.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e5a25c6e222dd511f2d5c3cb42628cdb.png) </span>
   
   * Batch authorize users
   
      1. On the **Personal user management** tab, select the target users to be authorized as needed.
   
      2. Click **Batch authorize** in the bottom menu bar and select the permissions to be granted.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5dab7b19e135f6730cd25ff2d4f99fe5.png) </span><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d18379c60b3f7fe829b3e9966f98a19b.png) </span>
   
   
   
   
   
   </Tab>
   <Tab zoneid="ZXD66rPgxg" title="Authorize users in user groups">
   <TabTitle>Authorize users in user groups</TabTitle>
   
   1. On the **User management** page, click **User group management**.
   
   2. On the **User group management** subtab, click **Permission management** in the **Actions** column of the target user group, then select the permissions to authorize.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_814ea22ccfebf99ef8743702487f1cf1.png) </span>
   
   
   </Tab>
   </Tabs>
   

5. In the newly opened control panel, configure the following parameters:

   
   |**Authorization type** |**Parameter** |**Description** |
   |---|---|---|
   |**Authorize instance** |**Database instance** |Select **Cache for Redis**. |
   ||**Authorization method** |Select an authorization method as required. You can select instances to be authorized by **Directly select** or **Select based on the project it belongs to**. |
   ||**Authorize instance** |Check the instance to be authorized from the drop\-down list. Multiple selections are supported.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The dropdown list only displays instances with security control enabled in the current region.</div><br> |
   ||**Permission type** |Check the permission type as needed. Currently, the following options are supported.<br><br><br>* **SQLchange**: Refers to operations that add, modify, or delete data in the database.<br><br>* **SQL query**: Refers to the operation of retrieving the required data from the database.<br><br>* **Structural change**: Represents operations that can modify, add, or delete a database structure.<br><br>* **Operation and maintenance read\-only**: Refers to read\-only permissions for operation and maintenance management capabilities, such as viewing real\-time sessions and slow SQL analysis lists.<br><br>* **Operation and maintenance read/write**: Refers to full permissions for operation and maintenance management capabilities, such as Kill sessions and creating SQL rate limiting tasks.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>SQL change</strong>, <strong>SQL query</strong>, and <strong>Schema change</strong> can be checked or unchecked together, but not individually.</div><br> |
   ||**Effective time** |Select the validity period of the authorization from the drop\-down list, with options including **1 month** (default), **3 months**, **6 months**, and **1 year**. Additionally, custom days can be set as the validity period, with a default of 1 day and a range of [1, 365]. |
   

6. Click **OK**.
