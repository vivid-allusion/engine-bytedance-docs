---
title: "Changing account password"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Changing_account_password"
---

This article describes how to change the account password.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance).

* An account has been created. For more information on specific operations, refer to [Creating an account](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Accounts**.

5. On the **Accounts** tab, click **Change password** under the **Actions** column of the target account.

6. In the pop\-up dialog box, enter the **Password** and **Confirm password**, and click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The password rules are as follows:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The length is 8~32 characters.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It contains at least three of the following: uppercase letters, lowercase letters, digits, and special characters.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Special characters are <code>_ #!@$%^&*()+=-</code>.   </div>
   


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[ResetDBAccount](https://www.byteplus.com/en/docs/NDB_for_MySQL/ResetDBAccount) |Call the ResetDBAccount to change the account password. |
