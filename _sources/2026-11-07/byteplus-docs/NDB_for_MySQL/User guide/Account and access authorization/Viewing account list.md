---
title: "Viewing account list"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_account_list"
---

The account list displays the account names, account types, and supported operations of all accounts in the target instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Accounts created through SQL that do not comply with naming conventions can be modified and deleted in the console, but cannot be searched through the console's search bar.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Accounts**.

5. Under the **Accounts** page, you can view all account information for your instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can search for the target account by <strong>Account name</strong>, and fuzzy match is supported. Only support searching for accounts that conform to the naming convention through the console.   </div>
   

<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent Operations


* [Creating and deleting accounts](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts)

* [Modifying normal account permissions](https://www.byteplus.com/en/docs/NDB_for_MySQL/Modifying_normal_account_permissions)

* [Resetting super account permissions](https://www.byteplus.com/en/docs/NDB_for_MySQL/Resetting_super_account_permissions)

* [Changing account password](https://www.byteplus.com/en/docs/NDB_for_MySQL/Changing_account_password)


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeDBAccounts](https://www.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBAccounts) |Call the DescribeDBAccounts to query the account information of the instance. |
