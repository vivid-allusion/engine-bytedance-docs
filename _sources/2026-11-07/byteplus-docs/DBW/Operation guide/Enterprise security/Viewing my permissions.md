---
title: "Viewing my permissions"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Viewing_my_permissions"
---

The Database Workshop (DBW) console allows you to view the permissions currently assigned to your account.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* This topic is only applicable to sub\-accounts to view account information and permissions. The primary account has all permissions by default.

* If the DBW role or instance operation permissions of the current account do not meet your needs, you can apply for permissions as required. For detailed steps, refer to [Applying for permissions](https://docs.byteplus.com/en/docs/DBW/role-permission-request).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DBW Console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Enterprise security** \> **My permissions.** 

4. On the **My permissions** page, you can view all permissions available under the current account:

   * Basic information: In the **Basic information** area, you can view the current account's **username**, **DBW role**, **daily execution limit**, **daily query row limit**, and **Affiliated DBW user group**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can click the number next to the <strong>Affiliated DBW user group</strong> to view the user groups the current account is added to in the <strong>User group list</strong> dialog box. For detailed information on user groups, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-user-group-management">User group management</a>.      </div>
      

   * Permission information: In the **Permission list** area, you can view the operational permissions of the current account, including permissions for **RDS for MySQL**, **NDB for MySQL**, ** RDS for PostgreSQL**, and **RDS for SQL Server**, covering **instances**, **databases**, **tables**, or **columns**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If a BytePlus sub\-user is added to a user group and the sub\-user's permissions are modified in the sub\-user settings, the permission list will display the union of individual user and user group permissions.      </div>
