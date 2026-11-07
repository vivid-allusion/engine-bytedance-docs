---
title: "Denying normal users to display all databases"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/denying-normal-users-to-display-all-databases"
---

This article describes how to use stored procedures to deny normal users access to all databases.

<span id="prerequisite"></span>
## prerequisite

The SQL Server instance is connected. For more information, see [Connection instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connecting-an-instance).

<span id="precautions"></span>
## Precautions


* Only highly privileged accounts `veyun_user` have permission to deny normal users access to all databases.

* The rejection and recovery of the two usage methods described in this article must be used in pairs and cannot be used interchangeably.

* For permission conflicts between user and `public` roles, deny permission takes precedence over grant permission. Therefore, even if the `public` role has permissions to view the database, a user cannot view the database if denied individually.

* When adjusting permissions, it is recommended to verify the effect of relevant measures in the testing environment before applying them to the production environment to prevent inappropriate permission settings from affecting the normal function of the application.

* Currently, only instances of the base version type are supported to deny normal user display of all database operations.


<span id="operation-steps"></span>
## Operation steps

Command to select reject and restore methods on demand:


* Method 1: Operating Public Roles

   * Execute the following command to deny all users permission to view the database.

      ```sql
      EXEC [master].[dbo].[sp_rds_deny_view_any_database];
      ```
      

   * Select the following command as needed to restore all user view database permissions.

      * Directly execute the command to restore all users and display all databases:

         ```sql
         EXEC [master].[dbo].[sp_rds_deny_view_any_database] 'public', 1;
         ```
         

      * Pending parameter name to perform recovery All users Display all databases:

         ```sql
         EXEC [master].[dbo].[sp_rds_deny_view_any_database] @login_name = 'public', @action = 1;
         ```
         

      The parameters are described as follows:

      * `@login_name`: (Optional) Logins to refuse to view all databases. Defaults to the `public` role, if not specified, all databases cannot be viewed by all users by default (except SA).

      * `@Action`: (optional) Whether to restore all users to view the database, the value is as follows:

         * `0`: (default) denies restoring all user view database permissions.

         * `1`: Indicates that allowing all users to view database permissions is restored.

* Method 2: Operate the designated user

   * Select the following command to deny the specified user ( `login1`) permission to view the database.

      * Execute the command directly to deny the specified user ( `login1`) permission to view the database

         ```sql
         EXEC [master].[dbo].[sp_rds_deny_view_any_database] 'login1';
         ```
         

      * Pending parameter name denies specified user ( `login1`) view database permission

         ```sql
         EXEC [master].[dbo].[sp_rds_deny_view_any_database] @login_name = 'login1';
         ```
         

      The parameter `@login_name` denotes a login that denies all database permissions.

   * Execute the following command to restore the view database permissions for the specified user ( `login1`).

      * Directly execute the command to restore the specified user ( `login1`) to view database permissions:

         ```sql
         EXEC [master].[dbo].[sp_rds_deny_view_any_database] 'login1', 1;
         ```
         

      * Execute the command to restore the specified user ( `login1`) to view database permissions with parameters:

         ```sql
         EXEC [master].[dbo].[sp_rds_deny_view_any_database] @login_name ='login1',@action = 1;
         ```
         

         The parameters are as follows:

         * `@login_name`: A login that restores view all database permissions.

         * `@Action`: (Optional) Whether to restore the specified user's view database permission, the value is as follows:

            * `0`: (default) denies the specified user access to view the database.

            * `1`: Indicates that the specified user is allowed to resume viewing database permissions.
