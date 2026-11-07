---
title: "How to change the locale of rds for sql server?"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/how-to-change-the-locale-of-rds-for-sql-server"
---

This article describes how to modify the SQL Server locale to Chinese.

<span id="modify-the-default-locale-of-an-instance-through-the-sql-server-console"></span>
## Modify the default locale of an instance through the SQL Server console

This method only works for newly created accounts, and the created accounts are still in the language environment before modification. To modify the locale of a created account, see [Modifying the default locale of an instance account via SSMS](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/how-to-change-the-locale-of-rds-for-sql-server).


1. Gets the value of the instance parameter `default language` when changing the locale of the instance to Simplified Chinese:

   1. Connect the instance via SSMS. For more details, see [Connection instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connect-instance).

   2. Open a session and execute the following command to view the value in Simplified Chinese:

      ```sql
      EXEC sp_helplanguage;
      ```
      

   The expected output is shown in the figure below, which shows that the value of the instance parameter `default language` is `30` when the locale is Simplified Chinese.

2. Sets the value of the instance parameter `default language`.

   1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

   2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

   3. In the left navigation bar, click **Instance List**.

   4. On the **Instance List** page, click the name of the target instance.

   5. On the target instance details page, click **Parameter Configuration**.

   6. On the **parameter configuration** tab, modify the parameter run value column of the parameter `default language` **parameter run value column of the parameter default language** to **30**.

   7. Click **Submit** at the top left of the page, **confirm Modify instance parameters?**  Dialog box Click **OK**.


<span id="modify-the-default-locale-of-the-instance-account-through-ssms"></span>
## Modify the default locale of the instance account through SSMS

This method can modify the default locale of the specified account.


1. Connect the instance via SSMS. For more details, see [Connection instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connect-instance).

2. In the left navigation bar, select **Security** \> **Logins**.

3. Right\-click the target account and click **Properties**.

4. On the **Properties** page of the login account, set the **Default language**.

   Set **Default language** to **Simplified Chinese \- Simplified Chinese**.

5. Click **OK**.


After completing the modification, you need to reopen a session to verify that the locale modification was successful.

<span id="modify-the-locale-of-the-current-session-via-ssms"></span>
## Modify the locale of the current session via SSMS

This method can only modify the locale of the current session and does not apply to reopened new sessions.


1. Connect the instance via SSMS. For more details, see [Connection instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connect-instance).

2. Execute the following command to modify the locale of the current session:

   ```sql
   SET LANGUAGE 'Simplified Chinese';
   ```
   

3. Execute the following command to verify that the locale of the current session was successfully modified:

   ```sql
   SELECT DATENAME (weekday, GETDATE ()) AS'Today is';
   ```
