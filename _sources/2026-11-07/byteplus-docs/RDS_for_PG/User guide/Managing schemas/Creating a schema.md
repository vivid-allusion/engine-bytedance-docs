---
title: "Creating a schema"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/creating_a_schema"
---

This topic introduces how to create a schema.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance), and the instance is in the **Running** status.

* [A database has been created](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_a_database).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click on the target instance name.

4. On the **Summary** page, click **Databases**.

5. On the **Databases** tab, click **Manage Schema** in the **Actions** column of the target database.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also click the <strong>Schema tab</strong> to enter the Schema management page.   </div>
   

6. In the dropdown list to the right of **Create Schema** at the top left of the page, select the database to which the Schema belongs.

7. Click **Create Schema**, and set the following parameters in the pop\-up dialog box.

   
   |Parameters |Note |
   |---|---|
   |Database name |Not required to set, it is the database selected in step 6. |
   |Schema |Enter the schema name. Requirements are as follows:<br><br><br>* The name is unique.<br><br>* Can contain letters, digits, underscores (_) and hyphens (\-).<br><br>* Must start with a letter and end with a letter or a digit.<br><br>* 2 to 63 characters in length.<br><br>* Some reserved words or keywords cannot be used in the schema name, see [List of reserved keywords](https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_forbidden_keywords) for all reserved keywords.<br><br>* Do not start the name with `pg_`. |
   |Schema Owner |Select an account to manage the schema in the drop\-down list, the account has the owner permission of the schema. The schema owner can be modified after creation. For more details, refer to [Modifying schema owner](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_schema_owner).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Instance read\-only accounts, super accounts with DDL privileges disabled, or normal accounts with DDL privileges disabled cannot be used as schema owners.</div><br> |
   

8. Click **OK** to complete the Schema creation.
