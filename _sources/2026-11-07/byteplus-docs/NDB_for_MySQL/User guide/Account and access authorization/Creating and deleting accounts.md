---
title: "Creating and deleting accounts"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts"
---

This article describes how to create and delete a database account for instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Accounts created through SQL that do not comply with naming conventions can be modified and deleted in the console, but cannot be searched through the console's search bar.

<span id=".5Yib5bu66LSm5Y-3"></span>
## Create account


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Accounts**.

5. On the **Accounts** tab, click **Create account**, and in the dialog box that pops up, set the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Database account |The name of the account. This parameter is required, and the naming rules are as follows:<br><br><br>* The account name is unique under the current instance.<br><br>* It starts with a letter and ends with a letter or a digit.<br><br>* It must consist of letters, numbers, underscores (_) and hyphens (\-). The name length is limited to 2–32 characters.<br><br>* Account names cannot use certain reserved words, see [List of forbidden keywords](https://docs.byteplus.com/en/docs/NDB_for_MySQL/List_of_forbidden_keywords). |
   |Account type |Type of database account, support the creation of the following two types of accounts, account permissions detailed description please refer to [Account permission description](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Account_permission_description).<br><br><br>* **Super account**: An instance can only create one super account, and has all the permissions of all databases under the instance, and can manage all normal accounts and databases.<br><br>* **Normal account**: An instance can create multiple normal accounts, and it is necessary to manually grant the permissions of a specific database to the normal account. |
   |Description |Fill in the description information of the account, with a length of 0 to 256 characters. It can contain numbers, Chinese characters, English characters, underscores (_) and hyphens (\-). |
   |Password |The password of the account. The password rules are as follows:<br><br><br>* The length is 8~32 characters.<br><br>* It contains at least three of the following: uppercase letters, lowercase letters, digits, and special characters.<br><br>* Special characters are `~!@#$%^&*_-+=`\|\(){}[]:;'<>,.?/`. |
   |Confirm password |Enter the password again, it must be the same as the password entered in the previous step. |
   |Authorized database |* **Super account**: By default, it has all permissions for all databases under this instance, and no separate authorization is required.<br><br>* **Normal account**: You need to grant the specified permissions for the specified database for the normal account. When permissions are not set, this account does not have any permissions for any database. You can also modify the database authorized by the account after creation is complete. Currently supported permission types include: **Read/Write (DDL+DML)** , **Read\-only**, **DDL only**, **DML only**, **Custom permissions (multiple choices)** . For the specific SQL operation permissions included in each permission type, see the [Account permission list](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Account_permission_description).<br><br>   * **Setting permissions for a single database**<br><br>      1. Reselect the permission type from the drop\-down list in the **Permission** column of the target database.<br><br>         If you choose **Custom permissions**, you need to manually tick one or more SQL action permissions for them.<br><br>      2. When the selection is complete, click **OK** in the lower right corner of the drop\-down list.<br><br>   * **Bulk setting permissions**<br><br>      1. Check multiple target database names and click **Bulk settings permissions**.<br><br>      2. Select the permission type in the drop\-down list.<br><br>         If you choose **Custom permissions**, you need to manually tick one or more SQL action permissions for them.<br><br>      3. When the selection is complete, click **OK** in the lower right corner of the drop\-down list. |
   

6. After all database authorization settings are completed, click **OK** to complete the creation of the account.


<span id=".5Yig6Zmk6LSm5Y-3"></span>
## Delete account

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After the account is deleted, it cannot be restored, and the connection to use the account may be interrupted. Please exercise caution.</div>



1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Accounts**.

5. On the **Accounts** tab, click **Delete** under the **Actions** column of the target account.

6. Click **OK** in the pop\-up dialog box.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[CreateDBAccount](https://www.byteplus.com/en/docs/NDB_for_MySQL/CreateDBAccount) |Call the CreateDBAccount to create a database account. |
|[DeleteDBAccount](https://www.byteplus.com/en/docs/NDB_for_MySQL/DeleteDBAccount) |Call the DeleteDBAccount to delete the database account. |
|[DescribeDBAccounts](https://www.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBAccounts) |Call the DescribeDBAccounts to query the account information of the instance. |
