---
title: "Manage clear table tickets"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/manage_clear_table_tickets_NDB"
---

This topic explains how to manage submitted tickets on the Database Workshop (DBW) console, including viewing, modifying, and approving tickets.

<span id="IbrMpv8E"></span>
## Prerequisites

A cleat table ticket has been created. For detailed operations, see [Create a cleat table ticket](https://docs.byteplus.com/en/docs/DBW/cleate_a_clear_table_ticket_NDB).

<span id="9mkOFM9e"></span>
## Precautions


* View a ticket: DBW administrators can view all tickets, while DBW normal users can only view tickets they created or are assigned as approvers.

* Approve a ticket: Approvers for ticket approval are set in the approval workflow when instance security control is enabled. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control).

* Manually execute a ticket: If the ticket is created with the manually executed after approval option, its status will change to waiting for execution once approved. The creator must manually execute the ticket to complete the SQL statement execution.


<span id="nyGROMur"></span>
## Procedure


<Tabs>
<Tab zoneid="UBRTSQJgcq" title="View a ticket">
<TabTitle>View a ticket</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, after filtering for the target ticket as needed, you can view the following information:

   * **Database type** is **NDB for MySQL**.

   * **Ticket type** is **Clear table tickets**.

      On the ticket list page, you can view all ticket information, including **Ticket number**, **Ticket title**, **Database instance**, **Database name**, **Source table name**, **Operation type**, **Historical data retention policy**, **Database type**, **Ticket status**, **Execution method**, **Creator**, **Current handler**, **Creation time**, **Last operation time, Ticket remarks, Actions**, etc.

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Description      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The ticket status includes <strong>Not started</strong>, <strong>Approving</strong>, <strong>Cancelled</strong>, <strong>Rejected</strong>, <strong>Wait for execution</strong>, <strong>In progress</strong>, <strong>Failed</strong>, <strong>Executed successfully</strong>, and <strong>Terminated</strong>. You can filter tickets by ticket status.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">When a ticket fails to pass pre\-check, you can hover the cursor over the status of the target ticket to view the error information.      </div>
      

         * Click the target ticket ID. On the ticket details page, you can view the ticket's **Basic information**, **Execute SQL statement**, **Operation log**, **Configuration information**, and ticket processing workflow.

      On the ticket details page, click **Approve ticket** in the workflow to view the current approval progress, including approver and approval time. Click **Execute ticket** to view the execution progress of the ticket.


</Tab>
<Tab zoneid="bEEixUGi6O" title="Approve a ticket">
<TabTitle>Approve a ticket</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, go to the **Pending my approval** tab and filter for the target tickets as needed.

   * **Database type** is **NDB for MySQL**.

   * **Ticket type** is **Clear table tickets**.

5. On the **Pending my approval** sub\-tab, approve the tickets as needed.

   * **Pass**: Click **Pass** under the **Actions** column to allow the ticket to execute SQL operations.

   * **Refuse**: Click **Refuse** under the **Actions** column to disallow the ticket to execute SQL operations.

   After the approval workflow is complete, the ticket status varies depending on the approval method:

   * Automatic execution after approval: After the ticket is approved, it will automatically proceed to execution.

   * Scheduled execution after approval: After the ticket is approved, its status changes to Waiting for execution. The ticket will only be executed once its scheduled start time is reached.

   * Manually executed after approval: After the ticket approvalis completed, the ticket status changes to Wait for execution. The ticket creator needs to click **Manual execution** to execute the ticket.


</Tab>
<Tab zoneid="VNbMFX2eP0" title="Manually execute ticket">
<TabTitle>Manually execute ticket</TabTitle>

If the execution method of the ticket is **Manually executed after approval**, the ticket creator still needs to manually execute the ticket after the ticket approval is passed.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Only the ticket creator can manually execute the ticket task.</div>



1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, under the **All** tab, filter for the target ticket as needed:

   * **Database type** is **NDB for MySQL**.

   * **Ticket type** is **Clear table tickets**.

5. On the **Create a checklist ticket** tab, click **Manual execution** in the **Actions** column of the target ticket, or click **Manual execution** on the ticket details page.

6. In the **Execute ticket** dialog box, click **OK**.

   You can view the ticket execution result later.


</Tab>
<Tab zoneid="EyEXQFkEAM" title="Terminate a ticket">
<TabTitle>Terminate a ticket</TabTitle>

You can terminate the checklist ticket when you no longer need to execute the checklist task.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Only the ticket creator can terminate a ticket task.</div>



1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, under the **All** tab, filter for the target ticket as needed:

   * **Database type** is **NDB for MySQL**.

   * **Ticket type** is **Clear table tickets**.

5. On the **Clear table ticket** tab, click **Terminate** in the **Actions** column of the target ticket.

6. In the **Confirm termination** dialog box, click **OK**.


</Tab>
</Tabs>
