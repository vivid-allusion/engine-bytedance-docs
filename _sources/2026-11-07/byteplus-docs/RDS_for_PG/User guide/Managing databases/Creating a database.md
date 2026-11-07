---
title: "Creating a database"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/creating_a_database"
---

To use RDS for PostgreSQL, you need to create databases in your instance. This topic describes how to create a database for PostgreSQL instance.

<span id="FmbKK3Xz"></span>
## Precautions

A maximum of 2000 databases can be created under one instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance), and the instance is in the **Running** status.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


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
