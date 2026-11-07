---
title: "Creating an operation permission ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket_"
---

This topic describes how to create an operation permission ticket for applying for an RDS for SQL Server instance on the Database Workshop (DBW) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Your account is already assigned a DBW system role. For detailed steps, refer to [The administrator has added your account as a DBW role](https://docs.byteplus.com/en/docs/DBW/Personal_user_management) or [The sub-account has applied to become a DBW role](https://docs.byteplus.com/en/docs/DBW/role-permission-request).

* The administrator has enabled security control for the instance. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-control_).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only normal users in DBW can apply for instance operation permissions. The DBW administrator has all instance permissions by default.

* All administrators in DBW can approve DBW role application tickets.

* Approvers for operation permission tickets are set in the approval workflow when security control is enabled.

* The maximum validity period for permissions is 1 year.

* Currently, only the application for operation permissions for RDS for SQL Server instances is supported.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Data management** \> **Ticket list**.

3. On the top menu bar, select the region.

4. On the **Ticket list** page, click **Permission application**.

5. On the **Permission application** tab, click **Create ticket**.

6. In the dialog box that appears, select the required information for authorization.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Applicant** |The applicant defaults to the currently logged\-in account and can not be modified. |
   |**Ticket title** |Optional. Custom ticket title. The ticket title can not exceed 200 characters. |
   |**Application type** |Default is **Authorize instance** and cannot be modified. |
   |**Database type** |Select the database type **RDS for SQL Server** from the drop\-down list. |
   |**Authorize instance** |Check the target instance from the drop\-down list. Multiple selections are supported. |
   |**Permission type** |Check the permission type as needed. Currently, the following options are supported.<br><br><br>* **SQLchange**: Refers to operations that add, modify, or delete data in the database. SQL statement types include `CREATE`, `ALTER`, `DROP`, `UPDATE`, `INSERT`and `DELETE`.<br><br>* **SQL query**: Refers to the operation of retrieving the required data from the database. SQL statement types include `SELECT`, and `SHOW` .<br><br>* **Structural change**: Represents operations that can modify, add, or delete a database structure. SQL statement types include `ALTER TABLE`, `CREATE INDEX`, and `DROP INDEX`.<br><br>* **Operation and maintenance read\-only**: Refers to read\-only permissions for operation and maintenance management capabilities, such as viewing real\-time sessions and slow SQL analysis lists.<br><br>* **Operation and maintenance read/write**: Refers to full permissions for operation and maintenance management capabilities, such as Kill sessions and creating SQL rate limiting tasks. |
   |**Effective time** |Select the validity period of the authorization from the drop\-down list, with options including **1 month**, **3 months**, **6 months**, and **1 year**. Additionally, custom days can be set as the validity period, with a default of 1 day and a range of [1, 365]. |
   |**Ticket remarks** |Customize your ticket remarks. We recommend aligning them with your business for easier approval and tracking. |
   

7. Click **Submit application**.
