---
title: "Creating database and account"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/creating_databases_and_accounts"
---

This topic describes how to create database and account for PostgreSQL instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance), and the instance is in the **Running** status.

<span id=".5Yib5bu65pWw5o2u5bqT"></span>
## Creating a database


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name to enter the instance details page.

5. At the top of the page, click **Databases**.

6. On the **Databases** tab, click ** Create database**, and in the dialog box that pops up, set the following parameters.



|Parameter |Description |
|---|---|
|Database name |Fill in the database name. The naming rules are as follows:<br><br><br>* The name is unique within the instance.<br><br>* 2 to 63 characters in length.<br><br>* Must start with a letter and end with a letter or a digit.<br><br>* Can contain letters, digits, underscores (_) and hyphens (\-).<br><br>* Some reserved words or keywords cannot be used in the database name, see [Reserved keywords](https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_forbidden_keywords) for all reserved keywords. |
|Character set |Select `UTF8`, `Latin1`, or `ASCII`. |
|Collate |String collation. |
|Ctype |Character set |
|Database owner |Select an account to be the owner of the database. This parameter is optional. You can also modify the database authorized by the account after the creation is complete.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Instance read\-only accounts, high\-privilege accounts with DDL privileges disabled, or normal accounts with DDL privileges disabled cannot be used as database owners.</div><br> |



7. Click **OK** to complete database creation.


<span id=".5Yib5bu66LSm5Y-3"></span>
## Creating an account


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name to enter the instance details page.

5. Click the **Accounts** tab on top of the page.

6. On the **Accounts** tab, click **Create account**, and set the following parameters in the pop\-up dialog box.



|Parameter |Description |
|---|---|
|Database account |Enter the account name. Naming rules are as follows:<br><br><br>* The name is unique within the instance.<br><br>* The account name length is 2 to 63 characters.<br><br>* Must start with a letter and end with a letter or a digit.<br><br>* Can contain letters, digits, underscores (_) and hyphens (\-).<br><br>* Some reserved characters or keywords are forbidden in database account names. For more information about a list of forbidden keywords, refer to [List of reserved keywords](https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_forbidden_keywords).<br><br>* Do not start the name with `pg_`. |
|Account type |Select **Super account**, **Normal account**, or **Instance read\-only account** as the account type.<br><br><br>* Super account: You can create multiple super accounts in an instance to manage all normal accounts and databases.<br><br>* Normal account: Multiple accounts can be created in one instance, and only operations permitted by permissions can be performed in authorized databases.<br><br>* Instance read\-only account: Multiple accounts can be created in one instance, only has read\-only permissions on all databases under the instance. |
|Password |Set the account password. Requirements are as follows:<br><br><br>* The password length is limited to 8~32 characters.<br><br>* The password consists of any three types of characters as follows: uppercase letters, lowercase letters, digits, and special characters.<br><br>* Special characters include `!@#$%^*&()_+-=`. |
|Confirm password |Enter the password again. |
|Account privileges |You can set the following permissions for your account:<br><br><br>* `Login`: Login.<br><br>* `Inherit`: Inheritance.<br><br>* `CreateRole`: Create a role.<br><br>* `CreateDB`: Creates the database.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The super account has all four permissions and does not need to be set separately.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Permissions can be set for normal accounts as required.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If you are creating an instance read\-only account, no account permission settings are required.</div><br> |



7. Click **OK**.


&nbsp;

&nbsp;
