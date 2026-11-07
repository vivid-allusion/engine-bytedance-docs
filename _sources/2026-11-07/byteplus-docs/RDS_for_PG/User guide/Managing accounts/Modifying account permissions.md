---
title: "Modifying account permissions"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_account_permissions"
---

You can modify the permissions of a normal account as needed. This topic explains how to modify account privileges for a normal account and the procedure.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

[An account has been created](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_and_managing_an_account) for the instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* A super account can only be reset to the initial status.

* Modifying account priviledges may cause an impact on the business. Operate with caution and confirm whether the business is normal after the modification.

* The instance read\-only account only has read\-only permissions for all databases in the instance, and does not support modifying the permissions of the instance read\-only account.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click on the target instance name.

4. Click **Accounts** at the top of the page.

5. On the **Accounts** tab, click  **... \> Modify priviledges** in the **Actions** column of the target account.

6. Select the target database for authorization in the pop\-up dialog box, select the account permission, and click **OK**.
