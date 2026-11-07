---
title: "DBW role application"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/role-permission-request"
---

This article describes how sub\-users can apply to become a DBW role on the Database Workshop (DBW) console.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* This article applies only to normal users of non\-DBW system roles and DBW applying for related permissions. DBW administrators do not need to apply.

* When you first log in to DBW's User management with a BytePlus IAM user that has the `AdministratorAccess` permission policy, follow the prompts to authorize DBW to access the official IAM configuration. DBW will then automatically initialize the IAM user as an administrator role.

* IAM users who have been added as administrators may not have the `AdministratorAccess` permission policy.

* Non\-DBW system roles support only the creation of DBW role tickets.

* All administrators in DBW can approve DBW role application tickets.

* The approver is all administrators added to DBW.


<span id=".55Sz6K-3LWRidy3op5LoibI="></span>
## Apply for a DBW role


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click **Create ticket**.

5. In the dialog box, go to **Permission application** \> **DBW role**.

6. In the **Create DBW role ticket** panel, configure the following parameter information.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Applicant** |Defaults to the currently logged\-in account and can not be modified. |
   |**Ticket title** |Optional. Custom ticket title. The ticket title can not exceed 200 characters. |
   |**Application type** |Defaults to the DBW role and cannot be modified. |
   |**DBW role**<br><br> |Select a DBW role as needed. The values are as follows:<br><br><br>* **Administrator**: By default, administrators have all DBW permissions for this account.<br><br>* **Normal user**: Normal users have some DBW functional permissions.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For detailed information about DBW roles, see <a href="https://docs.byteplus.com/en/docs/DBW/role-description?lang=zh">Role description</a>.</div><br> |
   |**Daily execution limit** |1. Set the upper limit on the number of execution times for the DBW role per day as needed. The default value is 2,000, and its range is 1 to 999,999,999.<br><br>2. Set the validity period for the maximum number of daily executions. Currently, the options include **Permanent valid**, **Valid for 6 months**, **Valid for 3 months (default)** , **Valid for 1 month**, **Valid for 2 weeks**, **Valid for 7 days**, **Valid for the day**, and **Customize**. The default validity period is **valid for 3 months**.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">To execute SQL, the SQL execution permission of the database object must be authorized for the user.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The default number of days per month is 30.</div><br> |
   |**Daily query row limit** |1. Set the upper limit on the number of rows queried daily by the DBW role as needed. The default is 2000 times, and the value range is 1 to 999999999.<br><br>2. Set the validity period for the daily query row limit. Currently, the options include **Permanent valid**, **Valid for 6 months**, **Valid for 3 months (default)** , **Valid for 1 month**, **Valid for 2 weeks**, **Valid for 7 days**, **Valid for the day**, and **Customize**. The default validity period is **valid for 3 months**.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">To query SQL, the SQL query permission of the database object must be authorized for the user.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The default number of days per month is 30.</div><br> |
   |**Ticket remarks** |Note the reason why you applied for this DBW role for administrator approval. |
   

6. Click **Submit application**.


<span id=".5ZCO57ut5pON5L2c"></span>
## Next steps


* After you complete the application for the DBW user role, you can continue to apply for the operation permission of the corresponding Instance. The detailed operations are as follows:

   * [Applying for operation permissions related to RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket)

   * [Applying for operation permissions related to veDB for MySQL](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket)

   * [Applying for operation permissions related to RDS for PostgreSQL](https://docs.byteplus.com/en/docs/DBW/Create_operation_permission_ticket)

   * [Applying for operation permissions related to RDS for SQL Server](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket_)

   * [Applying for operation permissions related to Cache for Redis.](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket-for-redis?lang=en)

* If you are an administrator of DBW, on the **Permission application** tab, you can view all ticket orders for the applied roles and support approval. The details are as follows:

   * **Pass**: After clicking Pass, the sub\-user will be granted the relevant role of DBW.

   * Refuse: After clicking **Refuse**, the sub\-user will not be granted the requested DBW role.

* If you are a Normal user of DBW or a non\-DBW system role, you can only view the tickets you applied for on this page.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

To learn how to view the role or operation permissions of the current [My permission](https://docs.byteplus.com/en/docs/DBW/Viewing_my_permissions) in DBW, see .
