---
title: "How do I query the time zone and character set of RDS for SQL Server instance?"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/how-do-I-query-time-zone-and-character-set-of-rds-for-sql-server-instance"
---

This article describes how to view the time zone and instance character set of a SQL Server instance.

<span id="view-the-time-zone-where-the-sql-server-instance-is-located"></span>
## View the time zone where the SQL Server instance is located


* Method 1: View the time zone where the instance is located through the console

   1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

   2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

   3. On the **instance list** page, click the target instance name.

   4. In the Instance Information area of the Target Instance Instance In tab, you can view the time zone of the target instance.

* Method 2: Check the time zone of the instance through SSMS

   1. Connect the instance via SSMS. For more details, see [Connection instance ](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connect-instance).

   2. Open a session and execute the following command to view the time zones supported by the instance.

      ```sql
      SELECT master.dbo.rds_fn_get_tz_info();
      ```
      


<span id="view-instance-character-sets"></span>
## View instance character sets


* Method 1: View the instance's character set through the console

   1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

   2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

   3. On the **instance list** page, click the target instance name.

   4. In the Instance Information area of the Target Instance Instance In tab, you can view the character set of the target instance.

* Method 2: View the instance character set through SSMS

   1. Connect the instance via SSMS. For more details, see [Connection instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connect-instance).

   2. Open a session and execute the following command to see the character sets supported by the instance.

      ```sql
      SELECT SERVERPROPERTY('Collation') AS InstanceCollation;
      ```
