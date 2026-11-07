---
title: "Creating an SQL result set export ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/creating-an-sql-result-set-export-ticket"
---

This topic explains how to create an SQL result set export ticket for an RDS for MySQL instance on the DBW console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance for RDS for MySQL and an account with read/write permissions to the target database have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts#.5Yib5bu66LSm5Y-3).

* The instance has enabled security control. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql).

* The BytePlus sub\-user has been added as a DBW role. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/Personal_user_management).

* The BytePlus sub\-user added as a DBW role has been granted relevant permissions. For detailed steps, refer to [Permission management](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The download link is valid for 30 days. After this period, the file will no longer be available for download. Please download the data promptly. If the link becomes invalid within the validity period, you can regenerate a new link on the ticket details page.

* Only one export task can be created at a time. Concurrent exports are not supported.

* For export tasks, the maximum size for a single table is 10 GiB, and the maximum total size for a single task is 50 GiB.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the **Ticket list** page, click **Create ticket**.

4. In the dialog box that appears, select **Data import/export** \> **Data import/export**.

5. On the **Fill in the ticket** configuration wizard of the **Create data import/export ticket** control panel, configure the following parameters.

   
   <Tabs>
   <Tab zoneid="Uv7KvIbQOH" title="Export CSV file tickets">
   <TabTitle>Export CSV file tickets</TabTitle>
   
   
   |**Type** |**Parameter** |**Description** |
   |---|---|---|
   |**Basic information** |**Creator** |Defaults to the currently logged\-in account and can not be modified. |
   ||**Ticket title** |Optional. Custom ticket title. The ticket title can not exceed 200 characters. If not set, it defaults to empty. |
   ||**Database type** |This topic describes how to create a full database export ticket for RDS for MySQL. Therefore, select **RDS for MySQL** as the **Database type**. |
   ||**Ticket type** |Select **SQL result set export**. |
   ||**Execution method** |Defaults to **Automantic execution after approval**, meaning full database export tickets will run automatically once approved. This parameter can not be modified. |
   |**Data import/export configuration** |**Instance** |From the drop\-down list, select the target instance. |
   ||**Database** |From the drop\-down list, select the target database. |
   ||**File type** |Select **CSV**. |
   ||**Data location** |Select data location. The following options are currently supported:<br><br><br>* **First row attributes**: The first row of the table contains field names.<br><br>* **First row of data**: The first row of the table contains data. |
   ||**Character set** |Select the target character set from the drop\-down list. Currently supported options include `utf8`, `utf8mb4`, `latin1`, and `ascii`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">It is recommended to use the suggested character encoding. Based on the database and target table you select, DBW automatically retrieves the character sets from all relevant tables and provides a recommended option.</div><br> |
   ||**Export executed SQL** |Enter `select` statements to query data from multiple tables. When entering multiple SQL statements, the total text size must not exceed 4 GiB. |
   ||**Ticket remarks** |Optional. Customize your ticket remarks for database export. We recommend aligning them with your business for easier tracking. |
   
   
   
   
   
   </Tab>
   <Tab zoneid="RpsJyfpnYq" title="Create an SQL file ticket">
   <TabTitle>Create an SQL file ticket</TabTitle>
   
   
   |**Type** |**Parameter** |**Description** |
   |---|---|---|
   |**Basic information** |**Creator** |Defaults to the currently logged\-in account and can not be modified. |
   ||**Ticket title** |Optional. Custom ticket title. The ticket title can not exceed 200 characters. If not set, it defaults to empty. |
   ||**Database type** |This topic describes how to create a full database export ticket for RDS for MySQL. Therefore, select **RDS for MySQL** as the **Database type**. |
   ||**Ticket type** |Select **SQL result set export**. |
   ||**Execution method** |Defaults to **Automantic execution after approval**, meaning full database export tickets will run automatically once approved. This parameter can not be modified. |
   |**Data import/export configuration** |**Instance** |From the drop\-down list, select the target instance. |
   ||**Database** |From the drop\-down list, select the target database. |
   ||**File type** |Select **CSV**. |
   ||**Data location** |Select data location. The following options are currently supported:<br><br><br>* **First row attributes**: The first row of the table contains field names.<br><br>* **First row of data**: The first row of the table contains data. |
   ||**Character set** |Select the target character set from the drop\-down list. Currently supported options include `utf8`, `utf8mb4`, `latin1`, and `ascii`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">It is recommended to use the suggested character encoding. Based on the database and target table you select, DBW automatically retrieves the character sets from all relevant tables and provides a recommended option.</div><br> |
   ||**Export executed SQL** |Enter `select` statements to query data from multiple tables. When entering multiple SQL statements, the total text size must not exceed 4 GiB. |
   ||**Ticket remarks** |Optional. Customize your ticket remarks for database export. We recommend aligning them with your business for easier tracking. |
   
   
   
   
   
   </Tab>
   </Tabs>
   

6. Click **Next step: Pre\-check**.

7. On the **Ticket pre\-check** configuration wizard of the **Create data import/export ticket** control panel, you can view pre\-check items, including **Syntax** and **Permission**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If pre\-check fails, you can click <strong>View details</strong> in the <strong>Result details</strong> column of the check item to review the specific reasons for the failure. After making corrections, recreate the ticket.   </div>
   

8. Click **OK**.
