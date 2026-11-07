---
title: "User role description"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/role-description"
---

This article describes the user roles provided by DBW, including system roles and ticket approval roles.


|**Type** |**Role** |**Description** |**Privilege** |
|---|---|---|---|
|System role |Administrator |* The primary account of Volcengine is Defaulted as the Administrator of DBW, namely RootAccount.<br><br>* Sub\-users can be set as administrators with no quantity limit. |* The primary account has all permissions under the account by default.<br><br>* DBW administrators have default access to all DBW features.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only administrators can have permissions such as user management, security control, and security rules. For details, see <a href="https://docs.byteplus.com/en/docs/DBW/user-management?lang=en">User introduction</a>.</div><br> |
||Normal user |Normal users are sub\-users and a type of identity for access control, created by administrators with no quantity limit. |Normal users have partial DBW permissions. For details, see [User introduction](https://docs.byteplus.com/en/docs/DBW/user-management?lang=en). |
|Resource role |Instance owner |* Both administrator role and normal role can be set as the owner. It is suggested to set the administrator role as the instance owner.<br><br>* The instance owner is the default first\-level ticket approver in the system default template.<br><br>* Each instance can have multiple owners.<br><br>* Only administrator role can modify the owner. |* All read and write permissions under this database instance.<br><br>* Corresponds to the owner node in the default approval workflow. |
||Instance DBA |* Both administrator role and normal role can be set as DBA. It is suggested that you set the administrator role as instance DBA.<br><br>* Instance DBA will default to the second\-level ticket approver in the system default template.<br><br>* Each instance can have multiple DBAs.<br><br>* Only the administrator role can modify the DBA. |* All read and write permissions under this database instance.<br><br>* Corresponds to the DBA node in the default approval workflow. |
||Instance Admin |* The administrator role defaults to instance Admin.<br><br>* The administrator defaults to the approver of the three\-level ticket approval in the system default template. |* All read and write permissions under this database instance.<br><br>* Corresponds to the Admin node in the default approval workflow. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Sub\-users not added to DBW user management are not recognized as individual users or user groups within DBW. Therefore, they do not support instance security control, passwordless login for the Data Interaction Console, or platform features such as user management, security control, and ticket lists. To ensure a full feature experience, we recommend adding BytePlus sub\-users to DBW's individual users or user groups.</div>


<span id="4x8nfkkd"></span>
## View roles


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. In the left\-side navigation pane, select **Corporate security** \> **My permission**.

3. On the **My permission** page, locate the **Basic information** section to view your **DBW role**.

   * If your account is the primary account, you can view the username and DBW role on this page.

   * If your account has a DBW system role (Normal user or Administrator), you can apply for additional permissions on this page.

   * If your account does not have a DBW system role, you can apply to become one on this page.
