---
title: "Resetting super account permissions"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Resetting_super_account_permissions"
---

If you modify the permissions of the super account through SQL, you can restore the permissions of the account super to the original state by resetting the permissions. This article describes how to reset a super account.

<span id="前提条件"></span>
## Prerequisites


* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance).

* A **super account** has been created. For more information on specific operations, refer to [Creating an account](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts).


<span id="操作步骤"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Accounts**.

5. On the **Accounts** tab, click **Reset permissions** under the **Actions** column of the super account.

6. In the reset permissions dialog box that pops up, click **OK** to restore the permissions of the super account to its original state.


<span id="相关-api"></span>
## Related APIs


|API |Description |
|---|---|
|[ResetAccount](https://www.byteplus.com/en/docs/NDB_for_MySQL/ResetAccount) |Call the ResetAccount to reset the permissions of the super account. |
