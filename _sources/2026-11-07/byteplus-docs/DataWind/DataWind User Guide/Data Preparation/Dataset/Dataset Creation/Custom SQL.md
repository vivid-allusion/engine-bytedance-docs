---
title: "Custom SQL"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Custom_SQL"
---

<span id="_1-概述"></span>
# 1. Overview

After completing [Data Connections Overview](https://docs.byteplus.com/docs/DataWind/Data_Connections_Overview), you can create datasets. You can create datasets directly from original tables, generate datasets through multi\-table join or union, or use custom SQL for more complex logic. The following describes how to create datasets using data tables or custom SQL.

<span id="_2-快速入门"></span>
# 2. Quick start

(1) Click Data Preparation \-\> Datasets, click the plus sign on the left, and select "Create dataset".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a4e20ea57f54527b81ef6a8153e8910~tplv-goo7wpa0wc-image.image) </span>

(2) Select the target data source from existing data connections. If there is no data connection, you can create one in Data Connections.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/092759190fc64925929b63714b360573~tplv-goo7wpa0wc-image.image" width="610px" /></div>


(3) Choose between table creation and SQL creation.


* On the model configuration page, select Custom SQL or a table from the database on the left, then drag it to the canvas on the right.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ab353a4ec5a4d4bb86a8e181311a13d~tplv-goo7wpa0wc-image.image) </span>


* After dragging Custom SQL to the canvas, you can enter SQL statements in the SQL editor area below.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34ed74af0462485b9e9db521fe37fb5b~tplv-goo7wpa0wc-image.image) </span>


* You can also click a table on the left, then click "Insert query statement" in the pop\-up box to quickly generate an SQL query statement for that table.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01ef6962f41d42a0bbbeb3c3eeb4a9d9~tplv-goo7wpa0wc-image.image) </span>

* Click the "Save" button above the SQL editor box shown below to save the SQL statement. Select the Extract mode or Direct mode, then click Save in the upper right corner.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/373bbf41c050422396199083f459c7a8~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Features

<span id="_3-1-表创建与-sql-创建区别"></span>
## 3.1 Differences between table creation and SQL creation


| |[Model Configuration](https://docs.byteplus.com/docs/DataWind/Model_Configuration) |[Data Connections Overview](https://docs.byteplus.com/docs/DataWind/Data_Connections_Overview)**Type support limitations** |**Database syntax limitations** |
|---|---|---|---|
|Table creation |Single table, JOIN/UNION |All data sources support table creation. |No restrictions |
|SQL creation |Single table |Only supported for database sources. For a detailed support list, see [Data Connections Overview](https://docs.byteplus.com/docs/DataWind/Data_Connections_Overview) |Depending on the database type, there are limitations on SQL syntax. For example, if the data connection is MySQL, Oracle syntax is not supported. |


<span id="_3-2-快捷创建-sql-语句"></span>
## 3.2 Quickly create SQL statements

SQL statements can be entered manually in the SQL input box, or you can select a database and data table on the left. Hover the mouse over the data table to choose to insert the table name, insert field names, or insert a query statement, enabling quick creation of SQL statements.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d67dba66ec1b43ad981961804fc1f732~tplv-goo7wpa0wc-image.image) </span>


* Click Insert Table Name, and the table name will appear in the Custom SQL box.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e36891d059a742f0ac099274c9f2daae~tplv-goo7wpa0wc-image.image) </span>


* Click Insert Fields, and the field names will appear in the Custom SQL box.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3eeddef886d542eab26fb6faf7e34955~tplv-goo7wpa0wc-image.image) </span>


* Click Insert Query Statement, and the query statement for the table will appear in the Custom SQL box (format: select Field A, Field B from DB.T_table).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ca6e2b15f7344fd8406f4d55fb15256~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-自定义-sql-面板"></span>
## 3.3 Custom SQL panel

Provides formatting, parsing, saving, preview display, data preview, field names, and extract settings functions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/305ea35b64b54523abb1b6ecd8be9cbc~tplv-goo7wpa0wc-image.image) </span>


* Formatting: Click to format the current statement and enhance the readability of the SQL statement.

* Parse: Validate the SQL syntax and display the reason for any syntax errors.

* Save: Save the current statement. After modifying the SQL statement, it is recommended to click Save. You must click Save before saving the dataset.

* Show preview: Preview the result of this SQL statement.

* Data preview: Display the execution result of the SQL statement on the left in the right panel. You can adjust the number of preview rows in "Show rows".

* Field names: Click to directly view the field names and data types of the SQL result.

* Extraction settings: Click to configure extraction parameters. For parameter explanations, please refer to [Extraction Parameters](https://docs.byteplus.com/docs/DataWind/Extraction_Parameters).

> Data source limitations: Currently, ADB2.0, ADB3.0, DB2, Phoenix, Vertica, Teradata, PostgreSQL, and Greenplum do not support parameter configuration. Other data sources that allow creating custom SQL support this setting.


* Rename and fullscreen: In the top bar of the custom SQL, click to rename the SQL dataset, or click the fullscreen button to display the SQL dataset in fullscreen mode.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd3c49f97858431eb8a640778c95333e~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-同步多天"></span>
## 3.4 Synchronize multiple days

To synchronize data for multiple days at a time, such as specifying to synchronize data from 1, 3, and 7 days ago into this dataset, you need to use custom SQL to create the dataset.

**Operation method**

(1) Create a custom SQL dataset as described above.

(2) Click the synchronization settings at the top to enter the synchronization settings page, then click Advanced settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a4f6cb3c0334a1e95b584f526121e49~tplv-goo7wpa0wc-image.image) </span>

(3) In Advanced settings, there is a switch for synchronizing multiple days. Enable multi\-day synchronization, and a prompt for multi\-day parameter settings will appear below.

(4) After enabling multi\-day synchronization, return to the model configuration page, write the SQL according to the writing specifications, and then complete the configuration and save as you would when creating a dataset normally.

**Feature description**

In the custom SQL panel, click Variable description in the lower left corner to view the default variable prompts. This means you can introduce date variables in the custom SQL to implement dynamic date queries.


* ${DATE} Business date, format: yyyy\-MM\-dd, for example: 2015\-05\-1

* ${date} Business date, format: yyyyMMdd, for example: 20150526

* ${DATE+n} or ${DATE\-n}: Use DATE as the anchor point to move forward (+) or backward (\-) n days.

* ${date+n} or ${date\-n}: Use date as the anchor point to move forward (+) or backward (\-) n days.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5df04cbea30149b8b2ee26b13f230679~tplv-goo7wpa0wc-image.image) </span>

**SQL writing specifications**


* In the SQL statement, you must specify a date field, name it p_date as the partition field, and put it at the end.

* Explicitly specify synchronization requirements in the WHERE clause.


**Example 1:** 

Synchronize data for day 1 and for all days prior to day 7.

```sql
select
user_id,country,city,gender,
date as p_date #Specify partition fields
from table A
where date in ('${date}','${date-6}') #Specify the synchronization of data from Day 1 and Day 7
```


**Example 2:** 

Synchronize data from the most recent 7 days.

```plaintext
select
user_id,country,city,gender,
date as p_date #Specify partition fields
from table A
where date >= ${date-6} #Specify the synchronization of data from the past seven days
```


**Caution**

If the dataset has already been created, enabling multi\-day synchronization and then clicking synchronize may result in a prolonged dependency wait.


* When enabling multi\-day synchronization midway, ensure that the dataset already contains partitions covering more than the multi\-day synchronization range.

   * For example: If multi\-day synchronization is set to synchronize the previous 30 days, but the current dataset only contains partitions for the past 7 days, enabling multi\-day synchronization at this time will result in a prolonged dependency wait.

   * Solution: First disable multi\-day synchronization, backfill data for at least the past 30 days of partitions, and then enable multi\-day synchronization again.

   * Caution: If the dataset is created directly by **table extraction**, after disabling multi\-day synchronization, remember to return to the model configuration to modify the partition settings. When multi\-day synchronization is enabled, the partition settings will be automatically modified. After disabling multi\-day synchronization, the partition field will retain the multi\-day synchronization settings. If not modified manually, this will cause one partition in the dataset to synchronize data from N partitions in the upstream table.
