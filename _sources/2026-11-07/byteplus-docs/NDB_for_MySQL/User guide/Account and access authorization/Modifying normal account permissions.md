---
title: "Modifying normal account permissions"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_normal_account_permissions"
---

You can modify the permissions of a normal account as needed. This article describes how to modify the permissions of a normal account.

<span id="前提条件"></span>
## Prerequisites


* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance).

* An account has been created. For more information on specific operations, refer to [Creating an account](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts).

* The instance account type is a **Normal account**.


<span id="注意事项"></span>
## Precautions

Super accounts cannot modify account permissions through the console, and can only be reset to the initial state. For details, please refer to [Resetting super account permissions](https://www.byteplus.com/en/docs/NDB_for_MySQL/Resetting_super_account_permissions).

<span id="操作步骤"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Accounts**.

5. In the **Modify permissions** sidebar, reselect the permissions for the specified database for the target account. Currently supported permission types include: **Read/Write (DDL + DML)** , **Read\-only**, **DDL\-only**, **DML\-only**, **Custom permissions** (multiple choices). For the specific SQL operation permissions included in each permission type, see the [Account permission list](https://www.byteplus.com/en/docs/NDB_for_MySQL/Account_permission_description#账号权限列表).

   * **Setting permissions for a single database**

      1. Reselect the permission type from the drop\-down list in the **Permission** column of the target database. Click **Reset** to clear the original permissions.

         If you choose **Custom permissions**, you need to manually tick one or more SQL action permissions for them.

      2. When the selection is complete, click **OK** in the lower right corner of the drop\-down list.

   * **Bulk setting permissions**

      1. Check multiple target database names and click **Bulk settings permissions**.

      2. Select the permission type in the drop\-down list.

         If you choose **Custom permissions**, you need to manually tick one or more SQL action permissions for them.

      3. When the selection is complete, click **OK** in the lower right corner of the drop\-down list.

6. After all database authorization settings are completed, click **OK** to modify the normal account permissions.


<span id="相关-api"></span>
## Related APIs


|API |Description |
|---|---|
|[GrantDBAccountPrivilege](https://www.byteplus.com/en/docs/NDB_for_MySQL/GrantDBAccountPrivilege) |Calling the GrantDBAccountPrivilege gives the account permissions on the specified database. |
|[RevokeDBAccountPrivilege](https://www.byteplus.com/en/docs/NDB_for_MySQL/RevokeDBAccountPrivilege) |Call RevokeDBAccountPrivilege to revoke permissions to the database for the account. |
