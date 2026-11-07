---
title: "Creating an operation permission ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket"
---

This topic explains how to create a ticket on the Database Workshop (DBW) console to apply for operation permissions on NDB for MySQL instances, databases, tables, and columns.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Your account is already assigned a DBW role. For detailed steps, refer to the guide for accounts that have been [added as](https://docs.byteplus.com/en/docs/DBW/Personal_user_management) or [applied to become a DBW role](https://docs.byteplus.com/en/docs/DBW/role-permission-request).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only normal users in DBW can apply for instance operation permissions.

* All administrators in DBW can approve DBW role application tickets.

* The maximum validity period for permissions is 1 year.

* Approvers for operation permission tickets are set in the approval workflow when security control is enabled.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click Create ticket.

5. In the dialog box, select the permissions you need to apply for.

   
   <Tabs>
   <Tab zoneid="mdGMxW0AxK" title="Authorize instance">
   <TabTitle>Authorize instance</TabTitle>
   
   In the dialog box that appears, select **Permission application** \> **Authorize instance**.
   
   
   |**Parameter** |**Description** |
   |---|---|
   |**Applicant** |Defaults to the currently logged\-in account and can not be modified. |
   |**Ticket title** |Optional. Custom ticket title. The ticket title can not exceed 200 characters. |
   |**Application type** |Default is **Authorize instance** and cannot be modified. |
   |**Database type** |, select  From the drop\-down list, select **veDB for MySQL**. |
   |**Authorize instance** |Check the instance to be authorized from the drop\-down list. Multiple selections are supported. |
   |**Permission type** |Check the permission type as needed. Currently, the following options are supported.<br><br><br>* **SQLchange**: Refers to operations that add, modify, or delete data in the database. SQL statement types include `CREATE`, `ALTER`, `DROP`, `UPDATE`, `INSERT`and `DELETE`.<br><br>* **SQL query**: Refers to the operation of retrieving the required data from the database. SQL statement types include `SELECT`, and `SHOW` .<br><br>* **Structural change**: Represents operations that can modify, add, or delete a database structure. SQL statement types include `ALTER TABLE`, `CREATE INDEX`, and `DROP INDEX`.<br><br>* **Operation and maintenance read\-only**: Refers to read\-only permissions for operation and maintenance management capabilities, such as viewing real\-time sessions and slow SQL analysis lists.<br><br>* **Operation and maintenance read/write**: Refers to full permissions for operation and maintenance management capabilities, such as Kill sessions and creating SQL rate limiting tasks. |
   |**Effective time** |Select the valid period for the authorized instance from the drop\-down list, with options including **1 month**, **3 months**, **6 months**, and **1 year**. Additionally, custom days can be set as the validity period, with a default of 1 day and a range of [1, 365]. |
   |**Ticket remarks** |Customize your ticket remarks. We recommend aligning them with your business for easier approval and tracking. |
   
   
   
   </Tab>
   <Tab zoneid="Wu1eBRIyDz" title="Authorize database">
   <TabTitle>Authorize database</TabTitle>
   
   In the pop\-up dialog, select **Permission application** \> **Authorize database**.
   
   
   |**Parameter** |**Description** |
   |---|---|
   |**Applicant** |Defaults to the currently logged\-in account and can not be modified. |
   |**Ticket title** |Optional. Custom ticket title. The ticket title can not exceed 200 characters. |
   |**Application type** |Default is **Authorize database** and cannot be modified. |
   |**Database type** |, select  From the drop\-down list, select **veDB for MySQL**. |
   |**Authorize instance** |Select the instance to authorize from the drop\-down list. |
   |**Authorize database** |Select the databases to authorize from the drop\-down list. Multiple selections are supported. |
   |**Permission type** |Check the permission type as needed. Currently, the following options are supported.<br><br><br>* **SQLchange**: Refers to operations that add, modify, or delete data in the database. SQL statement types include `CREATE`, `ALTER`, `DROP`, `UPDATE`, `INSERT`and `DELETE`.<br><br>* **SQL query**: Refers to the operation of retrieving the required data from the database. SQL statement types include `SELECT`, and `SHOW` .<br><br>* **Structural change**: Represents operations that can modify, add, or delete a database structure. SQL statement types include `ALTER TABLE`, `CREATE INDEX`, and `DROP INDEX `. |
   |**Effective time** |Select the valid period for the authorized instance from the drop\-down list, with options including **1 month**, **3 months**, **6 months**, and **1 year**. Additionally, custom days can be set as the validity period, with a default of 1 day and a range of [1, 365]. |
   |**Ticket remarks** |Customize your ticket remarks. We recommend aligning them with your business for easier approval and tracking. |
   
   
   
   </Tab>
   <Tab zoneid="qp3bjIQAJ1" title="Authorize table">
   <TabTitle>Authorize table</TabTitle>
   
   In the dialog box, go to **Permission application** \> **Authorize table**.
   
   
   |**Parameter** |**Description** |
   |---|---|
   |**Applicant** |Defaults to the currently logged\-in account and can not be modified. |
   |**Ticket title** |Optional. Custom ticket title. The ticket title can not exceed 200 characters. |
   |**Application type** |Default is **Authorize database** and cannot be modified. |
   |**Database type** |, select  From the drop\-down list, select **veDB for MySQL**. |
   |**Authorize instance** |Select the instance to authorize from the drop\-down list. |
   |**Authorize database** |Select the database to be authorized from the drop\-down list. |
   |**Authorize table** |Select the tables to be authorized from the drop\-down list. Multiple selections are supported. |
   |**Permission type** |Check the permission type as needed. Currently, the following options are supported.<br><br><br>* **SQLchange**: Refers to operations that add, modify, or delete data in the database. SQL statement types include `CREATE`, `ALTER`, `DROP`, `UPDATE`, `INSERT`and `DELETE`.<br><br>* **SQL query**: Refers to the operation of retrieving the required data from the database. SQL statement types include `SELECT`, and `SHOW` .<br><br>* **Structural change**: Represents operations that can modify, add, or delete a database structure. SQL statement types include `ALTER TABLE`, `CREATE INDEX`, and `DROP INDEX `. |
   |**Effective time** |Select the valid period for the authorized instance from the drop\-down list, with options including **1 month**, **3 months**, **6 months**, and **1 year**. Additionally, custom days can be set as the validity period, with a default of 1 day and a range of [1, 365]. |
   |**Ticket remarks** |Customize your ticket remarks. We recommend aligning them with your business for easier approval and tracking. |
   
   
   
   </Tab>
   <Tab zoneid="h2CHaiIwPa" title="Authorize column">
   <TabTitle>Authorize column</TabTitle>
   
   In the dialog box, select **Permission application** \> **Authorize column**.
   
   
   |**Parameter** |**Description** |
   |---|---|
   |**Applicant** |Defaults to the currently logged\-in account and can not be modified. |
   |**Ticket title** |Optional. Custom ticket title. The ticket title can not exceed 200 characters. |
   |**Application type** |Default is **Authorize database** and cannot be modified. |
   |**Database type** |, select  From the drop\-down list, select **veDB for MySQL**. |
   |**Authorize instance** |Select the instance to authorize from the drop\-down list. |
   |**Authorize database** |Select the database to be authorized from the drop\-down list. |
   |**Authorize table** |Select the table to be authorized from the drop\-down list. |
   |**Authorize column** |Select columns to be authorized from the drop\-down list. Multiple selections are supported. After selecting the instance, database, table, and column as needed, click **Add** to include the column permissions in user permissions. |
   |**Permission type** |Check the permission type as needed. Currently, the following options are supported.<br><br><br>* **SQLchange**: Refers to operations that add, modify, or delete data in the database. SQL statement types include `CREATE`, `ALTER`, `DROP`, `UPDATE`, `INSERT`and `DELETE`.<br><br>* **SQL query**: Refers to the operation of retrieving the required data from the database. SQL statement types include `SELECT`, and `SHOW` .<br><br>* **Structural change**: Represents operations that can modify, add, or delete a database structure. SQL statement types include `ALTER TABLE`, `CREATE INDEX`, and `DROP INDEX `. |
   |**Effective time** |Select the valid period for the authorized instance from the drop\-down list, with options including **1 month**, **3 months**, **6 months**, and **1 year**. Additionally, custom days can be set as the validity period, with a default of 1 day and a range of [1, 365]. |
   |**Ticket remarks** |Customize your ticket remarks. We recommend aligning them with your business for easier approval and tracking. |
   
   
   
   </Tab>
   </Tabs>
   

6. Click **Submit application**.
