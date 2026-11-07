---
title: "Managing data change tickets"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Managing_data_change_ticket"
---

This topic explains how to manage submitted tickets on the Database Workshop (DBW) console, including viewing, modifying, approving, and terminating tickets.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A ticket has been created. For detailed steps, refer to [Creating a regular SQL change ticket](https://docs.byteplus.com/en/docs/DBW/Create_a_regular_SQL_change_ticket).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* View a ticket: DBW administrators can view all tickets, while DBW normal users can only view tickets they created or are assigned as approvers.

* Edit a ticket: Only tickets that failed pre\-check can be edited. When editing a ticket, only the SQL text within the ticket can be modified.

* Approve a ticket: Only administrators, instance DBAs, and instance owners can approve tickets. The first\-level approver is the instance owner, the second\-level approver is the instance DBA, and the third\-level approver is the administrator. This approval workflow can not be modified.

* Manually execute a ticket: If the ticket is created with the Manually executed after approval option, its status will change to Waiting for execution once approved. The creator must manually execute the ticket to complete the SQL statement execution.

* Terminate a Ticket: You can terminate a ticket if it no longer meets your requirements and is in one of the following statuses: Not started, Pre\-checking, Approving, Pre\-check failed, Waiting for execution, or Executing.

* Copy a ticket: Currently, only successfully executed tickets can be copied.


<span id=".5p-l55yL5bel5Y2V"></span>
## Procedure


<Tabs>
<Tab zoneid="pEvMKcqxWK" title="View a ticket">
<TabTitle>View a ticket</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">DBW administrators can view all tickets, while DBW normal users can only view tickets they created or are assigned as approvers.</div>



1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **All** tab of the **Ticket list** page, filter the target tickets as needed and view the ticket details.

   * The **Database type** is **RDS for PostgreSQL**.

   * The **Ticket type** is **Data changes**.

      * View data change ticket list information: On the **Data change** tab, view ticket lists including those **Created by me**, **Pending my approval**, and **All**. The ticket list includes details such as **Ticket number**, **Ticket title**, **Database instance**, **Database name**, **Ticket type**, **Database type**, **Ticket status**, **Execution method**, **Creator**, **Current handler**, **Creation time**, **Last operation time**, and **Ticket remarks**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The ticket status includes <strong>Not started</strong>, <strong>Pre\-checking</strong>, <strong>Pre\-check failed</strong>, <strong>Approving</strong>, <strong>Cancelled</strong>, <strong>Rejected</strong>, <strong>Waiting for execution</strong>, <strong>Executing</strong>, <strong>Execution failed</strong>, and <strong>Executed successfully</strong>. You can filter tickets by ticket status.      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When a ticket fails to pass pre\-check, you can hover the cursor over the status of the target ticket to view the error information.      </div>
      

      * View ticket details: Click the target **Ticket number ID** in the column to open the **Ticket details** page, where you can view **Ticket information**, **SQL statements**, **Operation log** and ticket progress.

         Ticket progress includes **Pre\-check**, **Approval**, **Execution**, and **Completion**. On the **Pre\-check** configuration wizard page, you can view pre\-check items such as **Syntax check**, **Security rule check**, **Permission check**, and **Rows affected (system estimated; actual affected rows are subject to SQL execution)** .


</Tab>
<Tab zoneid="U8LzqrPK0Y" title="Approving a ticket">
<TabTitle>Approving a ticket</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click **Pending my approval**.

5. On the **Pending my approval** page,  filter the target tickets as needed.

   * **Database Type** is **RDS for PostgreSQL**.

   * The **Ticket type** is **Data changes**.

6. On the **Pending my approval** tab, click **Pass** or **Reject** in the **Actions** column of the target ticket.

   * **Pass**: To allow the operations specified in the ticket, click **Pass** in the **Actions** column.

   * **Refuse**: To deny the operations specified in the ticket, click **Refuse** in the **Actions** column.

7. In the **Confirm pass** or **Reject application** dialog box, click **OK**.


After the approval workflow is complete, the ticket status varies depending on the approval method:


* Automatic execution after approval: After the ticket is approved, it will automatically proceed to execution and will remain executed until its status changes to executed successfully.

* Manually executed after approval: After the ticket is approved, its status changes to Waiting for execution. The applicant must click Manual execution for the ticket to proceed until its status changes to Executed successfully.

* Scheduled execution after approval: After the ticket is approved, its status changes to Waiting for execution. The ticket will proceed automatically at the scheduled time you set, and its status will change to Executed successfully upon completion.


</Tab>
<Tab zoneid="rWGQSnXhHD" title="Terminating a ticket">
<TabTitle>Terminating a ticket</TabTitle>

* You can terminate a ticket if it no longer meets your requirements and is in one of the following statuses: Not started, Pre\-checking, Approving, Pre\-check failed, Waiting for execution, or Executing.

* You can only terminate tickets that you have created.

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket List** page, under the **Created by me** tab, filter the target tickets as needed.

   * **Database Type** is **RDS for PostgreSQL**.

   * The **Ticket type** is **Data changes**.

5. Select the  **...**  in the **Actions** column of the target ticket. \> **Terminate**.

6. In the **Confirm termination** dialog box, click **OK**.


</Tab>
<Tab zoneid="csLnG6mDV4" title="Copying a ticket">
<TabTitle>Copying a ticket</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Currently, copying of tickets in any status is supported.</div>



1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, under the **all** tab, filter for the target ticket as needed.

   * **Database Type** is **RDS for PostgreSQL**.

   * The **Ticket type** is **Data changes**.

5. Click **Copy ticket** in the **Actions** column of the target ticket.

6. On the **Create ticket** control panel, refer to the following instructions to modify relevant configuration information.

   [Creating a regular SQL change ticket](https://docs.byteplus.com/en/docs/DBW/Create_a_regular_SQL_change_ticket)

8. Click **Submit ticket**.


</Tab>
</Tabs>
