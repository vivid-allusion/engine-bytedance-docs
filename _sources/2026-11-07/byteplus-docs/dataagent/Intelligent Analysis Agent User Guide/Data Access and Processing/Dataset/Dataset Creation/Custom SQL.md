---
title: "Custom SQL"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Custom_SQL"
---

<span id="_1-概述"></span>
# 1. Overview

After completing [Overview of Data Connection](https://docs.byteplus.com/docs/dataagent/Overview_of_Data_Connection), users can create datasets. It supports creating datasets directly from original tables, generating datasets through multi\-table join or union operations, and using custom SQL for datasets with complex logic. The following describes how to create datasets using data tables or custom SQL.

<span id="_2-快速入门"></span>
# 2. Quick start

(1) Click Data Preparation \-\> Dataset, click the plus sign on the left, and select "Create dataset".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4ca5b6394d444cf81e8df127727c52f~tplv-goo7wpa0wc-image.image) </span>

(2) Select the target data source from existing data connections. If there is no data connection, you can create one in the data connections section.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ddf9bc848a449ae9266b1a55a306175~tplv-goo7wpa0wc-image.image" width="610px" /></div>


(3) Choose table creation and SQL creation.


* On the model configuration page, select Custom SQL or a table from the database on the left, then drag it to the canvas on the right.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/906c2411aff64dd08c2f092499b24322~tplv-goo7wpa0wc-image.image) </span>


* After dragging Custom SQL to the canvas, you can enter SQL statements in the SQL editor area below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf5ba5bdd0ee4b519850309d2065daf5~tplv-goo7wpa0wc-image.image) </span>

* You can also click a table on the left, then click "Insert query statement" in the pop\-up box to quickly generate a SQL query statement for that table.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42c4f0c5e0d84c308d49633bc8c0cfe8~tplv-goo7wpa0wc-image.image) </span>


* Click the "Save" button above the SQL editor box shown below to save the SQL statement. Select the extraction or direct connection mode, then click Save in the upper right corner.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ae7612af5894a23b66cdb4e88a775cf~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-表创建与-sql-创建区别"></span>
## 3.1 Differences between table creation and SQL creation


| |[Model Configuration](https://docs.byteplus.com/docs/dataagent/Model_Configurations) |**Data source type support restrictions** |**Database syntax restrictions** |
|---|---|---|---|
|Table creation |Single table, JOIN/UNION |All data sources support table creation. |No restrictions. |
|SQL creation |Single table |Only database source types are supported. For a detailed support list, see [Overview of Data Connection](https://docs.byteplus.com/docs/dataagent/Overview_of_Data_Connection) |SQL syntax is restricted based on the database type. For example, if the database connection is MySQL, Oracle syntax is not supported. |


<span id="_3-2-快捷创建-sql-语句"></span>
## 3.2 Quickly create SQL statements

SQL statements can be created by manually entering them in the SQL input box. Alternatively, select a database and data table on the left, hover the mouse over the data table, and choose to insert the table name, insert fields, or insert query statement to quickly create SQL statements.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6698424962bd4e0fb8656ba1e4f18be8~tplv-goo7wpa0wc-image.image) </span>


* Click Insert Table Name to display the table name in the Custom SQL box.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/115f0f21627e4c55bf7f17c64afbe7ad~tplv-goo7wpa0wc-image.image) </span>


* Click Insert Fields to display the field names in the Custom SQL box.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b29777d299f4bf697156a0a82611549~tplv-goo7wpa0wc-image.image) </span>


* Click Insert Query Statement to display the query statement for the table in the Custom SQL box (format: select Field A, Field B from DB.T_table).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/260cd5b94a6942ff9c075554de9b8cbb~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-自定义-sql-面板"></span>
## 3.3 Custom SQL panel

Provides formatting, parsing, saving, preview display, data preview, field names, and extraction settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8e3f7a0cfe04b82ab3ab6b6566f8fd9~tplv-goo7wpa0wc-image.image) </span>


* Formatting: Click to format the current statement and enhance the readability of the SQL statement.

* Parse: Validate the SQL syntax and display the reason for any syntax issues.

* Save: Save the current statement. After modifying the SQL statement, it is recommended to click Save. You must click Save before saving the data set.

* Show preview: Preview the result of this SQL statement.

* Data preview: Display the execution result of the SQL statement on the left in the right panel. You can adjust the number of preview rows in "Rows to display".

* Field names: Click to directly view the field names and data types of the SQL result.

* Extraction settings: Click to configure extraction parameters. For parameter explanations, please refer to [Extraction Parameters](https://docs.byteplus.com/docs/dataagent/Extraction_Parameters).

> Data source limitations: Currently, ADB2.0, ADB3.0, DB2, Phoenix, Vertica, Teradata, PostgreSQL, and Greenplum do not support parameter configuration. All other data sources that support custom SQL support this setting.


* Rename and full screen: In the top bar of the custom SQL, click to modify the name of the SQL data set, or click the full screen button to view the SQL data set in full screen.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e476a7981574af5965528d5c31571c7~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-同步多天"></span>
## 3.4 Synchronize multiple days

To synchronize data for multiple days each time, such as specifying to synchronize data from 1, 3, or 7 days ago into this data set, you need to use custom SQL to create the data set.

**Operation method**

(1) Create a custom SQL data set as described above.

(2) Click the synchronization settings at the top to enter the synchronization settings page, then click Advanced settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4323fb5e94fa4f9a8c0d3bc0f021192b~tplv-goo7wpa0wc-image.image) </span>

(3) In Advanced settings, there is a switch for synchronizing multiple days. Select to enable synchronizing multiple days. There is also a prompt below for synchronizing multiple days parameter settings.

(4) After enabling synchronizing multiple days, return to the model configuration page, write the SQL according to the writing specifications, and then complete the configuration and save as you would when creating a data set normally.

**Feature description**

In the custom SQL panel, click Variable description in the lower left corner to see the default variable prompts. This means that date variables can be introduced in the custom SQL to implement dynamic date queries.


* ${DATE} Business date, format: yyyy\-MM\-dd, for example: 2015\-05\-01

* ${date} Business date, format: yyyyMMdd, for example: 20150526

* ${DATE+n} or ${DATE\-n}: Use DATE as the anchor point to move forward (+) or backward (\-) n days

* ${date+n} or ${date\-n}: Use date as the anchor point to move forward (+) or backward (\-) n days


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83a4446815f34b2181f0f9528aa0e726~tplv-goo7wpa0wc-image.image) </span>

**SQL writing specifications**


* In the SQL statement, you must specify a date field and name it as the p_date partition field (place it last).

* Explicitly specify synchronization requirements in the WHERE clause.


**Example 1:** 

Synchronize data from day 1 and data before day 7.

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

If the dataset has already been created, enabling multi\-day synchronization and then clicking synchronize may result in waiting for dependencies indefinitely.


* When enabling multi\-day synchronization after initial dataset creation, ensure the dataset already contains partitions beyond the multi\-day synchronization range.

   * For example: If multi\-day synchronization is set to synchronize the previous 30 days, but the current dataset has only synchronized partitions for the past 7 days, enabling multi\-day synchronization will result in waiting for dependencies indefinitely.

   * Solution: First disable multi\-day synchronization, backtrack and synchronize data for at least the past 30 days of partitions, and then enable multi\-day synchronization again.

   * Caution: If the dataset is created directly by **table creation extraction**, after disabling multi\-day synchronization, remember to return to the model configuration to modify the partition settings. When multi\-day synchronization is enabled, the partition settings will be automatically updated. After disabling multi\-day synchronization, the partition field will retain the multi\-day synchronization settings. If you do not manually modify it, the dataset's single partition will synchronize data from N partitions of the upstream table.
