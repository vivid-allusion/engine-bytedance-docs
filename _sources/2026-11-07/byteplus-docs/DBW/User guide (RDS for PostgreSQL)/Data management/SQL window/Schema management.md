---
title: "Schema management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/schema-management-for-PG"
---

This topic describes how to visually create, edit, and delete schema on the Database Workshop (DBW) console to manage the entire lifecycle of schema.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance, an account, and a database have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance), [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_and_managing_an_account) and [Creating a database](https://docs.byteplus.com/en/docs/DBW/database-management-for-PG).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The account you create must have the corresponding permissions for querying and modifying the corresponding database.</div>


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* A deleted schema cannot be recovered. In addition, deleting a schema requires the database to process a large number of files, which may block the processing of other transactions and degrade database performance. Exercise caution when performing this operation.

* The creation, deletion, and other operations you perform may affect the online business operation. It is recommended to perform them during off\-peak hours.


<span id=".5Yib5bu65qih5byP"></span>
## Create schema


1. Log on to the [data interaction platform (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/log-in-database-interaction-platform-for-PG).

2. On the top menu bar of the **Data interaction platform** page, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Schema**, right\-click the target schema, and select **Create schema**.

4. In the **Create schema** dialog box, configure the schema name. The rules for schema names are as follows:

   * The schema name is unique within the database.

   * The length must be between 2 and 63 characters.

   * The name must start with a letter and end with a letter or a digit.

   * It consists of letters, numbers, underscores (_), or hyphens (\-).

   * It can not start with pg_ and can not use reserved keywords.

5. Click **OK**.


<span id=".57yW6L6R5qih5byP"></span>
## Edit schema


1. Log on to the [data interaction platform (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/log-in-database-interaction-platform-for-PG).

2. On the top menu bar of the **Data interaction platform** page, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Schema**, right\-click the target schema, and select **Edit schema**.

4. In the **Edit mode** dialog box, modify the schema name. The rules for schema names are as follows:

   * The schema name is unique within the database.

   * The length must be between 2 and 63 characters.

   * The name must start with a letter and end with a letter or a digit.

   * It consists of letters, numbers, underscores (_), or hyphens (\-).

   * It can not start with pg_ and can not use reserved keywords.

5. Click **OK**.


<span id=".5Yig6Zmk5qih5byP"></span>
## Delete schema


1. Log on to the [data interaction platform (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/log-in-database-interaction-platform-for-PG).

2. On the top menu bar of the **Data interaction platform** page, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Schema**, right\-click the target schema, and select **Delete schema**.

4. In the **Delete schema** dialog box, confirm the SQL statement to be executed.

5. Click **Execute**.
