---
title: "Cloning a database"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Clone"
---

RDS for PostgreSQL supports cloning existing databases to quickly create new databases with the same structure as existing databases. This article describes the steps for cloning a database.

<span id="jwqgZkYM"></span>
## Precautions


* Only one clone database task can exist under an instance.

* A maximum of 2000 databases can be created under one instance. When the number of database instances has reached 2000, the database cannot be cloned.

* Only databases with no more than 1000 cloned tables are supported.

* During the process of cloning a database, you cannot perform DDL operations on the database.


<span id="KdfkjaRj"></span>
## Prerequisites


* Already created an instance, and the instance is **Running**. For more information about creating an instance, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance).

* The database has been created under the target instance. For more information about creating an account, see [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_a_database).


<span id="2UR6CuqY"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. At the top of the page, click **Databases**.

6. In the **Databases** list, click  **...**  \> **Clone this database** in the target database **Actions** column.

7. In the pop\-up **Clone this database** window, after completing the following configuration and checking the restriction information, click **OK**.

   
   |Configuration item |Is it required? |Description |
   |---|---|---|
   |Source database name |\- |Confirm the target database to be cloned. |
   |New database name |Yes |Set the name of the new database. The Database name must follow these rules:<br><br><br>* The name is unique within the instance.<br><br>* 2 to 63 characters in length.<br><br>* Must start with a letter and end with a letter or a digit.<br><br>* Can contain letters, digits, underscores (_) and hyphens (\-).<br><br>* Some reserved words or keywords cannot be used in the database name, see [Reserved keywords](https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_forbidden_keywords) for all reserved keywords.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The new database is named by default with the source database name + _clone_ + timestamp.</div><br> |
   |Data options |Yes |Currently only the structure of a cloned database is supported. |
   |PL/pgSQL options |No |You can check whether to clone the following contents of the source database on demand:<br><br><br>* Views<br><br>* Stored procedures<br><br>* Functions<br><br>* Triggers |
   |Risk warning |Yes |Check the prompt after confirming the known limitations of the clone database.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When the instance size is low, the reading and writing pressure is high, and the number of tables in the target database is large, the process of cloning the database will last for a long time. During the process of cloning a database, you cannot perform DDL operations on the database.</div><br> |
   


<span id="4QtsVn9Y"></span>
## Related APIs


|API |Note |
|---|---|
|[CloneDatabase](https://docs.byteplus.com/en/docs/RDS_for_PG/CloneDatabase) |Calling the CloneDatabase interface clones the database. |
