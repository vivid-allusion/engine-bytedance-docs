---
title: "Data management"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/managing_data"
---

RDS for PostgreSQL has been connected to Database Workshop (DBW), providing visual data management functions in DBW.

<span id=".5Yqf6IO95LuL57uN"></span>
## Function introduction

The data management function relies on DBW's data interaction platform to implement a visual operation interface. In the data interaction platform, you can perform the following operations:


* Execute SQL commands. For more details, refer to [Command operations](https://docs.byteplus.com/en/docs/DBW/command-operation-for-PG).

* Manage the database lifecycle, including creating database, modifying database, and Delete database. For more details, refer to [Databases](https://docs.byteplus.com/en/docs/DBW/database-management-for-PG).

* Manage the table lifecycle, including viewing tables, creating tables, Add data, modifying data, and deleting tables. For more details, refer to [Schema management](https://docs.byteplus.com/en/docs/DBW/schema-management-for-PG).

* Manage the full lifecycle of a schema, including creating, editing, and deleting schemas. For more information, refer to [Table management](https://docs.byteplus.com/en/docs/DBW/table-management-for-PG).


<span id=".55m75b2V5bel5L2c5Y-w"></span>
## Login DBW

The RDS for PostgreSQL workbench has two entrances: the instance list of RDS for PostgreSQL and the Database Workshop.


* **Log in to the RDS for PostgreSQL Workbench from the instance list of RDS for PostgreSQL**

   1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

   2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.      </div>
      

   3. On the **Instances** page, click **Login DBW** in the actions column of the target instance. In the pop\-up **Database DBW** dialog box, set the following parameters and check **Authorize the Database Workshop to add service IPs to the corresponding database instance allowlist**, and then click **Login**.

      
      |**Parameters** |**Note** |
      |---|---|
      |**Instance types** |Confirm that the instance type is RDS for PostgreSQL. |
      |**Instance name/ID** |Confirm that the instance is the target instance. Other instances can be switched from the drop\-down list. |
      |**Database account** |Enter the database account name. |
      |**Database password** |Enter the database account password. |
      

* **Log in to the RDS for PostgreSQL Workbench from Database Workbench**


For details, see [Log in database interaction platform](https://docs.byteplus.com/en/docs/DBW/log-in-database-interaction-platform-for-PG).
