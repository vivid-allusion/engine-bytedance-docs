---
title: "Creating a database"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_database"
---

To use RDS for MySQL, you need to create a database in an instance first. This topic describes how to create a database for a MySQL instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance has been created and the instance state is **Running**. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If no project is set, you should select the option <strong>All resources</strong> at this step.   </div>
   

3. In the left navigation bar, choose **MySQL** \> **Instances**.

4. On the **Instances** page, click the target instance name.

5. On the target instance page, click **Database**.

6. On the **Database** tab, click **Create database**, and set the following parameters on the database creation panel.

   
   |Parameters |Description |
   |---|---|
   |Database name |Required. Fill in the database name.Naming rules are as follows:<br><br><br>* The name must be unique.<br><br>* The name length is limited to 2–64 characters.<br><br>* It starts with a letter and ends with a letter or a digit.<br><br>* The name consists of letters, digits, underscores ( _ ), or hyphens ( \- ).<br><br>* Certain reserved words cannot be used, including `root`, `admin`, and forbidden keywords.For all forbidden keywords, refer to [List of forbidden keywords](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_forbidden_keywords). |
   |Description |Optional.Description of the database. The length should not exceed 256 characters and can include digits, Chinese, English, underscores (_), and dashes (\-). |
   |Character set |Required. `utf8`, `latin1`, `utf8mb4`, or `ascii` can be selected. |
   |Authorized account |Add a general account authorized for database access.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter can be left blank, and you can bind the account after creating the database. For more information, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_account_permissions">Modifying account permissions</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Since the super account has all permissions by default, only general accounts are allowed to be authorized here.</div><br> |
   |Account Permissions |Required. Choose the permissions of the account for the corresponding database: **Read/Write**, **Read\-only**, **DDL only**, **DML only**, or **Customize**.<br><br><div data-tips="true" data-tips-type="tip">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only when a specific account is selected in <strong>Authorized account</strong> do you need to choose the account type.</div><br> |
   |Custom permissions |Required. Customize the permissions of the authorized account for the current database.<br><br><div data-tips="true" data-tips-type="tip">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only when <strong>Customize</strong> is selected as the <strong>Account type</strong> can you customize the account permissions.</div><br><br><br><br>* `SELECT`<br><br>* `INSERT`<br><br>* `UPDATE`<br><br>* `DELETE`<br><br>* `CREATE`<br><br>* `DROP`<br><br>* `REFERENCES`<br><br>* `INDEX`<br><br>* `ALTER`<br><br>* `CREATE TEMPORARY TABLES`<br><br>* `LOCK TABLE`<br><br>* `EXECUTE`<br><br>* `CREATE VIEW`<br><br>* `SHOW VIEW`<br><br>* `EVENT`<br><br>* `TRIGGER`<br><br>* `CREATE ROUTINE`<br><br>* `ALTER ROUTINE` |
   

7. Click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Note |
|---|---|
|[CreateDatabase](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdatabase1) |Call CreateDatabase API to create a database. |
