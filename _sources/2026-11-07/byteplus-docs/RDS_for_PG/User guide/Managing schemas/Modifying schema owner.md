---
title: "Modifying schema owner"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_schema_owner"
---

This topic describes how to modify the schema owner.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance is created and in the **Running** state. For more information about creating an instance, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

* A database has been created. For more information about creating an account, see [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_a_database).

* A schema has been created. For more information about how to create a schema, refer to [Creating a schema](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_a_schema).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Modifying the schema owner may cause the original schema owner to be unable to access resources in the schema. Please proceed with caution.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click on the target instance name.

4. Click on the **Schema** tab on top of the page.

5. On the **Schema** tab, click **Change owner** in the **Actions** column of the target schema.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Instance read\-only accounts, high\-privilege accounts with DDL privileges disabled, or normal accounts with DDL privileges disabled cannot be used as database owners.   </div>
   

6. In the pop\-up dialog, select an account as the **Schema Owner** to manage this schema.
