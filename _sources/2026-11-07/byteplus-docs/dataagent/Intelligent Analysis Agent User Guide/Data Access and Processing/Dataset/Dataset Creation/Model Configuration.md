---
title: "Model Configuration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Model_Configuration"
---

<span id="_1-概述"></span>
# 1. Overview

The model configuration of a dataset enables the integration of data from different sources. The resulting data, including auxiliary data, can be presented visually, helping users comprehensively understand the data from multiple perspectives. After completing [Overview of Data Connection](https://docs.byteplus.com/docs/dataagent/Overview_of_Data_Connection), you can configure the model to create a dataset.

**Preliminary notes:** 

Extracted datasets support the following multi\-table Join and multi\-table Union operations as described; for direct connection datasets, except that Finder data connections only support single tables, other direct data sources support multi\-table Union, Join, and custom SQL. **Multi\-table operations cannot be used across data sources or data connections**. For example, table A from data connection A and table B from data connection B cannot be used for union or join operations, nor can custom SQL include operations involving both table A and table B at the same time.

> For the differences between extraction and direct connection, see: Data source access\-\-\>[Supported connection methods](https://docs.byteplus.com/docs/dataagent/Overview_of_Data_Connection#b2925a8e)


<span id="_2-快速入门"></span>
# 2. Quick start

The product supports integrating data from different sources. You can build a data model simply by dragging and dropping.

**Step 1**: The list on the left displays only tables you have permission to access. Drag the tables needed for dataset creation into the central "model area". The system supports cross\-source merging (Union) and cross\-source joining (Join).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e0462f8c2bf44bc817448295b264178~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: Click the capsule of each table to select the fields (columns) to use. Fields not selected will not be imported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5303f5b3fd714ef7bc3727e3ec2c71ee~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: Configure the matching relationships/association methods and associated fields for merging.


* Merging (Union): Click the blue area labeled 'Established merge relationship' and configure the matching relationships for merging below.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fa25e54685f43d7918ba390b01f2133~tplv-goo7wpa0wc-image.image) </span>


* Association (Join): Click the connection icon in the middle and set the association method and associated fields in the popup window.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed5c38f7912e427f8fcdc23e60323788~tplv-goo7wpa0wc-image.image) </span>

**Step 4**: During model construction, you can click the "Preview" button in the upper right corner to preview the data.

> Caution: The preview results are randomly sampled data and are for reference only.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ab4fb2cb9074d4ab9ee38c115bbcada~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-多表关联（join）"></span>
# 3. Multi\-table association (Join)

<span id="_3-1-使用限制"></span>
## 3.1 Usage restrictions


* Multi\-table association (Join) in extraction mode: supports data from the same data connection/data source, and also supports data from different data connections/data sources.

* Except for Finder data connections, which only support single tables, other direct connection data sources support multi\-table associations from the same data connection, but do not support **cross\-data source or cross\-data connection** usage.


<span id="_3-2-使用方法"></span>
## 3.2 Usage instructions

(1) Click the '+' at the top of the left\-side list to add additional data connections; you can select multiple data connections within a single canvas.

(2) Then, drag tables from **the same data connection/different data connections** into the central "model area". Afterward, you can select the required fields and configure associations.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0bd57fc7ee4a42a3b1061792e6b0aeb0~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-常见关联（join）类型"></span>
## 3.3 Common join types

<span id="_3-3-1-关联（join）"></span>
### 3.3.1 Join

JOIN is used to connect different data tables, commonly applied to data for analysis, which are stored in different tables according to different purposes. Therefore, when analyzing data, you need to connect the desired data based on the same fields in different tables. For example, an order connects the customer, dishes, kitchen department, suppliers, and more through the order number.

> Caution: The field types used for associations must remain consistent.


<span id="_3-3-2-inner-join-内部"></span>
### 3.3.2 Inner join

The logic is to take the "intersection" of the values that meet the condition in the join fields of Table1 and Table2, thereby extracting the corresponding data rows within the intersection range from both tables and concatenating the corresponding columns, as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d8eb2ea9ff747bf9f53d3eac45d670e~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-3-left-join-左连接"></span>
### 3.3.3 Left join

This means starting from the row data of the left table, searching for data rows in the right table that meet the join field conditions according to the join criteria, and then combining the specified fields from that row with the left table to form a complete data row, as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2be373f65364fe1b770543d3772ea50~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-4-right-join-右连接"></span>
### 3.3.4 **Right join**

Essentially, the logic is the same as left join, but in this case, the right table is used as the primary data row for Cartesian product calculation of the data columns; that is: A Right join B = B left join A

<span id="_3-3-5-full-join-完全外部连接"></span>
### 3.3.5 **Full join**

A full outer join returns all rows from both the left and right tables. If a row does not have a matching row in the other table, the selected columns from the other table will contain null values. If there are matching rows between tables, the entire result set row contains the data values from the base table.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f08f9396fb745deb31d52d9fe0e069f~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-多表合并（union）"></span>
# 4. Multi\-table union (Union)

<span id="_4-1-使用限制"></span>
## 4.1 Usage restrictions


* Multi\-table union in extraction mode (Union): Supports data from the same data connection/data source, and also supports data from different data connections/data sources.

* In direct connection mode, except for Finder data connections which only support single tables, other direct connection data sources support multi\-table union from the same data connection, but do not support **cross\-data source or cross\-data connection** usage.


<span id="_4-2-使用方法"></span>
## 4.2 Usage method

(1) Click the “+” at the top of the left list to add more types of data connections; multiple data connections can be selected within a single canvas.

(2) Then drag tables from **the same data connection/different data connections** into the central “model area”.

(3) Click the blue area labeled 'Merge relationship established', and configure the matching relationship below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/809d375d78d64571a1b4a79f5d216d83~tplv-goo7wpa0wc-image.image) </span>

<span id="_5-表替换与追加"></span>
# 5. Table replacement and append

<span id="_5-1-替换表"></span>
## 5.1 Replace table

Tables already dragged onto the canvas in the dataset support replacement, for example, replacing an existing MySQL data table with an Excel data table.

> Extraction mode supports cross\-data source table/data connection replacement, but direct connection mode only supports tables from the same data connection.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12125e89595c42cb95dbe6edd5d8e14b~tplv-goo7wpa0wc-image.image) </span>

After clicking the above “Replace table” button, select the target replacement table on the left, then drag the target table to the right to perform the table replacement.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3565174cc47041f18c6a4adf155d4bdb~tplv-goo7wpa0wc-image.image) </span>

When replacing tables, note that there may be differences in fields before and after replacement. You need to confirm deleted and newly added fields; newly added fields can be selected for application, while deleted fields are only available for preview.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cac309a9f1b6429c8b510dcd2eff715e~tplv-goo7wpa0wc-image.image" width="610px" /></div>


Because fields from the original table may be used subsequently, referencing deleted fields may result in errors, such as creating new expressions based on original fields or creating charts/dashboards based on those fields, which will result in errors. Therefore, it is recommended to proceed with caution when the warning pop\-up appears.

<span id="_5-2-追加文件"></span>
## 5.2 Append files

Only offline files (Excel, CSV, Access) support file append. Users can manually add new data to the dataset by appending files.

The file append feature does not affect the synchronization of data within the file prior to the append operation. For example, when the user performs the following operations:

> April 12: The user creates a dataset using file A (containing 100 rows of data) and completes the initial synchronization. April 13: The user uses the file append feature to upload file B (containing 10 rows of data), saves it, and resynchronizes the data.


The data in each partition of the system is as follows:

> P_date=0412: 100 rows of data (from file A) P_date=0413: 110 rows of data (from file A + file B)


The user can update the appended data to the system by resynchronizing historical data.

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



* After saving the dataset, data links created by extraction require manual synchronization to synchronize the newly added data to the base table, while direct connection tables do not require manual synchronization.

> The user can also perform file append operations in the data connection following the above steps. See [Append files](https://docs.byteplus.com/docs/dataagent/Local_Excel_CSV_files#295b54d5).


<span id="_5-3-替换文件"></span>
## 5.3 Replace file

Only offline files (Excel, Csv, Access) support file replacement.

After file replacement, the data in the replaced file will stop synchronizing. For example, when the user performs the following operations:

> April 12: The user creates a dataset using file A (containing 100 rows of data) and completes the initial synchronization. April 13: The user uses the file replacement feature to upload file B (containing 10 rows of data), saves it, and resynchronizes the data.


The data in each partition of the system is as follows:

> P_date=0412: 100 rows of data (from file A) P_date=0413: 10 rows of data (from file B)


The user can update the replaced data to the system by resynchronizing historical data.

> After resynchronizing the data for 0412, P_date=0412 should contain 10 rows of data (from file B).


**Operation steps**


* Right\-click and select [Replace file]

* Click or drag to upload the replacement file


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3904faec626438abe6010bc385c1341~tplv-goo7wpa0wc-image.image" width="667px" /></div>



* After previewing the replacement file data, set the mapping relationship between the replacement file and the original table fields, then click Complete.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/75a64c96b5b04b76af70ea1d9c2be7e8~tplv-goo7wpa0wc-image.image" width="683px" /></div>


> Users can also perform file append operations in the data connection by following the steps above. See: [Local Excel/CSV Files](https://docs.byteplus.com/docs/dataagent/Local_Excel_CSV_files)


<span id="_6-数据抽取设置"></span>
# 6. Data extraction settings

<span id="_6-1-使用方法"></span>
## 6.1 Usage

For the extraction table, click the table in the model to display its extraction settings below. In the extraction settings, select the extraction mode as full or incremental, choose to filter part of the data, and add extraction parameters as needed.

> Caution: If there are multiple tables in the model, settings can be configured for each individual table in the model.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d01641d4b3841beace9d9733e3ff527~tplv-goo7wpa0wc-image.image) </span>

<span id="_6-2-抽取设置"></span>
## 6.2 Extraction settings

<span id="_6-2-1-全量抽取"></span>
### 6.2.1 Full extraction

If the table has a small amount of data or the original data is updated frequently, full extraction can be used to synchronize the table data.

Each time data is synchronized, all data from the table will be synchronized to the product's storage and compute engine.

<span id="_6-2-2-增量抽取"></span>
### 6.2.2 Incremental extraction

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e31d2f6f4c7415d9af50268173e81cf~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* Incremental detection: Currently, only timestamp\-based incremental detection is supported.

* Incremental field: Select the field used for incremental detection. Currently, only time fields are supported for this purpose.

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

Click "Add condition" under extraction parameters to add more parameters. For detailed settings, see [Extraction Parameters](https://docs.byteplus.com/docs/dataagent/Extraction_Parameters).

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a1e79cabbcd9482d9ce0f8096f1f64a4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_7-模型切换（抽取改为直连）"></span>
# 7. Model switching (from extraction to direct connection)

After saving the dataset, switching between data extraction and direct connection is not supported.

<span id="_8-自定义-sql-模型"></span>
# 8. Custom SQL model

During data modeling, some complex logic can be implemented by creating datasets using a custom SQL model. DataAgent supports modeling and analysis through custom SQL, extends the depth of scenarios supported by agile BI, and meets the needs of complex data analysis scenarios. For more details, see [Custom SQL](https://docs.byteplus.com/docs/dataagent/Custom_SQL).
