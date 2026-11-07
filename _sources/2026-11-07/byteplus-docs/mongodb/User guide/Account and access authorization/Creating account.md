---
title: "Creating account"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/create-account"
---

After the Document Database for MongoDB instance is successfully created, the system will default to creating a super administrator account in the admin database. You can also create other accounts according to the business scenario and assign corresponding permissions to achieve operations of separating databases and authorities, thus realizing fine\-grained database management. This topic describes how to create accounts.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

The instance status must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The Document Database for MongoDB provides three types of accounts: super administrator account, high\-privileged account, and normal account. However, only high\-privileged accounts and normal accounts can be created. For more details about different types of accounts, refer to [Account type](https://docs.byteplus.com/en/docs/mongodb/account-overview#.6LSm5Y-357G75Z6L).

* Some keywords are disabled in the Document Database for MongoDB. When creating an account, please note:

   * The account name is not allowed to be the same as any of the following system\-reserved account names: `root`, `system_inspector`, `__system`, `mgr`.

      For example, you can set the account name to `test__system` or `__system__test`, but not to `__system`.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Except for the root account, the above\-mentioned system\-reserved accounts will not be displayed on the MongoDB console. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/viewing_account_information">Viewing account details</a>.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You don't need to pay attention to the permissions or operations of these system \- reserved accounts. It is highly recommended not to perform any modification, deletion, or renaming operations on these reserved accounts, otherwise, it will affect the normal operation of the database account.      </div>
      

   * The account name is not allowed to start with `vedb_mongodb_`.

      For example, you can set the account name to `testvedb_mongodb_`, but not to `vedb_mongodb_test`.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **Accounts** tab.

6. On **Accounts** tab, click **Create account**.

7. In the **Create database account** control panel, configure the following settings.

   
   |Parameter ||Required |Description |
   |---|---|---|---|
   |Basic account information |Database account |Required |Set the name of the account. The name must meet the following conditions simultaneously:<br><br><br>* The length is 1 to 32 characters.<br><br>* It consists of uppercase and lowercase letters, numbers, underscores (_), and hyphens (\-).<br><br>* Start with a letter and end with a letter or number.<br><br>* The account name is not allowed to be the same as any of the following system\-reserved account names: `root`, `system_inspector`, `__system`, `mgr`.<br><br>   For example, you can set the account name to `test__system` or `__system__test`, but not to `__system`.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Except for the root account, the above\-mentioned system\-reserved accounts will not be displayed on the MongoDB console. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/viewing_account_information">Viewing account details</a>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You don't need to pay attention to the permissions or operations of these system \- reserved accounts. It is highly recommended not to perform any modification, deletion, or renaming operations on these reserved accounts, otherwise, it will affect the normal operation of the database account.   </div><br>   <br><br>* The account name is not allowed to start with `vedb_mongodb_`.<br><br>   For example, you can set the account name to `testvedb_mongodb_`, but not to `vedb_mongodb_test`. |
   ||Target database |Required |Select the target database to which the newly created account belongs from the dropdown list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If no database is selected, the newly created account will by default belong to the admin database.</div><br> |
   ||Remarks |Optional |Set the remark information for the account. The remark information must meet the following conditions:<br><br><br>* The length should be 0 to 256 characters.<br><br>* It can contain numbers, Chinese characters, English letters, underscores (_), and hyphens (\-). |
   ||Password |Required |Set the password for the account. The password must meet the following requirements:<br><br><br>* Can only contain uppercase and lowercase letters, numbers, and the following special characters `_#!@$%^&*()+=-`.<br><br>* The length is 8 to 32 characters.<br><br>* Must contain at least three of the following: uppercase letters, lowercase letters, numbers, or special characters.<br><br>* Weak passwords that are easily cracked are not allowed (such as `Admin@123`).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you use special characters in the password, you might need to escape them when connecting to the instance. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/account-and-permission#.5b2T6L-e5o6l5Liy5Lit6LSm5Y-35a-G56CB5YyF5ZCr5LqG54m55q6K5a2X56ym5pe277yM5Li65L2V5Lya5a-86Ie06L-e5o6l5aSx6LSl77yf">Special characters requiring escaping</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For details on weak passwords prohibited in MongoDB, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/account-overview#.5byx5a-G56CB5YiX6KGo">Weak password list</a>.</div><br> |
   ||Confirm password |Required |Enter the password again for confirmation. |
   |Database permission settings |Admin database |Optional |Set the permissions the account has in the admin database from the dropdown list.<br><br>Permissions that can be granted to an account in the admin database: **read**, **userAdmin**, **readAnyDatabase**, **readWriteAnyDatabase**, **userAdminAnyDatabase**, **dbAdminAnyDatabase**, **clusterMonitor**, **backup**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If no admin database permissions are set, the account will not have any permissions for the admin database by default. For details on the permissions that can be granted for different types of databases, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/account-overview#.5pWw5o2u5bqT5LiO6LSm5Y-35p2D6ZmQ">Database and account permissions</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After the account is created, you can also modify the account permissions. For specific procedure, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modifying_account_privileges">Modifying account privileges</a>.</div><br> |
   ||Config database |Optional |Set permissions for the account in the config database. Only the **read** permission for the config database can be granted to new accounts.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If no config database permissions are set, the account will not have any permissions for the config database by default. For details on the permissions that can be granted for different types of databases, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/account-overview#.5pWw5o2u5bqT5LiO6LSm5Y-35p2D6ZmQ">Database and account permissions</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After the account is created, you can also modify the account permissions. For specific procedure, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modifying_account_privileges">Modifying account privileges</a>.</div><br> |
   ||Local database |Optional |Set permissions for the account in the local database. Only the **read** permission for the local database can be granted to newly created accounts.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If no local database permissions are set, the account will not have any permissions for the local database by default. For details on the permissions that can be granted for different types of databases, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/account-overview#.5pWw5o2u5bqT5LiO6LSm5Y-35p2D6ZmQ">Database and account permissions</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After the account is created, you can also modify the account permissions. For specific procedure, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modifying_account_privileges">Modifying account privileges</a>.</div><br> |
   ||Other databases |Optional |Set the permissions that the account has in other custom databases.<br><br>The following permissions can be granted to the account in other databases: **read**, **readWrite**, **dbAdmin**, **userAdmin**, **dbOwner**.<br><br>You can set permissions for each database individually according to your business needs, or set permissions for multiple databases in batches. The specific operation steps are as follows:<br><br><br>* Set permissions for each database individually<br><br>   1. Find the target database from the database list, and check the permissions of the newly created account in the current database in the drop\-down box of the **Permission** column.<br><br>   2. click **OK**.<br><br>* Set permissions for multiple databases in batches<br><br>   1. Check the databases for which you need to set permissions in batches in the database list.<br><br>   2. Click **Batch set permissions** in the lower left corner of the list.<br><br>   3. Check the permissions to be granted in the pop\-up permission list box, and click **OK**.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Batch setting permissions is only used to quickly set permissions for multiple databases. You can set permissions for different databases multiple times, and finally all permission configurations will be submitted together.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If no other database permissions are set, the account will not have any permissions for other databases by default. For details on the permissions that can be granted for different types of databases, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/account-overview#.5pWw5o2u5bqT5LiO6LSm5Y-35p2D6ZmQ">Database and account permissions</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After the account is created, you can also modify the account permissions. For specific procedure, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modifying_account_privileges">Modifying account privileges</a>.</div><br> |
   

8. Click **OK** in the lower right corner of the page.


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[CreateDBAccount](https://docs.byteplus.com/en/docs/mongodb/createdbaccount) |Call the CreateDBAccount API to create an account for a specified MongoDB instance. |
|[DescribeDBAccounts](https://docs.byteplus.com/en/docs/mongodb/describedbaccounts) |Call the DescribeDBAccounts API to query list of accounts for target MongoDB instance. |
