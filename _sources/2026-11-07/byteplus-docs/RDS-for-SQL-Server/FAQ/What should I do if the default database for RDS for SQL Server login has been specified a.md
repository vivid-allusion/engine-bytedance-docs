---
title: "What should I do if the default database for RDS for SQL Server login has been specified as custom database, but the properties of the default database cannot be synchronized to the standby database?"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/what-should-I-do-if-the-default-database-for-rds-for-sql-server-login-has-been-specified-as-custom-d"
---

<span id="problem-description"></span>
## Problem description

When the default database for a SQL Server login has been designated as a custom library, but the properties of the default database cannot be synchronized to the standby database, a restart or switch operation may affect the login account as follows:


* **Connection with no database name specified**: If you do not specify a specific database name in the connection string, SQL Server attempts to use the default database when logging in. When the default database properties are not synchronized to the standby, the login is connected to the master database by default. If you try to execute a query for a custom library in the master database, an error may be thrown.

* **Connections that specify the database name**: If you explicitly specify the database name in the connection string, such connections are not affected regardless of whether the default database properties are synchronized, and queries are executed directly in the specified database.


<span id="solution"></span>
## Solution

You can manually modify the default database. When you find that the properties of the default database are not synchronized after the switch, you can manually modify the default database of the login account. The specific operation is as follows:


1. Connect instances. For more details, see [Connection instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connect-instance).

2. In the left navigation bar, select **Security** \> **Logins**.

3. Right\-click the target account and click **Properties**.

4. On the login account's **Properties** page, set up **Default database**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended that <strong>Default database</strong> be set to <strong>master</strong>.   </div>
   

5. Click **OK**.
