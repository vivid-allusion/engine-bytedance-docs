---
title: "Manage members"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Manage_members"
---

Application delivery provides member management functionality, supports setting up application members and permissions, and meets the requirements for multi\-role collaboration in application delivery.

Each application's administrator has the authority to manage members, including adding members, modifying member permissions, deleting members, and more. This article introduces relevant actions for managing members.

<span id=".5re75Yqg5oiQ5ZGY"></span>
## Add members

Add new members to the current application, and associate an appropriate role with each member.


1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp), and in the left navigation pane, select **workspace**.

2. Click the target workspace name, then select **Application Delivery \> Application Management** in the left navigation bar of the current workspace.

3. Click the target application card to open the application. Click **settings** to switch to the settings tab.

4. In the permission management area, click **Add member**.

5. In the pop\-up search box, select the users to add; multiple selection is supported.

6. Click **OK**. The user will be successfully added to the member list.

7. Set members' permissions.

   The system provides five predefined roles: **Administrator**, **Developer**, **Tester**, **Operations**, and **Read\-only**. Members are assigned the **development** permission by default; this can be canceled by clearing the checkbox. A member must be associated with at least one role.


<span id=".5L-u5pS55oiQ5ZGY5p2D6ZmQ"></span>
## Modify member permissions

Modify the roles associated with members as needed. A member can be associated with multiple roles.


1. In the permission management area, locate the member whose permissions need to be modified and select the required roles for them.


<span id=".5Yig6Zmk5oiQ5ZGY"></span>
## Delete members

Delete members who no longer participate in this application.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The BytePlus account is the default administrator for the application and cannot be deleted.</div>



1. In the permissions management area, find the member you want to delete and click the **delete** button in the actions column.

2. In the pop\-up confirmation dialog box, click **Confirm** to delete this member.
