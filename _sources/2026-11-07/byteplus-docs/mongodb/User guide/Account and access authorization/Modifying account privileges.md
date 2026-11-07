---
title: "Modifying account privileges"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/modifying_account_privileges"
---

Document Database for MongoDB provides account management features. After an account is successfully created, you can modify its password or permissions at any time. This topic describes how to modify account permissions on the MongoDB console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* The instance status must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

* A database account has been created. For specific procedures, refer to [Creating account](https://docs.byteplus.com/en/docs/mongodb/create-account).

* Account type should be **High\-privileged account** or **Normal account**. For details on account types supported by MongoDB, refer to [Account type](https://docs.byteplus.com/en/docs/mongodb/account-overview).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The permissions of the super administrator account can only be reset to the initial state and cannot be modified to specified permissions. For specific procedure of resetting the permissions of the super administrator account, refer to [Resetting root account](https://docs.byteplus.com/en/docs/mongodb/reset-root-account).

* Modifying account permissions may cause errors such as lack of access rights when the current account connects to the corresponding database, affecting business operations. Please operate with caution.

* This modification will reset all permissions for this account. The account will have only the permissions granted on this page. Permissions previously set via **DBW**, **third\-party clients**, or other means will not be retained. Please verify carefully before confirming.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **Accounts** tab.

6. Find the account whose permissions need to be modified in the account list, and click **Modify permissions** in the **Actions** column on the left.

7. In the pop\-up control panel, set the following configurations.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This modification will reset all permissions for this account. The account will have only the permissions granted on this page. Permissions previously set via <strong>DBW</strong>, <strong>third\-party clients</strong>, or other means will not be retained. Please verify carefully before confirming.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Modifying account permissions may cause errors such as lack of access rights when the current account connects to the corresponding database, affecting business operations. Please operate with caution.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Different database types allow different account permissions to be granted. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/account-overview#.5pWw5o2u5bqT5LiO6LSm5Y-35p2D6ZmQ">Database and account permissions</a>.   </div>
   

   
   |Parameter |Description |
   |---|---|
   |Database account |Confirm the name of the database account whose permissions need to be modified. |
   |Admin database |Set the permissions the account has in the admin database from the dropdown list.<br><br>Permissions that can be granted to an account in the admin database: **read**, **userAdmin**, **readAnyDatabase**, **readWriteAnyDatabase**, **userAdminAnyDatabase**, **dbAdminAnyDatabase**, **clusterMonitor**, **backup**. |
   |Config database |Set permissions for the account in the config database. Only the **read** permission for the config database can be granted to accounts. |
   |Local database |Set permissions for the account in the local database. Only the **read** permission for the local database can be granted to accounts. |
   |Other databases |Set the permissions that the account has in other custom databases.<br><br>The following permissions can be granted to the account in other databases: **read**, **readWrite**, **dbAdmin**, **userAdmin**, **dbOwner**.<br><br>You can set permissions for each database individually according to your business needs, or set permissions for multiple databases in batches. The specific operation steps are as follows:<br><br><br>* Set permissions for each database individually<br><br>   1. Find the target database from the database list, and check the permissions of the newly created account in the current database in the drop\-down box of the **Permission** column.<br><br>   2. click **OK**.<br><br>* Set permissions for multiple databases in batches<br><br>   1. Check the databases for which you need to set permissions in batches in the database list.<br><br>   2. Click **Batch set permissions** in the lower left corner of the list.<br><br>   3. Check the permissions to be granted in the pop\-up permission list box, and click **OK**.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Batch setting permissions is only used to quickly set permissions for multiple databases. You can set permissions for different databases multiple times, and finally all permission configurations will be submitted together.   </div><br>    |
   

8. Click **OK** in the lower right corner of the page.


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[DescribeDBAccounts](https://docs.byteplus.com/en/docs/mongodb/describedbaccounts) |Call the DescribeDBAccounts API to query list of accounts for target MongoDB instance. |
|[UpdateDBAccountPrivilege](https://docs.byteplus.com/en/docs/mongodb/updatedbaccountprivilege) |Call the UpdateDBAccountPrivilege API to modify the privileges or account description of a specified account in the target MongoDB instance. |
