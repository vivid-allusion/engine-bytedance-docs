---
title: "Creating database"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-database"
---

Before using RDS for SQL Server, you need to create a database in your instance. This article describes how to create a database in the RDS for SQL Server console.

<span id="prerequisite"></span>
## prerequisite

An instance has been created and the instance state is **running**. For more details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

<span id="operation-steps"></span>
## Operation steps


1. Log in to [the RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **instance list** page, click the target instance name.

4. At the top of the page, click the **Database Administration** tab.

5. On the **Database Administration** tab, click **Create Database** .

6. In the **Create Database** panel, configure the following parameters.

   
   |**parameter** |**explain** |
   |---|---|
   |**database name** |Customize the database name as follows:<br><br><br>* Start with a letter and end with a letter or number.<br><br>* The length should be between 2 and 60 characters.<br><br>* Consists of letters, numbers, and underscores (_), and the case of letters is insensitive.<br><br>* Cannot use reserved words such as `master`, `msdb`, `model`, `tempdb`, `resource`, `rdsadmin`, `distribution`, etc. |
   |**Authorized account** |Select the permission policy in the drop\-down list of the permissions column of the target account. The permission policy supports selecting **owner**, **read\-write**, and **read\-only**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When authorizing an account, it supports granting <strong>owner</strong>, <strong>read\-write</strong> or <strong>read\-only</strong> permissions to the account in bulk.</div><br> |
   

7. Click **OK**.
