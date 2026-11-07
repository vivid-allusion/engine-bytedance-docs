---
title: "Model Configuration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Model_Configuration_"
---

<span id="_1-概述"></span>
# 1. Overview

The model configuration of a dataset enables the integration of data from different sources, allowing all data, including auxiliary data, to be presented visually and helping users comprehensively understand the data from multiple perspectives. After completing [Data Connection Overview](https://docs.byteplus.com/docs/dataagent/Data_Connection_Overview), you can configure the model to create a dataset.

**Prerequisite instructions:** 

Extracted datasets support the multi\-table Join and Union operations described below. For direct connection datasets, except for Finder data connections which only support single tables, other direct connection data sources support multi\-table Union, Join, and custom SQL. **Multi\-table operations cannot be used across data sources or data connections**; for example, Table A from data connection A and Table B from data connection B cannot be used for union or join, nor can operations involving both Table A and Table B be performed in custom SQL.

> See Data source access\-\-\>[Supported connection methods](https://docs.byteplus.com/docs/dataagent/Data_Connection_Overview#a7cf7826) for differences between extraction and direct connection.


<span id="_2-快速入门"></span>
# 2. Quick start

The product supports integrating data from different sources. Simply drag and drop to build a data model.

**Step 1**: The left list only displays tables you have permission to access. Drag the tables needed for the dataset into the central "model area". The system supports cross\-source merging (Union) and cross\-source joining (Join).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e0462f8c2bf44bc817448295b264178~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: Click the capsule for each table to select the fields (columns) to use. Fields not selected will not be imported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5303f5b3fd714ef7bc3727e3ec2c71ee~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: Configure the matching relationships, association methods, and associated fields.


* Merging (Union): Click the blue area labeled "Established merge relationships" and configure the matching relationships below.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fa25e54685f43d7918ba390b01f2133~tplv-goo7wpa0wc-image.image) </span>


* Association (Join): Click the connection icon in the middle and set the association method and associated fields in the popup window.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed5c38f7912e427f8fcdc23e60323788~tplv-goo7wpa0wc-image.image) </span>

**Step 4**: During model construction, you can click the "Preview" button in the upper right corner to preview the data.

> Note: The preview result is random sample data and is for reference only.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ab4fb2cb9074d4ab9ee38c115bbcada~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-多表关联（join）"></span>
# 3. Multi\-table association (Join)

<span id="_3-1-使用限制"></span>
## 3.1 Usage restrictions


* Multi\-table association (Join) in extraction mode: Supports data from the same data connection/data source, and also supports data from different data connections/data sources.

* Except for Finder data connections, which only support single tables, other direct connection data sources support multi\-table associations from the same data connection. **Cross\-data source and cross\-data connection** usage is not supported.


<span id="_3-2-使用方法"></span>
## 3.2 Usage

(1) Click the “+” at the top of the left\-hand list to add more types of data connections. Multiple data connections can be selected within a single canvas.

(2) Then, drag tables from **the same data connection or different data connections** into the central “model area”. You can then select the required fields and configure association relationships.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0bd57fc7ee4a42a3b1061792e6b0aeb0~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-常见关联（join）类型"></span>
## 3.3 Common join types

<span id="_3-3-1-关联（join）"></span>
### 3.3.1 Join

JOIN is used to connect different data tables. Data for analysis is often stored in different tables for different purposes. When analyzing data, you need to connect the desired data based on the same fields in different tables. For example, an order connects the customer, dishes, kitchen, and supplier together through the order number.

> Caution: The field types used for joining must be consistent.


<span id="_3-3-2-inner-join-内部"></span>
### 3.3.2 Inner join

The logic is to take the “intersection” of the values that meet the join conditions in the connection fields of Table1 and Table2, extract the corresponding data rows within the intersection range from both tables, and concatenate the corresponding columns, as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d8eb2ea9ff747bf9f53d3eac45d670e~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-3-left-join-左连接"></span>
### 3.3.3 Left join

This means starting from the row data of the left table, searching for rows in the right table that meet the join field conditions according to the join criteria, and then combining the specified fields from that row with the left table to form a complete data row, as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2be373f65364fe1b770543d3772ea50~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-4-right-join-右连接"></span>
### 3.3.4 **Right join**

The logic is essentially the same as left join, but in this case, the right table is used as the primary data row for Cartesian product calculation of data columns. That is: A Right join B = B left join A.

<span id="_3-3-5-full-join-完全外部连接"></span>
### 3.3.5 **Full join**

A full outer join returns all rows from both the left and right tables. If a row does not have a matching row in the other table, the selected columns from the other table will contain null values. If there are matching rows between the tables, the entire result set row contains the data values from the base table.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f08f9396fb745deb31d52d9fe0e069f~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-多表合并（union）"></span>
# 4. Union of multiple tables

<span id="_4-1-使用限制"></span>
## 4.1 Usage restrictions


* Union of multiple tables in extraction mode: supports data from the same data connection/data source, and also supports data from different data connections/data sources.

* In direct connection mode, except that Finder data connections only support single tables, other direct connection data sources support union of multiple tables from the same data connection, but do not support **cross\-data source or cross\-data connection** usage.


<span id="_4-2-使用方法"></span>
## 4.2 How to use

(1) Click the '+' at the top of the list on the left to add more types of data connections; multiple data connections can be selected on a single canvas.

(2) Then drag tables from **the same data connection/different data connections** into the 'Model Area' in the center.

(3) Click the blue area labeled 'Union established', and configure the mapping below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/809d375d78d64571a1b4a79f5d216d83~tplv-goo7wpa0wc-image.image) </span>

<span id="_5-表替换与追加"></span>
# 5. Table replacement and appending

<span id="_5-1-替换表"></span>
## 5.1 Replace table

Tables that have already been dragged onto the canvas in the dataset support replacement, for example, replacing an existing Mysql data table with an Excel data table.

> Extraction mode supports cross\-data source/table/data connection replacement, but direct connection mode only supports tables from the same data connection.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12125e89595c42cb95dbe6edd5d8e14b~tplv-goo7wpa0wc-image.image) </span>

After clicking the above 'Replace table' button, select the target replacement table on the left, then drag the target table to the right to complete the table replacement.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3565174cc47041f18c6a4adf155d4bdb~tplv-goo7wpa0wc-image.image) </span>

When replacing a table, note that there may be differences in fields before and after replacement, so you need to confirm the fields to be deleted and added; new fields can be selected and applied, while deleted fields are only available for preview.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cac309a9f1b6429c8b510dcd2eff715e~tplv-goo7wpa0wc-image.image" width="610px" /></div>


Since fields from the original table may be used later, deleting fields that are in use may cause errors, such as creating new expressions based on the original fields or creating charts/dashboards based on those fields, which will result in errors. Therefore, it is recommended to proceed with caution when the warning pop\-up appears.

<span id="_5-2-追加文件"></span>
## 5.2 Appending files

Only offline files (Excel, Csv, Access) support file appending. Users can manually add new data to the dataset by appending files.

The file append functionality does not affect the synchronization of data within the file prior to appending. For example, when the user performs the following operations:

> April 12: The user creates a dataset using file A (containing 100 rows of data) and completes the initial synchronization. April 13: The user uses the file append functionality to upload file B (containing 10 rows of data), saves, and then synchronizes the data again.


The data in each partition within the system is as follows:

> P_date=0412: 100 rows of data (from file A) P_date=0413: 110 rows of data (from file A + file B)


The user can update the appended data in the system by resynchronizing historical data.

> After resynchronizing the data for 0412, P_date=0412 should contain 110 rows of data (from file A + file B).


**Operation steps**


* Right\-click and select "Append file"


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a1795108f3c4eb2b4afd681e3f4dc51~tplv-goo7wpa0wc-image.image" width="581px" /></div>



* Click or drag to upload the appended file


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3904faec626438abe6010bc385c1341~tplv-goo7wpa0wc-image.image" width="667px" /></div>



* After previewing the appended file data, set the mapping relationship between the appended file and the original table fields, then click Finish.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/75a64c96b5b04b76af70ea1d9c2be7e8~tplv-goo7wpa0wc-image.image" width="683px" /></div>



* After saving the dataset, data links created using the extraction method require manual synchronization to synchronize the newly added data to the base table, while direct connection tables do not require manual synchronization.

> The user can also perform file append operations in the data connection following the steps above. Refer to: [Local Excel/CSV File](https://docs.byteplus.com/docs/dataagent/Local_Excel_CSV_File).


<span id="_5-3-替换文件"></span>
## 5.3 Replace file

Only offline files (Excel, Csv, Access) support file replacement.

After file replacement, the data in the replaced file will stop synchronizing. For example, when the user performs the following operations:

> April 12: The user creates a dataset using file A (containing 100 rows of data) and completes the initial synchronization. April 13: The user uses the file replacement functionality to upload file B (containing 10 rows of data), saves, and then synchronizes the data again.


The data in each partition within the system is as follows:

> P_date=0412: 100 rows of data (from file A) P_date=0413: 10 rows of data (from file B)


The user can update the replaced data in the system by resynchronizing historical data.

> After resynchronizing the data for 0412, P_date=0412 should contain 10 rows of data (from file B).


**Operation steps**


* Right\-click and select [Replace file]

* Click or drag to upload the replacement file


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3904faec626438abe6010bc385c1341~tplv-goo7wpa0wc-image.image" width="667px" /></div>



* After previewing the replacement file data, set the matching relationship between the replacement file and the original table fields, then click Complete.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/75a64c96b5b04b76af70ea1d9c2be7e8~tplv-goo7wpa0wc-image.image" width="683px" /></div>


> Users can also append files in the data connection by following the steps above. See: [Append file](https://docs.byteplus.com/docs/dataagent/Local_Excel_CSV_File#91d2195a).


<span id="_6-数据抽取设置"></span>
# 6. Data extraction settings

<span id="_6-1-使用方法"></span>
## 6.1 Usage

For the extraction table, click the table in the model to display its extraction settings below. In the extraction settings, select the extraction method as full or incremental, choose to filter specific data, and add extraction parameters as needed.

> Caution: If there are multiple tables in the model, settings can be configured for each individual table in the model.


<span id="_6-2-抽取设置"></span>
## 6.2 Extraction settings

<span id="_6-2-1-全量抽取"></span>
### 6.2.1 Full extraction

If the table has a small amount of data or the original data is frequently updated, you can use the full extraction method to synchronize the table data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d01641d4b3841beace9d9733e3ff527~tplv-goo7wpa0wc-image.image) </span>

Each time data is synchronized, all data from the table will be fully synchronized to the product's storage and computing engine.

<span id="_6-2-2-增量抽取"></span>
### 6.2.2 Incremental extraction

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e31d2f6f4c7415d9af50268173e81cf~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* Incremental judgment: Currently, only timestamp\-based incremental judgment is supported.

* Incremental field: Select the field used for incremental judgment. Currently, only time fields are supported for this purpose.

* Time format: If the incremental field is in date format, it will be displayed as yyyy\-MM\-dd HH:mm:ss or yyyy\-MM\-dd. For other formats, select the appropriate number of digits for the timestamp.


<span id="_6-3-其他功能"></span>
## 6.3 Other functions

<span id="_6-3-1-数据筛选"></span>
### 6.3.1 Data filtering

Filter the data in the table to exclude unnecessary data. Fields used for filtering do not need to be extracted.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae0a8fe8ea534b809c1d2c5c58637e46~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_6-3-2-抽取参数"></span>
### 6.3.2 Extraction parameters

Click "Add condition" under extraction parameters to add additional parameters. For detailed settings, see [Extraction Parameters](https://docs.byteplus.com/docs/dataagent/Extraction_Parameters__).

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a1e79cabbcd9482d9ce0f8096f1f64a4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_7-模型切换（抽取改为直连）"></span>
# 7. Model switching (change extraction to direct connection)

After saving the dataset, switching between data extraction and direct connection is not supported.

<span id="_8-自定义-sql-模型"></span>
# 8. Custom SQL model

During data modeling, some complex logic can be implemented by creating datasets using a custom SQL model. DataAgent supports custom SQL modeling and analysis, extending the depth of scenarios supported by agile BI and meeting the requirements of complex data analysis scenarios. For more details, see [Custom SQL](https://docs.byteplus.com/docs/dataagent/Custom_SQL_).
