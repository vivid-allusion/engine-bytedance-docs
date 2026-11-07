---
title: "Modifying password"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/reset-password"
---

Document Database for MongoDB provides account management features. After an account is successfully created, you can modify its password or permissions at any time. This topic describes how to modify database account password on the MongoDB console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* The instance status must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

* A database account has been created. For specific procedures, refer to [Creating account](https://docs.byteplus.com/en/docs/mongodb/create-account).

* Account type should be **High\-privileged account** or **Normal account**. For details on account types supported by MongoDB, refer to [Account type](https://docs.byteplus.com/en/docs/mongodb/account-overview).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Modifying the password may interrupt database connections currently using this account. Proceed with caution.

* If you use special characters in the password, you might need to escape them when connecting to the instance. For more details, refer to [Special characters requiring escaping](https://docs.byteplus.com/en/docs/mongodb/account-and-permission#.5b2T6L-e5o6l5Liy5Lit6LSm5Y-35a-G56CB5YyF5ZCr5LqG54m55q6K5a2X56ym5pe277yM5Li65L2V5Lya5a-86Ie06L-e5o6l5aSx6LSl77yf).

* To modify the password for the super administrator account, refer to [Reset root account](https://docs.byteplus.com/en/docs/mongodb/reset-root-account).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **Accounts** tab.

6. Find the account whose password needs to be modified in the account list, and click **Change password** in the **Actions** column on the left.

7. In the pop\-up dialog box, confirm the name of the account whose password needs to be modified first, and then enter the new password.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The new password must meet the following conditions:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Can only contain uppercase and lowercase letters, numbers, and the following special characters <code>_#!@$%^&*()+=-</code>.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The length is 8 to 32 characters.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Must contain at least three of the following: uppercase letters, lowercase letters, numbers, or special characters.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Weak passwords that are easily cracked are not allowed (such as <code>Admin@123</code>).   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you use special characters in the password, you might need to escape them when connecting to the instance. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/account-and-permission#.5b2T6L-e5o6l5Liy5Lit6LSm5Y-35a-G56CB5YyF5ZCr5LqG54m55q6K5a2X56ym5pe277yM5Li65L2V5Lya5a-86Ie06L-e5o6l5aSx6LSl77yf">Special characters requiring escaping</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For details on weak passwords prohibited in MongoDB, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/account-overview#.5byx5a-G56CB5YiX6KGo">Weak password list</a>.   </div>
   

8. Re\-enter and confirm the password, then click **OK**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Modifying the password may interrupt database connections currently using this account. Proceed with caution.   </div>
   

<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[DescribeDBAccounts](https://docs.byteplus.com/en/docs/mongodb/describedbaccounts) |Call the DescribeDBAccounts API to query list of accounts for target MongoDB instance. |
|[ResetDBAccount](https://docs.byteplus.com/en/docs/mongodb/resetdbaccount) |Call the ResetDBAccount API to modify password of specified account or reset the permissions of the root account to its initial state for target MongoDB instance. |
