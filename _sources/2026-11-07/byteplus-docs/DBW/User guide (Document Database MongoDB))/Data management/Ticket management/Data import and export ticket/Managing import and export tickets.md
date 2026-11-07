---
title: "Managing import and export tickets"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/managing-import-and-export-tickets-for-mongodb"
---

This topic explains how to manage import and export tickets you created on the Database Workshop (DBW) console.

<span id="LwSd8lbE"></span>
## Prerequisites

A ticket has been created. For detailed steps, refer to [Creating a data import ticket](https://docs.byteplus.com/en/docs/DBW/creating-a-data-import-ticket_for_mongodb?lang=en) and [Creating a full database export ticket](https://docs.byteplus.com/en/docs/DBW/creating-a-full-database-export-ticket-for-mongodb?lang=en).

<span id="QlJlNh1y"></span>
## Precautions


* Approve a ticket: Approvers for ticket approval are set in the approval workflow when instance security control is enabled. For detailed steps, refer to Enabling security control.

* Terminate a ticket: You can terminate a ticket if it no longer meets your requirements and is in one of the following statuses: Pre\-checking, Approving, Pre\-check failed, or Executing.

* View a ticket: DBW administrators can view all tickets, while DBW normal users can only view tickets they created or are assigned as approvers.


<span id="U8Hco00O"></span>
## Procedure


<Tabs>
<Tab zoneid="TfqLX29zYS" title="Approving a ticket">
<TabTitle>Approving a ticket</TabTitle>

Approvers for ticket approval are set in the approval workflow when instance security control is enabled. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/MongoDB_Enabling_security_control?lang=en).


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, in the **Pending my approval** tab, filter for the target ticket information as needed.

   * The **database type** is **Document Database for MongoDB**.

   * **Ticket type** is **Data import/export**.

1. Click the ticket number to view its details, including basic information and approval progress. Click the upload file to download and view the imported data file locally.

   * **Pass**: To allow the operations specified in the ticket, click **Pass** in the **Actions** column.

   * **Refuse**: To deny the operations specified in the ticket, click **Refuse** in the **Actions** column.


After the ticket is approved, it will automatically proceed to execution and will remain executed until its status changes to executed successfully.


</Tab>
<Tab zoneid="KkNw7USdK5" title="Terminating a ticket">
<TabTitle>Terminating a ticket</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can terminate a ticket if it no longer meets your requirements and is in one of the following statuses: Pre\-checking, Approving, Pre\-check failed, or Executing.</div>



1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, go to the **Created by me** tab and filter for the target ticket as needed.

   * The **database type** is **Document Database for MongoDB**.

   * **Ticket type** is **Data cleanup and archiving**.

5. On the **Data import/export** tab, click  **...**  \> Terminate in the **Actions** column of the target ticket. \> **Terminate**.

6. In the **Confirm termination** dialog box, click **OK**.


</Tab>
<Tab zoneid="sA3k6i6ReS" title="View data import and export tickets">
<TabTitle>View data import and export tickets</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">DBW administrators can view all tickets, while DBW normal users can only view tickets they created or are assigned as approvers.</div>



1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, under the **all**, **Created by me**, and **Pending my approval** tabs, filter and view the target ticket information as needed.

   * The **database type** is **Document Database for MongoDB**.

   * **Ticket type** is **Data import/export**.

      * View the data import/export ticket list: On the **Data import/export** tab, you can view the ticket list information, including **Created by me**, **Pending my approval**, and **All**. The ticket list includes **Ticket number**, **Ticket title**, **Database instance**, **Database name**, **Ticket type**, **Database type**, **Ticket status**, **Execution method**, **Creator**, **Current handler**, **Creation time**, **Last operation time**, and **Ticket remarks**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When a ticket fails pre\-check or execution, you can hover the cursor over the status of the target ticket to view the error information.      </div>
      

      * View data import/export ticket information: Click the target ticket ID in the **Ticket number** column. On the **Ticket details** page, you can view the ticket information, export executed SQL, operation log, and ticket progress.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Export executed SQL only appears in SQL result set export tickets.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Ticket progress includes <strong>Pre\-check</strong>, <strong>Approval ticket</strong>, <strong>Execute ticket</strong>, and <strong>Complete</strong>. On the <strong>Pre\-check</strong> configuration wizard page, you can review pre\-check items, including <strong>Syntax</strong> and <strong>Permission</strong>.      </div>
      


</Tab>
</Tabs>


&nbsp;
