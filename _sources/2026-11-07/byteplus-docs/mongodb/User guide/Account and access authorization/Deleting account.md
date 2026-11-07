---
title: "Deleting account"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/delete_account"
---

The Document Database for MongoDB provides account management function. You can delete database accounts that are no longer needed. This topic describes how to delete an account on the console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* The instance status must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

* A database account has been created. For specific procedures, refer to [Creating account](https://docs.byteplus.com/en/docs/mongodb/create-account).

* Account type should be **High\-privileged account** or **Normal account**. For details on account types supported by MongoDB, refer to [Account type](https://docs.byteplus.com/en/docs/mongodb/account-overview).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Deleting the super administrator account root is not allowed, but you can change the password of root or reset the permissions of the root account to the initial state. For specific procedures, refer to [Resetting password](https://docs.byteplus.com/en/docs/mongodb/reset-root-account).

* A deleted account cannot be restored. Deleting an account may interrupt connections that use it, so proceed with caution.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **Accounts** tab.

6. Find the account to be deleted in the account list, and ** ** select  **...**  \> **Delete** in the **Actions** column on the left.

7. In the pop\-up dialog box, confirm the name of the account to be deleted again, and click **OK**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">A deleted account cannot be restored. Deleting an account may interrupt connections that use it, so proceed with caution.   </div>
   

<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[DescribeDBAccounts](https://docs.byteplus.com/en/docs/mongodb/describedbaccounts) |Call the DescribeDBAccounts API to query list of accounts for target MongoDB instance. |
|[DeleteDBAccount](https://docs.byteplus.com/en/docs/mongodb/deletedbaccount) |Call the DeleteDBAccount API to delete the specified account in the target MongoDB instance. |
