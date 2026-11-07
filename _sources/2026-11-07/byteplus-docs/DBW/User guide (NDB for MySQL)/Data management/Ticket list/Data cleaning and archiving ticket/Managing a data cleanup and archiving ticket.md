---
title: "Managing a data cleanup and archiving ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Managing_data_cleaning_and_archiving_tickets"
---

This topic explains how to manage submitted tickets on the Database Workshop (DBW) console, including viewing, modifying, and approving tickets.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A data cleanup and archiving ticket has been created. For detailed steps, refer to [Creating a data cleanup and archiving ticket](https://docs.byteplus.com/en/docs/DBW/Creating_a_data_cleanup_and_archiving_ticket).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* View a ticket: DBW administrators can view all tickets, while DBW normal users can only view tickets they created or are assigned as approvers.

* Approve a ticket: Approvers for ticket approval are set in the approval workflow when instance security control is enabled. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql).

* Manually execute a ticket: If the ticket is created with the Manually executed after approval option, its status will change to Waiting for execution once approved. The creator must manually execute the ticket to complete the SQL statement execution.


<span id=".5p-l55yL5bel5Y2V"></span>
## Procedure


<Tabs>
<Tab zoneid="g6RGs1H32d" title="View a ticket">
<TabTitle>View a ticket</TabTitle>

<span id="onXwvG31"></span>
## 


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, use the **All**, **Created by me**, and **Pending my approval** tabs to filter and view target ticket information as needed.

   * **Database type** is **NDB for MySQL**.

   * **Ticket type** is **Data cleanup and archiving**.

      * On the ticket list page, you can view all ticket information, including **Ticket number**, **Ticket title**, **Database instance**, **Database name**, **Table name**, **Is deleted data backed up?** , **Database type**, **Ticket status**, **Execution method**, **Creator**, **Current handler**, **Creation time**, **Last operation time, Number of rows deleted, Ticket remarks, and Actions**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The ticket status includes <strong>Not started</strong>, <strong>Pre\-checking</strong>, <strong>Pre\-check failed</strong>, <strong>Approving</strong>, <strong>Cancelled</strong>, <strong>Rejected</strong>, <strong>Waiting for execution</strong>, <strong>Executing</strong>, <strong>Execution failed</strong>, and <strong>Executed successfully</strong>. You can filter tickets by ticket status.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When a ticket fails to pass pre\-check, you can hover the cursor over the status of the target ticket to view the error information.      </div>
      

      * Click the target ticket ID to view the basic information, including **Creator**, **Archive table**, **Database type**, **Creation time**, ** Instance ID**, ** Last operation time**, ** Database name**, ** Ticket title, and Ticket remarks**. Configuration information includes **Filter condition**, **Archive type**, **Delete data backup**, **Variables configuration**, **Execution time**, **and Single batch deletion row count**. Click **View** next to Variables configuration to view configuration details. You can also view the operation log of the ticket.

      * On the ticket details page, click **Approve ticket** in the workflow to view the current approval progress, including approver and approval time.

      * On the ticket details page, click **Execute ticket** in the workflow to view the current execution progress, including **Task ID**, **Execution status**, **Start Time**, **Completion time**, **Database user**, **Execute SQL statements**, **Number of rows deleted**, **backup address**, and **Actions**, etc. Click **View log** in the actions column to view detailed execution log of the current scheduling task. Click **Download** in the backup address column to download data backed up in TOS (data backup configured in the ticket). If the ticket is in the approval state and has not yet entered the execution phase, you can not view its execution status.


</Tab>
<Tab zoneid="FTN4naRuFo" title="Download backup data">
<TabTitle>Download backup data</TabTitle>

If the data backup function is configured when creating a data cleanup and archiving ticket, and the data is backed up to the built\-in TOS. After the ticket task is executed, the backup data is stored in CSV format and retained for 30 days; it will be automatically deleted after expiration. If necessary, download the backup data to your local device in time. The method to download backup data is as follows.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, go to the **All**, **Created by me** tab and filter to view the target ticket information as needed.

   * **Database type** is **NDB for MySQL**.

   * **Ticket type** is **Data cleanup and archiving**.

5. On the ticket details page, click **Execute ticket** in the workflow.

6. Click **Download** in the backup address column to save the data backed up in TOS to your local machine.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To re\-import the downloaded backup data into the database,  Refer to<a href="https://docs.byteplus.com/en/docs/DBW/Creating_a_data_import_ticket">Creating a data import ticket for NDB for MySQL</a>.   </div>
   


</Tab>
<Tab zoneid="f0rTRYPEQE" title="Approving a ticket">
<TabTitle>Approving a ticket</TabTitle>

<span id="sPbLeHfL"></span>
## 

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, go to the **Pending my approval** tab and filter the target ticket information as needed.

   * **Database type** is **NDB for MySQL**.

   * **Ticket type** is **Data cleanup and archiving**.

1. On the **Pending my approval** sub\-tab, find the target ticket and approve the ticket as required.

   * **Pass**: To allow the operations specified in the ticket, click **Pass** in the **Actions** column.

   * **Refuse**: To deny the operations specified in the ticket, click **Refuse** in the **Actions** column.

   After the approval workflow is complete, the ticket status varies depending on the approval method:

   * Automatic execution after approval: After the ticket is approved, it will automatically proceed to execution.

   * Scheduled execution after approval: After the ticket is approved, its status changes to Waiting for execution. The ticket will only be executed once its scheduled start time is reached.


</Tab>
<Tab zoneid="se9EitKEjX" title="Terminating a ticket">
<TabTitle>Terminating a ticket</TabTitle>

You can terminate the data cleanup and archiving task when archiving historical data is no longer needed.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Only the ticket creator can terminate a ticket task.</div>



1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, go to the **Created by me** tab and filter to view the target ticket information as needed.

   * **Database type** is **NDB for MySQL**.

   * **Ticket type** is **Data cleanup and archiving**.

6. On the **Created by me** subtab, click **Terminate** in the **Actions** column of the target ticket.

7. In the **Confirm termination** dialog box, click **OK**.


</Tab>
</Tabs>
