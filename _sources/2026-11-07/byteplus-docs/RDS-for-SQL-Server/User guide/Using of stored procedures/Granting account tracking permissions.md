---
title: "Granting account tracking permissions"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/granting-account-tracking-permissions"
---

This article describes how to use stored procedures to grant account tracking permissions.

<span id="prerequisite"></span>
## prerequisite

The SQL Server instance is connected. For more information, see [Connection instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connecting-an-instance).

<span id="precautions"></span>
## Precautions


* Only highly privileged accounts `veyun_user` have permissions to grant account tracking permissions.

* When adjusting permissions, it is recommended to verify the effect of relevant measures in the testing environment before applying them to the production environment to prevent inappropriate permission settings from affecting the normal function of the application.

* After enabling the grant of trace permissions, the issues to be concerned about involve the proper allocation of permissions, auditing and log management, security configuration, data protection, access control, and so on. It is recommended that you carefully manage and regularly review your account after granting tracking privileges to ensure that permission settings and operations always comply with the principle of least privilege and security policies, thus effectively reducing the security risk of the database system. For more information, see [Security and Permissions](https://learn.microsoft.com/zh-cn/previous-versions/tn-archive/cc293611(v=technet.10)?redirectedfrom=MSDN).

* Granting account tracking permissions is currently only supported on instances of the base version type.


<span id="operation-steps"></span>
## Operation steps

On demand, allow or deny users tracking privileges in the following ways:


* Allow specified users to have tracking privileges

   * Directly execute the command to allow the specified user to have tracking privileges:

      ```sql
      exec [master].[dbo].[sp_rds_set_alter_trace] 'login2';
      ```
      

   * Execute the command with parameters to allow users to have trace privileges:

      ```sql
      exec [master].[dbo].[sp_rds_set_alter_trace] @login_name = 'login2';
      ```
      

      The parameter `@login_name` represents the account with tracking privileges.

* Deny specified user access to tracking

   * Directly execute the command to deny the specified user tracking privileges:

      ```sql
      exec [master].[dbo].[sp_rds_set_alter_trace]  'login2', 1;
      ```
      

   * Execute the command with parameters to deny the specified user the right to trace:

      ```sql
      exec [master].[dbo].[sp_rds_set_alter_trace] @login_name = 'login2', @action = 1;
      ```
      

      Among them, the parameter description is as follows:

      * `@login_name`: denies a login that specifies that the user has tracking privileges.

      * `@Action`: (optional) Whether to deny the specified user tracking permission, the value is as follows:

         * `0`: (default) denies the specified user access to trace.

         * `1`: Allows the specified user to have tracking privileges.
