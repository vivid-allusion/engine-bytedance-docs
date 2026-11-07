---
title: "Viewing account details"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/viewing_account_information"
---

Document Database for MongoDB provides account management function. After creating an account successfully, you can view and manage the database accounts on the console. This topic describes how to view account details on the MongoDB console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* The instance status must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

* A database account has been created. For specific procedures, refer to [Creating account](https://docs.byteplus.com/en/docs/mongodb/create-account).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **Accounts** tab.

6. Under the **Accounts** tab, you can perform the following operations:

   
   |Classification of actions |Description |
   |---|---|
   |Filtering accounts |You can quickly filter out accounts that meet the conditions in the upper right corner of the account list through the following fields:<br><br><br>* Target database: Filter according to the name of the target database to which the account belongs. Fuzzy filtering is supported, and only one keyword can be entered for filtering each time.<br><br>* Account: Filter according to the account name. Fuzzy filtering is supported, and only one keyword can be entered for filtering each time. |
   |Viewing accounts |You can view the detailed information of accounts in the account list, including account name, account type, the target database to which the account belongs, the database permissions granted to the account, the creation time of the account, as well as the latest update time and account description, etc.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Document Database for MongoDB provides three types of accounts: super administrator account, high\-privileged account, and normal account. For more details about different types of accounts, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/account-overview#.6LSm5Y-357G75Z6L">Account type</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Different database types allow different account permissions to be granted. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/account-overview#.5pWw5o2u5bqT5LiO6LSm5Y-35p2D6ZmQ">Database and account permissions</a>.</div><br> |
   |Managing accounts |You can perform the following management operations on the specified account in the account list:<br><br><br>* Modifying account description<br><br>   1. Find the target account in the account list, and click the icon ** ** <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png) </span> in the **Description** column.<br><br>   2. Enter the new account description in the popped\-up dialog box and click **OK**.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The description should meet the following conditions simultaneously:      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The length is 0 to 256 characters.      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">It can contain numbers, Chinese characters, English letters, underscores (_), and hyphens (\-).      </div><br>      <br><br>* [Reset root account](https://docs.byteplus.com/en/docs/mongodb/reset-root-account)<br><br>* [Modifying password](https://docs.byteplus.com/en/docs/mongodb/reset-password)<br><br>* [Modifying account privileges](https://docs.byteplus.com/en/docs/mongodb/modifying_account_privileges)<br><br>* [Delete account](https://docs.byteplus.com/en/docs/mongodb/delete_account) |
   


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[DescribeDBAccounts](https://docs.byteplus.com/en/docs/mongodb/describedbaccounts) |Call the DescribeDBAccounts API to query list of accounts for target MongoDB instance. |
|[UpdateDBAccountPrivilege](https://docs.byteplus.com/en/docs/mongodb/updatedbaccountprivilege) |Call the UpdateDBAccountPrivilege API to modify the privileges or account description of a specified account in the target MongoDB instance. |
|[ResetDBAccount](https://docs.byteplus.com/en/docs/mongodb/resetdbaccount) |Call the ResetDBAccount API to modify password of specified account or reset the permissions of the root account to its initial state for target MongoDB instance. |
|[DeleteDBAccount](https://docs.byteplus.com/en/docs/mongodb/deletedbaccount) |Call the DeleteDBAccount API to delete the specified account in the target MongoDB instance. |
