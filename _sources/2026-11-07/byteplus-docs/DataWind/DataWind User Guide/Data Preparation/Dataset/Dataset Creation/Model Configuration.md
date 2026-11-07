---
title: "Model Configuration"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Model_Configuration"
---

<span id="_1-概述"></span>
# 1. Overview

Model configuration for datasets enables the integration of data from different sources. The integrated data can ultimately be presented in a visual format, helping users comprehensively understand the data from multiple perspectives. After completing [Data Connections Overview](https://docs.byteplus.com/docs/DataWind/Data_Connections_Overview), you can configure the model to create a dataset.

**Prerequisite notes:** 

Extracted datasets support multi\-table Join and multi\-table Union operations as described below. Direct connection datasets are subject to the following version\-specific restrictions:


* Before version V2.50.0, **only single\-table direct connection queries are supported**

* From version V2.50.0 and later, except that Finder data connections only support single tables, other direct connection data sources support multi\-table Union, Join, and custom SQL. **Multi\-table operations cannot be performed across data sources or data connections**, for example, Table A from data connection A and Table B from data connection B cannot be joined or unioned, nor can operations involving both Table A and Table B be performed in custom SQL.

> For the differences between extraction and direct connection, see: Data source integration\-\-\>[Connection methods](https://docs.byteplus.com/docs/DataWind/Data_Connections_Overview#0b15f366)


<span id="_2-快速入门"></span>
# 2. Quick start

The product supports integrating data from different sources. You can build a data model simply by dragging and dropping.

**Step 1**: The list on the left displays only tables you have permission to access. Drag the tables needed for dataset creation into the central "model area". The system supports cross\-source merging (Union) and cross\-source joining (Join).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c646902640954372bfa2fe61bd9413e7~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: Click the capsule for each table to select the fields (columns) to use. Fields not selected will not be imported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc0895989a984953bd10a8510d802145~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: Configure the matching relationships/association methods and associated fields for merging.


* Merging (Union): Click the blue area labeled 'Established merge relationship' and configure the matching relationship for merging below.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc5c906132584e60bb1f1e7138069fb5~tplv-goo7wpa0wc-image.image) </span>


* Association (Join): Click the connection icon in the center and set the association method and associated fields in the popup window.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63868ec3f03540fc84107bac21df3ef8~tplv-goo7wpa0wc-image.image) </span>

**Step 4**: During model construction, you can click the "Preview" button in the upper right corner to preview the data.

> Note: The preview results are randomly sampled data and are for reference only.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29a15605bf354d0199610dc33db1c4dd~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-多表关联（join）"></span>
# 3. Multi\-table association (Join)

<span id="_3-1-使用限制"></span>
## 3.1 Usage restrictions


* Multi\-table join in extraction mode: Supports data from the same data connection/data source, and also supports data from different data connections/data sources.

* Direct connection mode has the following restrictions depending on the version:

   * Before version V2.50.0, **only single\-table direct queries are supported; multi\-table join is not supported**

   * From version V2.50.0 and later, Finder data connections only support single tables. Other direct data sources support multi\-table joins from the same data connection, but do not support **cross\-data source or cross\-data connection** usage.


<span id="_3-2-使用方法"></span>
## 3.2 Usage method

(1) Click the “+” at the top of the left\-side list to add more types of data connections; you can select multiple data connections in a single canvas.

(2) Then drag tables from **the same data connection/different data connections** into the central “model area”, after which you can select the required fields and configure the join relationships.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e1e6db74a78f4f8f923134f10a0016a8~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-常见关联（join）类型"></span>
## 3.3 Common join types

<span id="_3-3-1-关联（join）"></span>
### 3.3.1 Join

JOIN is used to connect different data tables, commonly used for analytical data that is stored in different tables for different purposes. When analyzing data, you need to connect the desired data based on the same fields in different tables. For example, an order connects the customer, dishes, kitchen, and supplier together through the order number.

> Caution: The field types used for joins must be consistent.


<span id="_3-3-2-inner-join-内部"></span>
### 3.3.2 Inner join

The logic is to take the “intersection” of values in the join fields of Table1 and Table2 that meet the same condition, extract the corresponding rows from both tables within this intersection, and concatenate the relevant columns, as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f4e21d048daf44d7a04eb9bf0f6b006f~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-3-left-join-左连接"></span>
### 3.3.3 Left join

This means starting from the row data of the left table, searching for rows in the right table that meet the join field conditions according to the join criteria, and then combining the specified fields from that row with the left table to form a complete row of data, as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/430b4bb10f3d486baf0454e56214556b~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-4-right-join-右连接"></span>
### 3.3.4 **Right join**

Essentially, the logic is the same as that of a left join, but in this case, the right table is used as the main data row for the Cartesian product calculation of data columns; that is, A Right join B = B left join A.

<span id="_3-3-5-full-join-完全外部连接"></span>
### 3.3.5 **Full join**

A full join returns all rows from both the left and right tables. When a row does not have a matching row in the other table, the columns from the other table in the select list will contain null values. If there are matching rows between the tables, the entire result set row contains the data values from the base tables.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb31423a159b4359b88dbab21500842c~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-多表合并（union）"></span>
# 4. Multi\-table union (Union)

<span id="_4-1-使用限制"></span>
## 4.1 Usage restrictions


* In extract mode, multi\-table union (Union) supports data from the same data connection/data source, and also supports data from different data connections/data sources.

* In direct connection mode, the following restrictions apply depending on the version:

   * Before version V2.50.0\*\*, only single\-table direct connection queries are supported; multi\-table union (Union) is not supported\*\*

   * From version V2.50.0 and later, except that Finder data connections only support single tables, other direct connection data sources support multi\-table union from the same data connection, but do not support **cross\-data\-source or cross\-data\-connection** usage


<span id="_4-2-使用方法"></span>
## 4.2 Usage method

(1) Click the “+” at the top of the list on the left to add more types of data connections; multiple data connections can be selected on one canvas.

(2) Then drag tables from **the same data connection/different data connections** into the middle "Model area".

(3) Click the blue area labeled "Merge relationship established" and configure the matching relationship below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/154138bd91a848bcbb54af9e06ea7191~tplv-goo7wpa0wc-image.image) </span>

<span id="_5-表替换与追加"></span>
# 5. Table replacement and append

<span id="_5-1-替换表"></span>
## 5.1 Replace table

Tables that have already been dragged onto the canvas in the dataset support replacement, for example, replacing an existing MySQL data table with an Excel data table.

> Extract mode supports cross\-data\-source table/data connection replacement, but direct connection mode only supports tables from the same data connection.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/944ef5c1443f468fbd6fe9458b8278ad~tplv-goo7wpa0wc-image.image) </span>

After clicking the above “Replace Table” button, select the target replacement table on the left, then drag the target table to the right to perform the table replacement.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/497638af1d9f4ccc9f689e6655fdd21e~tplv-goo7wpa0wc-image.image) </span>

When replacing a table, note that since there may be differences in fields before and after replacement, you need to confirm which fields are deleted and which are added; new fields can be selected and applied, while deleted fields are only available for preview.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd7ed0cd564b4bf49d11994f69bdd8a0~tplv-goo7wpa0wc-image.image" width="610px" /></div>


Because the original table fields may be used later, if deleted fields are used, this will result in errors. For example, creating new expressions based on the original fields or creating charts/dashboards based on those fields will both cause errors. Therefore, when the following warning pop\-up appears, please confirm with caution before proceeding to the next step.

<span id="_5-2-追加文件"></span>
## 5.2 Append files

Only offline files (Excel, CSV, Access) support appending files. Users can manually add new data to the dataset by appending files.

The file append function does not affect the synchronization of data within files before appending. For example, if the user performs the following steps:

> April 12: The user creates a dataset using file A (containing 100 rows of data) and completes the first synchronization. April 13: The user uploads file B (containing 10 rows of data) using the file append function, saves, and resynchronizes the data.


The data in each partition in the system is as follows:

> P_date=0412: 100 rows of data (from file A) P_date=0413: 110 rows of data (from file A + file B)


The user can update the system with the appended data by resynchronizing historical data.

> After resynchronizing the data for 0412, P_date=0412 should contain 110 rows of data (from file A + file B).


**Operation steps**


* Right\-click and select "Append files"


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ead47581440d426c880b31f4d621f6f0~tplv-goo7wpa0wc-image.image) </span>


* Click or drag to upload the appended file


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94e5b5a6eb754722a8d49f9e75ab2282~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* After previewing the appended file data, map the fields between the appended file and the original table, then click Finish.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7d922bb64c04dc88714225b71f4598b~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* After saving the dataset, data links created by extraction require manual synchronization to sync the new data to the base table, while direct connection tables do not require manual synchronization.

> Users can also append files in the data connection by following the steps above. See [Append file](https://docs.byteplus.com/docs/DataWind/Local_Excel_CSV_Files#dced972f).


<span id="_5-3-替换文件"></span>
## 5.3 Replace files

Only offline files (Excel, CSV, Access) support file replacement.

After replacing a file, the data in the replaced file will stop synchronizing. For example, if the user performs the following steps:

> April 12: The user created a dataset using file A (containing 100 rows of data) and completed the initial synchronization. April 13: The user used the file replacement feature to upload file B (containing 10 rows of data), saved it, and then resynchronized the data.


The data in each partition in the system is as follows:

> P_date=0412: 100 rows of data (from file A) P_date=0413: 10 rows of data (from file B)


The user can update the replaced data in the system by resynchronizing historical data.

> After resynchronizing the data for 0412, P_date=0412 should contain 10 rows of data (from file B).


**Steps**


* Right\-click and select [Replace File]

* Click or drag to upload the replacement file


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21628721f2334700af762863a61cbef1~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* After previewing the replacement file data, set the mapping between the replacement file and the original table fields, then click Finish.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ab2946f508d479aaabfa80b698813cd~tplv-goo7wpa0wc-image.image" width="610px" /></div>


> The user can also append files in the data connection by following the steps above. Refer to [Replace file](https://docs.byteplus.com/docs/DataWind/Local_Excel_CSV_Files#af8342da).


<span id="_6-数据抽取设置"></span>
# 6. Data extraction settings

<span id="_6-1-使用方法"></span>
## 6.1 Usage

For the extraction table, click the table in the model to display its extraction settings below. In the extraction settings, select the extraction mode as full or incremental, select to filter part of the data, and add extraction parameters if needed.

> Caution: If there are multiple tables in the model, you can configure each individual table in the model.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/666226c03a9449e5b23d0115f8d981b2~tplv-goo7wpa0wc-image.image) </span>

<span id="_6-2-抽取设置"></span>
## 6.2 Extraction settings

<span id="_6-2-1-全量抽取"></span>
### 6.2.1 Full extraction

If the table data volume is small or the original data is updated frequently, you can use full extraction to synchronize the table data.

Each time data is synchronized, all data in the table will be synchronized to the product's storage and computing engine.

<span id="_6-2-2-增量抽取"></span>
### 6.2.2 Incremental extraction

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7580a5348feb424f8b48a5e1e429bf6c~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* Incremental determination: Currently, only timestamp\-based incremental determination is supported.

* Incremental field: Select the field for incremental determination. Currently, only time fields are supported for this purpose.

* Time format: If the incremental field is in date format, it is displayed as yyyy\-MM\-dd HH:mm:ss or yyyy\-MM\-dd; for other formats, select the number of digits for the timestamp.


<span id="_6-3-其他功能"></span>
## 6.3 Other features

<span id="_6-3-1-数据筛选"></span>
### 6.3.1 Data filtering

By filtering the data in this table, unnecessary data can be excluded. These filter fields do not need to be extracted.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dbf095ee9e3c4dafb814ffd82c07a031~tplv-goo7wpa0wc-image.image) </span>

<span id="_6-3-2-抽取参数"></span>
### 6.3.2 Extraction parameters

Click "Add condition" under extraction parameters to add more parameters for configuration. For detailed settings, see [Extraction Parameters](https://docs.byteplus.com/docs/DataWind/Extraction_Parameters).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c405bf22f11e4d35bb71d8434c60b59c~tplv-goo7wpa0wc-image.image) </span>

<span id="_7-模型切换（抽取改为直连）"></span>
# 7. Model switching (switching from extraction to direct connection)

After saving the dataset, switching between data extraction and direct connection is not supported.

<span id="_8-自定义-sql-模型"></span>
# 8. Custom SQL models

During data modeling, some complex logic can be implemented by creating datasets using custom SQL models. DataWind supports custom SQL modeling and analysis, extending the depth of scenarios supported by agile BI to meet the requirements of complex data analysis scenarios. For details, see [Custom SQL](https://docs.byteplus.com/docs/DataWind/Custom_SQL).
