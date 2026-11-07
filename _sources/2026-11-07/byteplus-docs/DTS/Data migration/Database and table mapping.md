---
title: "Database and table mapping"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Database_and_table_mapping"
---

Database and table mapping refers to the process of establishing corresponding relationships between database names and table names in the source and target databases during data migration or data synchronization scenarios, to facilitate operations such as data migration and synchronization. In scenarios with a large number of database tables, establishing mapping relationships for individual table or database names one by one is inefficient. Therefore, DTS supports a batch mapping feature.

<span id="z8k1DpsO"></span>
## Prerequisites

A data synchronization or data migration task has been created and is currently in the stage of **Configure migration object** or **Configure synchronization object**. For methods to enter the stage of **Configure migration object** or **Configure synchronization object**, refer to [Migration solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_migration_solutions) or [Synchronization solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_synchronization_solutions).

<span id="UYgK0Tla"></span>
## Precautions


* Regular expression search for target objects is supported in the migration object or selected object areas.

* In data synchronization, Cache for Redis and RDS for PostgreSQL databases do not support database and table mapping.

* In data migration, Cache for Redis, RDS for PostgreSQL, and RDS for SQL Server databases do not support database and table mapping.

* After starting the migration or synchronization task, modifying the database and table mapping is not supported.


<span id="EeDFEcYp"></span>
## Single database and table mapping


1. Go to the **Configure migration object** or **Configure synchronization objects** wizard page.

2. In the **Migration object** area, locate the **Selected object**, click the pen icon next to the target database, table, or view to rename the database, table, or view.

   If you select entire databases in the **Migration object** area, you can only modify the database name in the **Selected object** area, and can not expand the database.

3. In the **Modify name** pop\-up, change the names of the target databases, tables, and views.

4. Click **OK**.


<span id="IffQDPLo"></span>
## Batch database and table mapping


1. Go to the **Configure migration object** or **Configure synchronization object** wizard page.

2. In the **Migration object** area, locate the **Selected object**, and click **Batch mapping**.

3. In the **Batch mapping** dialog box, batch modify the names of the target databases or tables according to the mapping rules.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When there are many databases and tables in batch mapping, regular expressions can be used to search target objects.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When selecting a database name, data under the database name, such as table names and trigger names, will not be selected simultaneously.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Batch modification of view names is not supported.   </div>
   

   
   |Batch mapping rules |**Description** |
   |---|---|
   |**Add prefix or suffix to the name** |Add a prefix or suffix to the original database and table names, such as adding a prefix new or a suffix backup. The effect is shown below. |
   |**Unified renaming** |Modify the original database and table names uniformly to new names. For example, to unify three subtables auth_operation, test123table, and test_table1 into one table, the auth_operation table can use the unified renaming rule to establish mapping rules. The effect is shown below. |
   |**Uniformly reduce the name** |Certain keywords can be uniformly removed from the original database and table names, as shown below. When using the **Uniformly reduce the name** rule, if a database or table name does not match the mapping rules, such as lacking content to reduce, the name remains unchanged. |
   

4. Click **Apply**.
