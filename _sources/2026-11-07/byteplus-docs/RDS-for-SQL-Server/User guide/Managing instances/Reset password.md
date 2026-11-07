---
title: "Reset password"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Reset_password"
---

You need to set a password for the super account when you create an instance. RDS for SQL Server also allows you to reset passwords after an instance is created. This topic describes how to reset the password for a super account.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

An instance has been created and is in the **Running** state. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the project and region where the instance is located.

3. In the **instances**, click the target instance to go to the **Instance information** page.

4. In the **Instance information** section on the **Instance information** page, click the **Reset password** button.

5. In the **Reset password** window, enter a password in the **Password** text box and re\-enter it in the **Confirm password** text box. The password must meet the following requirements:

   * It must be 8 to 32 characters long.

   * It must contain at least three of the following character types: uppercase letters, lowercase letters, numbers, and special characters.

   * Special characters are `!@#$%^&*()_+-=`.

   * It cannot contain `veyun_user` (case\-insensitive).

6. Click **Confirm** to complete the password reset.
