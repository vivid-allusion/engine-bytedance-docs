---
title: "Modifying the database owner"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_the_database_owner"
---

This topic describes how to modify the database owner.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have [created an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance), and the instance is in the **Running** status.

* [A database has been created](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_a_database).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click on the target instance name.

4. At the top of the page, click **Databases**.

5. Go to the **Databases** tab and choose **Actions** \> **Change owner** of the target database.

6. Select an account in the pop\-up dialog box as the ** Database owner** for accessing this database.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Instance read\-only accounts, high\-privilege accounts with DDL privileges disabled, or normal accounts with DDL privileges disabled cannot be used as database owners.   </div>
   

7. Click **OK**.
