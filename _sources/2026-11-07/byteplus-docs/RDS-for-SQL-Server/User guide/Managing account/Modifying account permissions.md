---
title: "Modifying account permissions"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/modifying-account-permissions"
---

You can modify the permissions of the normal account as needed. This article describes how to modify the permissions of a normal account in the SQL Server Edition console of a cloud database.

<span id="prerequisite"></span>
## prerequisite


* An instance has been created and the instance state is **running** . For more details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

* A regular account has been created. For more information, see [Create and manage accounts](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-and-managing-account).


<span id="precautions"></span>
## Precautions


* Modifying account permissions may affect the normal operation of the business, and caution is required.

* High\-authority accounts have all permissions by default, and do not support modifying the permissions of high\-authority accounts.

* The accounts dbw_admin, dbm_login, Rdsadmin, and veyun_user are internal special accounts, only used for internal automated operation and maintenance. They will not record or modify the data in the business database and will not have any special impact on your business. However, operating these accounts may cause some functions of the cloud database SQL Server edition to become unavailable. Therefore, do not perform any operations including `CREATE`, `ALTER`, `DROP`, etc. on the internal accounts.


<span id="operation-steps"></span>
## Operation steps


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **instance list** page, click the target instance name.

4. At the top of the page, click the **Account Management** tab.

5. On the **Account Management** tab, click Modify permissions for the target account action column.

6. In the **Modify Permissions** panel, modify the relevant permissions.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When modifying permissions, the permissions policy for batch account modification is supported.   </div>
   

7. Click **OK**.
