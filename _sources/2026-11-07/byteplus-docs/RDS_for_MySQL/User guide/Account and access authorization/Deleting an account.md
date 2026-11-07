---
title: "Deleting an account"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Deleting_an_account"
---

This topic describes how to delete a database account for a MySQL instance.

<span id="3aA6YTft"></span>
## Prerequisites

An instance has been created and the instance state is **Running**. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id="SA7ekaJI"></span>
## Precautions

A deleted account cannot be restored. Deleting an account may interrupt connections that use it, so proceed with caution.

<span id="Ya0PS4uz"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. Click the **Accounts** tab on top of the page.

6. On the **Accounts** tab, click **Delete** in the **Actions** column for the target account.

7. In the dialog box that appears, enter the name of the account to be deleted, and then click **OK**.


<span id="gGFfbvfW"></span>
## Related API


|API |Description |
|---|---|
|[DescribeDBAccounts](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbaccounts) |Call the DescribeDBAccounts API to view the account list. |
|[DeleteDBAccount](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedbaccount) |Call the DeleteDBAccount API to delete an account. |
