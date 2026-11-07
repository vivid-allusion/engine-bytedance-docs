---
title: "Managing permission application tickets"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/managing-permission-application-tickets_"
---

This topic describes how to manage permission application tickets on the Database Workshop (DBW) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An operation permission ticket has been created. For detailed steps, refer to [Creating an operation permission ticket](https://docs.byteplus.com/en/docs/DBW/Create_operation_permission_ticket).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Approvers for ticket approval are set in the approval workflow when instance security control is enabled. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-control).

* DBW administrators can view all tickets, while DBW normal users can only view tickets they created or are assigned as approvers.


<span id=".5p-l55yL5bel5Y2V"></span>
## View a ticket

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">DBW administrators can view all ticket information, while DBW regular users can only view tickets they created or are assigned as approvers.</div>



1. Log in to the [DBW Console](https://console.byteplus.com/dbw).

2. Select the region from the top menu bar.

3. In the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click **Permission request**.

5. On the **Permission request** tab, you can view the following information:

   * View basic ticket information: On the **Permission Request** tab, you can view the **Ticket number**, **Request type**, **Ticket status**, **Reason for request**, **Creator**, **Current handler**, **Creation time**, **Last operation time**, and other details for all tickets.

   * View ticket details: On the **Permission request** tab, click the **Ticket number** of the target ticket. On the **Ticket details** page, you can view the ticket's **Basic information** and **Request content**. You can also check the current status of the ticket.


<span id=".5a6h5om55bel5Y2V"></span>
## Approve a ticket


1. Log in to the [DBW Console](https://console.byteplus.com/dbw).

2. Select a region from the top menu bar.

3. In the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click **Permission request**.

5. On the **Data change** tab, click **Pending my approval**.

6. On the **Pending my approval** sub\-tab, click **Approve** or **Reject** in the **Operation** column of the target ticket.

   * **Approve**: Click **Approve** under the **Operation** column to allow the account to be granted the requested permissions.

   * **Reject**: Click **Reject** under the **Operation** column to deny the account the requested permissions.

7. In the **Confirmation** or **Reject application** dialog, click **OK**.
