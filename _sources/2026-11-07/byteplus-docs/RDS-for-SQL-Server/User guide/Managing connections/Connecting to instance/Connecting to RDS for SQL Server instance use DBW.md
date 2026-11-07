---
title: "Connecting to RDS for SQL Server instance use DBW"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connecting-to-rds-for-sql-server-instance-use-dbw"
---

Database Workbench (DBW) is a unified cloud management platform for multi\-type database lifecycle management. You can use DBW to help you quickly connect remotely and manage SQL Server databases online. This article describes how to connect to a RDS for SQL Server instance through DBW.

<span id="background-information"></span>
## Background information

Database Workbench DBW is a database SaaS product that integrates database graphical user interface (GUI), troubleshooting and auditing. It provides Web end point management capabilities such as comprehensive observation and analysis, intelligent risk checking and autonomous operation and maintenance, and provides you with stable, secure and efficient database management Cloud as a Service. For more details, see [What is a Database Workbench](https://docs.byteplus.com/en/docs/DBW/what-is-database-workbench).

<span id="prerequisite"></span>
## prerequisite

An instance of RDS for SQL Server has been created and is **running**. Instance creation methods, see [Creating Instances](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

<span id="precautions"></span>
## Precautions


* When you log in to a RDS for SQL Server instance through DBW, you need to authorize the addition of the DBW service IP to the RDS for SQL Server instance whitelist. After authorization, the system will automatically create a whitelist named `DBW_Sole_ *** _ *** * _For_mssql` on the side of the RDS for SQL Server instance (the whitelist will contain the service IP of DBW), and bind the whitelist to the target RDS for SQL Server instance.

* When using DBW to connect to a RDS for SQL Server instance, do not modify, unbind, or delete the above whitelist, as this will cause the target RDS for SQL Server instance to fail to connect.

* Login to primary and read\-only instances is supported.


<span id="operation-steps"></span>
## Operation steps


1. Set the RDS for SQL Server instance connection parameters by entering the instance connection dialog box of the DBW data interaction table by any of the following methods.

   * Method 1: Through the RDS for SQL Server console

      1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

      2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

      3. On the Instance List page, click the Login Workbench in the Target Instance Actions column.

   * Option 2: Through the DBW console

      1. Log in to [the DBW console](https://console.byteplus.com/dbw/region:dbw+ap-southeast-1/).

      2. In the upper left corner of the top menu bar, select the project and region to which the target RDS for SQL Server instance belongs.

      3. In the left navigation bar, select **Data Management** \> **Data Interaction Desk**.

2. In the **database workbench DBW** dialog box, set the relevant parameters as shown in the following table.

   
   |**parameter** |**explain** |
   |---|---|
   |**instance type** |Select **RDS for SQL Server** from the drop\-down list. |
   |**instance name** |Select the target instance from the drop\-down list. |
   |**database account** |Enter the database account name. |
   |**Database password** |Enter the database account password. |
   |**database name** |(Optional) Enter the database name on demand, the default is the `master` library. |
   

3. Check **Authorize Database Workbench to add service IPs to the corresponding database instance whitelist**, and click **Login**.


<span id="follow-up-operation"></span>
## follow\-up operation

After successfully connecting to a RDS for SQL Server instance through DBW, you can manage the database instance by executing various command statements in the command window of the DBW's Data Interaction Desk.
