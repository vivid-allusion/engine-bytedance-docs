---
title: "Managing permission application tickets"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/managing-permission-application-tickets__"
---

This topic describes how to manage permission application tickets on the Database Workshop (DBW) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An operation permission ticket has been created. For detailed steps, refer to [Creating an operation permission ticket](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket_).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Approvers for ticket approval are set in the approval workflow when instance security control is enabled. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-control_).

* DBW administrators can view all tickets, while DBW normal users can only view tickets they created or are assigned as approvers.


<span id=".5p-l55yL5bel5Y2V"></span>
## View a ticket

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">DBW administrators can view all tickets, while DBW normal users can only view tickets they created or are assigned as approvers.</div>



1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Data management** \> **Ticket list**.

3. On the top menu bar, select the region.

4. On the **Ticket list** page, click **Permission application**.

5. On the **Permission application** tab, you can view the following information:

   * View basic ticket information: On the **Permission application** tab, you can view information such as the **Ticket number**, **Application type**, **Ticket status**, **Application reason**, **Creator**, **Current handler**, **Creation time**, and **Last operation time** of all tickets.

   * View detailed ticket information: On the **Permission application** tab, click the **Ticket number** of the target ticket. On the **Ticket details** page, you can view the ticket **Basic information** and **Application content**. You can also view the current state of the ticket.


<span id=".5a6h5om55bel5Y2V"></span>
## Approve a ticket


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Data management** \> **Ticket list**.

3. On the top menu bar, select the region.

4. On the **Ticket list** page, click **Permission application**.

5. On the **Data change** tab, click **Pending my approval**.

6. On the **Pending my approval** tab, click **Pass** or **Reject** in the **Actions** column of the target ticket.

   * **Pass**: Click **Pass** in the **Actions** column to allow the account to be granted the requested permissions.

   * **Refuse**: Click **Refuse** in the **Actions** column to refuse granting the requested permissions to the account.

7. In the **Confirm pass** or **Reject application** dialog box, click **OK**.
