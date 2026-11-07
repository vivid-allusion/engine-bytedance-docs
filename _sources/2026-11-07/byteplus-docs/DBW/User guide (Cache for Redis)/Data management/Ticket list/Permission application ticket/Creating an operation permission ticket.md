---
title: "Creating an operation permission ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket-for-redis"
---

This topic describes how to create an operation permission ticket for applying for a Cache for Redis instance on the Database Workshop (DBW) console.

<span id="lcRmGAvw"></span>
### Prerequisites

Your account is already assigned a DBW role. For detailed steps, refer to the guide for accounts that have been [added as](https://docs.byteplus.com/en/docs/DBW/Personal_user_management) or [applied to become a DBW role](https://docs.byteplus.com/en/docs/DBW/role-permission-request).

<span id="8orfp0oi"></span>
### Precautions


* Only users in DBW can apply for instance operation permissions.

* All administrators in DBW can approve DBW application tickets.

* The maximum validity period for permissions is 1 year.

* Approvers for operation permission tickets are set in the approval workflow when security control is enabled.

* Currently, only tickets for authorizing instances of Cache for Redis are supported.


<span id="vkVpdYNq"></span>
### Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Permission application** tab, click **Create ticket**.

5. In the dialog box that appears, select the required information for authorization.

   
   |Parameter |Description |
   |---|---|
   |**Application type** |Select **Authorize instance**. |
   |**Ticket title** |Optional. Custom ticket title. The ticket title can not exceed 200 characters. |
   |**Application type** |Default is **Authorize instance** and cannot be modified. |
   |**Database type** |From the drop\-down list, select **Cache for Redis**. |
   |**Authorize instance** |Check the instance to be authorized from the drop\-down list. Multiple selections are supported.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The drop\-down list only displays instances with security control enabled in the current region.</div><br> |
   |**Permission type** |Check the permission type as needed. Currently, the following options are supported.<br><br><br>* **SQLchange**: Refers to operations that add, modify, or delete data in the database.<br><br>* **SQL query**: Refers to the operation of retrieving the required data from the database.<br><br>* **Structural change**: Represents operations that can modify, add, or delete a database structure.<br><br>* **Operation and maintenance read\-only**: Refers to read\-only permissions for operation and maintenance management capabilities, such as viewing real\-time sessions and database audit logs.<br><br>* **Operation and maintenance read/write**: Refers to full permissions for operation and maintenance management capabilities, such as Kill sessions.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>SQL change</strong>, <strong>SQL query</strong>, and <strong>Schema change</strong> can be checked or unchecked together, but not individually.</div><br> |
   |**Effective time** |Select the validity period of the authorization from the drop\-down list, with options including **1 month** (default), **3 months**, **6 months**, and **1 year**. Additionally, custom days can be set as the validity period, with a default of 1 day and a range of [1, 365]. |
   |**Ticket remarks** |Customize your ticket remarks. We recommend aligning them with your business for easier approval and tracking. |
   

6. Click **Submit ticket**.
