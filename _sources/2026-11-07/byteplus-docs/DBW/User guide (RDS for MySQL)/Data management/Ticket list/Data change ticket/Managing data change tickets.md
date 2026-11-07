---
title: "Managing data change tickets"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/ticket-management-for-mysql"
---

This topic explains how to manage submitted tickets on the Database Workshop (DBW) console, including viewing, modifying, approving, and terminating tickets.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A ticket has been created. For detailed steps, refer to [Creating a regular SQL ticket](https://docs.byteplus.com/en/docs/DBW/creating-a-normal-sql-change-ticket-for-mysql), [Creating a lock-free data change ticket](https://docs.byteplus.com/en/docs/DBW/creating-a-lock-free-sql-change-ticket-for-mysql), and [Creating a lock-free schema change ticket (OnlineDDL)](https://docs.byteplus.com/en/docs/DBW/creating-a-lock-free-structural-change-ticket-onlineddl-ticket-for-mysql).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* **View a ticket**:

   * DBW administrators can view all tickets, while DBW normal users can only view tickets they created or are assigned as approvers.

   * Both standard SQL change tickets and lock\-free data change tickets support real\-time monitoring of detailed execution information during the execution phase, including the overall progress percentage, the number of executed SQL statements, and the execution status and affected rows for each SQL statement.

* **Approve a ticket**:

   * The approver is determined by the approval workflow configured when instance security control is enabled. For more information, see Enable security control.

   * For lock\-free schema change tickets (OnlineDDL) that have force\-ignored SQL syntax inspection results, you must go to the ticket details page to complete the approval. The Pass and Refuse operations on the ticket list page are not available.

* **Manually execute a ticket**: If a ticket is created with the Manually executed after approval option or with pre\-check items force\-ignored, its status will change to Waiting for execution once approved. The creator must trigger the execution manually. For data change tickets (SQL change or lock\-free change) that fail to execute, the executed SQL statements will not be automatically rolled back.

* **Terminate a ticket**: You can terminate a ticket when its status is Not started, Pre\-checking, Approving, Pre\-check failed, Waiting for execution, or In progress. After a ticket in progress is terminated, the executed SQL statements will not be automatically rolled back.

* **Suspend a ticket**: You can suspend a ticket during execution. The executed SQL statements will not be automatically rolled back, and execution can be resumed later.

* **Copy ticket**: It supports reusing tickets in all statuses.

* **Retry ticket**:

   * Only lock\-free schema change tickets that failed to execute can be retried.

   * Regular SQL change tickets support submitting multiple SQL statements at once. When retrying, only the failed SQL statements are re\-executed, while the successfully executed SQL statements remain unaffected.


<span id="1ttwlkzm"></span>
## Procedure


<Tabs>
<Tab zoneid="oGSBsNAVxs" title="View a ticket">
<TabTitle>View a ticket</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">DBW administrators can view all tickets, while DBW normal users can only view tickets they created or are assigned as approvers.</div>



1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **All** tab of the **Ticket list** page, filter the target tickets as needed and view the ticket details.

   * **Database type** is **RDS for MySQL**.

   * The **Ticket type** is **Data changes**.

      * View data change ticket list information: On the **Data change** tab, view ticket lists including those **Created by me**, **Pending my approval**, and **All**. The ticket list includes details such as **Ticket number**, **Ticket title**, **Database instance**, **Database name**, **Ticket type**, **Database type**, **Ticket status**, **Execution method**, **Creator**, **Current handler**, **Creation time**, **Last operation time**, and **Ticket remarks**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The ticket status includes <strong>Not started</strong>, <strong>Pre\-checking</strong>, <strong>Pre\-check failed</strong>, <strong>Approving</strong>, <strong>Cancelled</strong>, <strong>Rejected</strong>, <strong>Waiting for execution</strong>, <strong>Executing</strong>, <strong>Execution failed</strong>, and <strong>Executed successfully</strong>. You can filter tickets by ticket status.      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When a ticket fails to pass pre\-check, you can hover the cursor over the status of the target ticket to view the error information.      </div>
      

      * View ticket details: Click the target **Ticket number ID** in the column to open the **Ticket details** page, where you can view **Ticket information**, **SQL statements**, **Operation log** and ticket progress.

         * On the **Pre\-check** wizard page, you can view the results of various checks, including **Syntax checks**, **Security rule checks**, and **Permission checks**, **and number of rows affected (which is a system statistic; the actual number of affected rows is subject to the final SQL execution)** .

         * On the **Execute ticket** wizard page (for standard SQL change tickets and lock\-free data change tickets), you can view the following execution progress information:

            * **Overall execution progress**: Displayed as a percentage, accurate to two decimal places (e.g., 43.05%).

            * **Executed SQL / Total SQL count**: The ratio of the number of completed SQL statements to the total number of SQL statements in the current ticket.

            * **SQL task list**: Displayed as a list showing the execution details of each SQL statement in the current ticket, including the sequence number, execution status, execution count, affected rows, and the executed SQL statement.


</Tab>
<Tab zoneid="ujrh1z7HTp" title="Approving a ticket">
<TabTitle>Approving a ticket</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click **Pending my approval**.

5. On the **Pending my approval** page,  filter the target tickets as needed.

   * **Database type** is **RDS for MySQL**.

   * The **Ticket type** is **Data changes**.

   Click the ticket number to view its details, including basic information, executed SQL statements, and approval progress.

   * **Pass**: To allow the operations specified in the ticket, click **Pass** in the **Actions** column.

   * **Refuse**: To deny the operations specified in the ticket, click **Refuse** in the **Actions** column.


After the approval workflow is complete, the ticket status varies depending on the approval method:


* Automatic execution after approval: After the ticket is approved, it will automatically proceed to execution and will remain executed until its status changes to executed successfully.

* Manually executed after approval: After the ticket is approved, its status changes to Waiting for execution. The applicant must click Manual execution for the ticket to proceed until its status changes to Executed successfully.

* Scheduled execution after approval: After the ticket is approved, its status changes to Waiting for execution. The ticket will proceed automatically at the scheduled time you set, and its status will change to Executed successfully upon completion.


</Tab>
<Tab zoneid="uc7Wb6EGXN" title="Terminating a ticket">
<TabTitle>Terminating a ticket</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">You can terminate a ticket if it no longer meets your requirements and is in one of the following statuses: Not started, Pre\-checking, Approving, Pre\-check failed, Waiting for execution, or Executing.</div>


* <div data-tips="true" data-tips-type="default">You can only terminate tickets that you have created.</div>


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket List** page, under the **Created by me** tab, filter the target tickets as needed.

   * **Database type** is **RDS for MySQL**.

   * The **Ticket type** is **Data changes**.

5. Select the ... in the **Actions** column of the target ticket. \> **Terminate**.


You can also click the **Terminate** button on the **Ticket details** \> **Execute ticket** configuration wizard page.


6. In the **Confirm termination** dialog box, click **OK**.


</Tab>
<Tab zoneid="YTWH3wWLJy" title="Copying a ticket">
<TabTitle>Copying a ticket</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Currently, the reuse of tickets in any status is supported.</div>



1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, under the **all** tab, filter for the target ticket as needed.

   * **Database type** is **RDS for MySQL**.

   * The **Ticket type** is **Data changes**.

5. Click **Copy ticket** in the **Actions** column of the target ticket.

6. On the **Create ticket** control panel, refer to the following instructions to modify relevant configuration information.

   * [Creating a regular SQL change ticket](https://docs.byteplus.com/en/docs/DBW/creating-a-normal-sql-change-ticket-for-mysql)

   * [Creating a lock-free data change ticket](https://docs.byteplus.com/en/docs/DBW/creating-a-lock-free-sql-change-ticket-for-mysql)

   * [Creating a lock-free schema change ticket](https://docs.byteplus.com/en/docs/DBW/creating-a-lock-free-structural-change-ticket-onlineddl-ticket-for-mysql)

7. Click **Submit ticket**.


</Tab>
<Tab zoneid="bLqWeAKdGt" title="Retry ticket">
<TabTitle>Retry ticket</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Currently, only failed Lock\-free schema change tickets can be retried.</div>


* <div data-tips="true" data-tips-type="default">Since a regular SQL change ticket supports submitting multiple SQL statements at once, retrying will immediately execute the failed SQL statements, while completed SQL executions remain unaffected.</div>


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click **Data change**.

5. On the **Data changes** tab, filter by **Ticket type** and **Database type**.

   * **Ticket type** is **Lock\-free schema change**.

   * **Database type** is **RDS for MySQL**.

6. Click the target ticket name.

7. On the **Ticket details** page, in the **Execute ticket** configuration wizard, click **Retry**.

8. In the **Confirm retry** dialog box, click **OK**.


</Tab>
<Tab zoneid="Bnnr4LPej5" title="Edit a ticket">
<TabTitle>Edit a ticket</TabTitle>

You can edit tickets that are in progress or suspended.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket List** page, under the **Created by me** tab, filter the target tickets as needed.

   * **Database type** is **RDS for MySQL**.

   * The **Ticket type** is **Data changes**.

5. Click the target ticket number.

6. On the target ticket details page, in the **Execute ticket** configuration wizard, click Edit parameters.

7. In the Modify work ticket execution parameters dialog, set the **Full copy size** and **Primary\-standby delay threshold** parameters.

8. Click **OK**.


</Tab>
<Tab zoneid="SKXlhVltKn" title="Suspend a ticket">
<TabTitle>Suspend a ticket</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket List** page, under the **Created by me** tab, filter the target tickets as needed.

   * **Database type** is **RDS for MySQL**.

   * The **Ticket type** is **Data changes**.

5. Click the target ticket number.

6. On the target ticket details page, in the **Execute ticket** configuration wizard, click **Suspend**.

7. In the **Confirm suspension** box, click **OK**.


After pausing, you can resume the ticket. On the **Execution ticket** page, click **Resume**. In the **Confirm recovery** box, click **Confirm**.


</Tab>
</Tabs>
