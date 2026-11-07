---
title: "Database management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/database-management-for-PG"
---

This topic describes how to visually create, edit, and delete databases on the Database Workshop (DBW) console to manage the entire lifecycle of databases.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have created an instance and account. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_and_managing_an_account).

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Deleting and editing system databases is not supported.

* It is not recommended to perform operations such as adding, deleting, or modifying tables, views, functions, and triggers in the system database.

* The creation, deletion, and other operations you perform may affect the online business operation. It is recommended to perform them during off\-peak hours.


<span id=".5Yib5bu65pWw5o2u5bqT"></span>
## Create a database


1. Log on to the [data interaction platform for RDS for PostgreSQL](https://docs.byteplus.com/en/docs/DBW/log-in-database-interaction-platform-for-PG).

2. On the top menu bar of the **Data interaction platform** page, click the drop\-down icon next to the database.

3. Click **Create database**.

4. In the **Create database** dialog box, configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Database name** |Custom database name. The naming convention is as follows:<br><br><br>* The length must be between 2 and 63 characters.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of letters, numbers, underscores (_), or hyphens (\-).<br><br>* Reserved keywords can not be used. |
   |**Character set** |Select a character set from the drop\-down list. You can select `utf8`, `ascii`, and `latin1`. |
   |**Sorting rules** |Select a sorting rule from the drop\-down list. Sorting rules vary depending on the character set, as follows:<br><br><br>* `utf8`: When `utf8` is selected as the character set, the supported collations include `C`, `C.UTF-8`, `en_US.UTF-8`, `zn_CN.UTF-8`, and `POSIX`.<br><br>* `ascii`: When `ascii` is selected as the character set, the supported collations include `C`, `C.UTF-8`, `en_US.UTF-8`, `zn_CN.UTF-8`, and `POSIX`.<br><br>* `latin1`: When `latin1` is selected as the character set, the supported collations include `C` and `POSIX`. |
   |**CType** |From the drop\-down list, select CType. The CType varies depending on the character set, as follows:<br><br><br>* `utf8`: When `utf8` is selected as the character set, the supported CType includes`C` , `C.UTF-8`, `en_US.UTF-8`, `zn_CN.UTF-8`, and `POSIX`.<br><br>* `ascii`: When `ascii` is selected as the character set, the supported CType includes `C`, `C.UTF-8`, `en_US.UTF-8`, `zn_CN.UTF-8`, and `POSIX`.<br><br>* `latin1`: When the `latin1` is selected as the character set, the supported CType includes `C` and `POSIX`. |
   |**Connection limit** |Set the connection limit. When set to  **\-1**, it means that the number of connections is not limited. |
   |**Remarks** |Set the remarks information of the created database as needed, which can be used for business differentiation. |
   

5. Click **OK**.


<span id=".57yW6L6R5pWw5o2u5bqT"></span>
## Edit a database

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The account you create must have the corresponding permissions for querying and modifying the corresponding database.</div>


* <div data-tips="true" data-tips-type="tip">Editing system databases is not supported.</div>


1. Log on to the [data interaction platform for RDS for PostgreSQL](https://docs.byteplus.com/en/docs/DBW/log-in-database-interaction-platform-for-PG).

2. On the top menu bar of the **Data interaction platform** page, click the drop\-down icon next to the database.

3. Click **Database management**.

4. On the **Database management** tab, click **Edit** in the **Actions** column of the target database.

5. In the **Edit database** dialog box, configure **Connection limit** and **Remarks**.

   When the connection limit is set to  **\-1**, it indicates that the number of connections is not limited.

6. Click **OK**.


<span id=".5Yig6Zmk5pWw5o2u5bqT"></span>
## Delete a database

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The account you create must have the corresponding permissions for querying and modifying the corresponding database.</div>


* <div data-tips="true" data-tips-type="tip">Deleting system databases is not supported.</div>


1. Log on to the [data interaction platform for RDS for PostgreSQL](https://docs.byteplus.com/en/docs/DBW/log-in-database-interaction-platform-for-PG).

2. On the top menu bar of the **Data interaction platform** page, click the drop\-down icon next to the database.

3. Click **Database management**.

4. On the **Database management** tab, click **Delete** in the **Actions** column of the target database.

5. In the **Confirm deletion** dialog box, enter the database name in the **Confirm deletion** input box.

6. Click **Delete**.
