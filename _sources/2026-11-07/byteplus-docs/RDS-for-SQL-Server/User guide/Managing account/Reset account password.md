---
title: "Reset account password"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/resetting-account-password"
---

This topic describes how to reset the passwords for the super account, normal accounts, and the system admin account in the RDS for SQL Server console.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The System Admin account feature is available on an allowlist basis. To request access, <a href="https://console.byteplus.com/workorder/create">Submit a ticket</a> to contact the SQL Server technical team.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance has been created and the instance state is **Running**. For detailed operations, see [Create an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

* To reset the password of a **normal account** or a **system admin account**, you must first create the account. For detailed steps, refer to [Creating and managing an account](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-and-managing-account).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the project and region where the instance is located.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click the **Account management** tab.

5. On the **Account management** tab, click **Reset password** in the **Actions** column for the target account.

6. In the **Reset password** dialog box, set a new password for the database account. The password rules for different account types are as follows:

   
   <Tabs>
   <Tab zoneid="Vmf7ZDkass" title="Super account">
   <TabTitle>Super account</TabTitle>
   
   * The length must be between 8 and 32 characters.
   
   * Contain at least three of the following: uppercase letters, lowercase letters, numbers, or special characters.
   
   * Special characters include `~!@#$%^&*()-_+=?`.
   
   * Cannot contain `veyun_user` (case\-insensitive)
   
   
   </Tab>
   <Tab zoneid="DJibH7oLOn" title="Normal account">
   <TabTitle>Normal account</TabTitle>
   
   * The length must be between 8 and 32 characters.
   
   * Contain at least three of the following: uppercase letters, lowercase letters, numbers, or special characters.
   
   * Special characters include `~!@#$%^&*()-_+=?`.
   
   
   </Tab>
   <Tab zoneid="Qr5uN4Dpxw" title="SystemAdmin account">
   <TabTitle>SystemAdmin account</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">The System Admin account feature is available on an allowlist basis. To request access, <a href="https://console.byteplus.com/workorder/create">Submit a ticket</a> to contact the SQL Server technical team.</div>
   
   
   
   * The length must be between 8 and 32 characters.
   
   * Contain at least three of the following: uppercase letters, lowercase letters, numbers, or special characters.
   
   * Special characters include `~!@#$%^&*()-_+=?`.
   
   
   </Tab>
   </Tabs>
   

7. Click **OK**.
