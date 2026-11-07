---
title: "Resetting root account"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/reset-root-account"
---

After the Document Database for MongoDB instance is successfully created, the system will automatically create a super administrator（that is, root） account in the admin database. You can change root account's password or restore the permissions of the root account to the initial state. This topic describes how to reset the root account on the console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* The instance status must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

* Account type should be **Super adminstrator account**. For details on account types supported by MongoDB, refer to [Account type](https://docs.byteplus.com/en/docs/mongodb/account-overview).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Modifying the password may cause the database connection using the current account to be interrupted. Please operate with caution.

* If you use special characters in the password, you might need to escape them when connecting to the instance. For more details, refer to [Special characters requiring escaping](https://docs.byteplus.com/en/docs/mongodb/account-and-permission#.5b2T6L-e5o6l5Liy5Lit6LSm5Y-35a-G56CB5YyF5ZCr5LqG54m55q6K5a2X56ym5pe277yM5Li65L2V5Lya5a-86Ie06L-e5o6l5aSx6LSl77yf).

* The permissions of the super administrator account can only be reset to the initial state and cannot be modified to specified permissions.

* If you need to modify the password or permissions of a high\-privileged account account or a normal account, refer to [Modifying password](https://docs.byteplus.com/en/docs/mongodb/reset-password) and [Modifying account privileges](https://docs.byteplus.com/en/docs/mongodb/modifying_account_privileges).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **Accounts** tab.

6. Find the root account in the account list, and click **Reset account** in the **Actions** column on the left.

7. Set the following configurations in the popped\-up dialog box.

   
   |Parameter |Description |
   |---|---|
   |Username |Confirm that the account to be reset is the root account. |
   |New password |Set a new password for the root account. The password must meet the following requirements:<br><br><br>* Can only contain uppercase and lowercase letters, numbers, and the following special characters `_#!@$%^&*()+=-`.<br><br>* The length is 8 to 32 characters.<br><br>* Must contain at least three of the following: uppercase letters, lowercase letters, numbers, or special characters.<br><br>* Weak passwords that are easily cracked are not allowed (such as `Admin@123`).<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Modifying the password may cause the database connection using the current account to be interrupted. Please operate with caution.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you use special characters in the password, you might need to escape them when connecting to the instance. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/account-and-permission#.5b2T6L-e5o6l5Liy5Lit6LSm5Y-35a-G56CB5YyF5ZCr5LqG54m55q6K5a2X56ym5pe277yM5Li65L2V5Lya5a-86Ie06L-e5o6l5aSx6LSl77yf">Special characters requiring escaping</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">For details on weak passwords prohibited in MongoDB, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/account-overview#.5byx5a-G56CB5YiX6KGo">Weak password list</a>.</div><br> |
   |Confirm password |Enter the password again for confirmation. |
   |Regrant permission |After checking, the account will be re\-granted with root permissions.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For details about the complete permissions that can be granted to the administrator account root, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/account-overview#.5pWw5o2u5bqT5LiO6LSm5Y-35p2D6ZmQ">Database and account permissions</a>.</div><br> |
   

8. Click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[DescribeDBAccounts](https://docs.byteplus.com/en/docs/mongodb/describedbaccounts) |Call the DescribeDBAccounts API to query list of accounts for target MongoDB instance. |
|[ResetDBAccount](https://docs.byteplus.com/en/docs/mongodb/resetdbaccount) |Call the ResetDBAccount API to modify password of specified account or reset the permissions of the root account to its initial state for target MongoDB instance. |
