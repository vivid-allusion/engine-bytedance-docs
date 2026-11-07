---
title: "Creating an SQL review ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/creating-an-sql-review-ticket"
---

DBW provides the SQL review ticket feature, which helps you check for potential syntax errors and performance issues in SQL statements before submission. This enhances the standardization and systematization of database management, reduces human errors, and ensures the security, accuracy, and compliance of database operations. This topic explains how to create and approve SQL review tickets on the DBW console.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only instances with security control enabled are supported for creating SQL change tickets for management.

* Only users added within DBW User management can create tickets.

* When submitting multiple SQL statements at once, use semicolons (;) to separate them.

* Currently, only approval\-free submissions are supported during the approval workflow.

* If the instance status is not running, even if security control is enabled, you cannot create an SQL review ticket.

* After the intelligent review is completed, if the instance's security rules are disabled, the ticket can not be submitted.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance and account for RDS for MySQL have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_and_managing_an_account).

* The instance has enabled security control. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql).

* The user is added as a DBW role. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/Personal_user_management).

* Permissions related to adding users as DBW roles have been granted. For detailed steps, refer to [Permission management](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click **Create ticket**.

5. Create an SQL approval ticket.

   5. In the dialog box that appears, select **SQL audit ticket** \> **SQL audit**.

   2. On the **Create SQL review ticket** dashboard, configure the following parameters:

      
      |**Parameter** |**Description** |
      |---|---|
      |**Creator** |Defaults to the currently logged\-in account and can not be modified. |
      |**Ticket title** |Custom ticket title. The ticket title can not exceed 200 characters, and can not be empty. |
      |**Database type** |Only **RDS for MySQL** is supported currently. |
      |**Instance** |From the drop\-down list, select the target instance with security control enabled. |
      |**Database** |From the drop\-down list, select the target database. |
      |**SQLtext** |Enter SQL text. When multiple SQL statements are present, they must be separated by semicolons (;). |
      |**Approval template** |Only approval\-free submission is supported currently. |
      |**Ticket remarks** |Remarks. It is recommended to provide business\-related information. |
      

   3. Click **Submit ticket**.

6. Submit the approval ticket.

   When the SQL approval ticket is submitted, the system will automatically perform an intelligent review. The intelligent review will evaluate content against established security rule standards. You can click the ticket name to view the review details. If you confirm that the review results will not impact your business, you can proceed with the approval. For more information on security rules, refer to [References](https://docs.byteplus.com/en/docs/DBW/security-rule-management#.5Y-C6ICD5paH5qGj).

   1. On the **SQL audit** tab, click **Submit for approval** in the **Actions** column of the target ticket with **Ticket status** as **Intelligent review completed**.

   2. In the **Submit for approval** dialog box, set **Approval workflow**. The current **Approval workflow** only supports **Approval\-free**.

   3. Click **OK**.


<span id=".5ZCO57ut5pON5L2c"></span>
## Next steps

[Managing an SQL review ticket](https://docs.byteplus.com/en/docs/DBW/Managing_an_SQL_review_ticket)
