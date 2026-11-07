---
title: "Common Dataset FAQs"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Common_Dataset_FAQs"
---

<span id="_1-数据集"></span>
# 1. Datasets

<span id="_1-1-常见报错信息"></span>
## 1.1 Common error messages

<span id="修改了-hive-表字段类型修改，同步不成功是什么问题？"></span>
### What could cause synchronization to fail after modifying the field type of a hive table?

**Example 1**: The hive data is not empty in the original database, but after synchronizing to DataWind, both the dataset preview and visual queries return null values.

The database contains values:

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_6625422915ca922fbc9dc7e3c6022c84) </span>

After synchronizing the dataset, the preview value is null:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e59e30a078af4f8d84ceb85ce4608aa3~tplv-goo7wpa0wc-image.image) </span>

**Example 2**: The hive data was initially synchronized to DataWind as int type. It was found that the data type did not meet expectations (all displayed values are 0, but 0.23 was expected). After changing the data type in hive to double, the DataWind data preview still does not show the expected 0.23.

**Root cause analysis**: A hive table consists of a storage file and a metadata file. When modifying the field type, only the metadata file was changed, but the storage file type was not updated, resulting in abnormal type conversion during data synchronization.

**Solution**:


* After modifying the field type of the hive table, reload the data into the hive table.

* Then, edit and save the corresponding dataset in DataWind, and resynchronize the data.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Editing and saving a dataset is used to update the field types in the dataset model. This operation will cause data in columns with changed types to be lost. After resynchronizing the data, the data will be restored to normal.</div>


<span id="kafka-接入数据集报错-olap-接口异常"></span>
### Kafka dataset integration reports OLAP interface exception

**Possible cause:**  Field format is not allowed

**Troubleshooting suggestions:** 

Currently, nested JSON is not supported, and modifying map field columns is not supported.

If the issue is not as described above, please refer to the following documentation for troubleshooting Kafka integration issues: [Kafka](https://docs.byteplus.com/docs/DataWind/Kafka).

<span id="飞书表格数据源显示上游数据源-token-不存在"></span>
### **Lark spreadsheet data source displays upstream data source Token does not exist**

**Possible cause:**  This issue occurs the first time a user uses the Lark data source, due to the absence of the Lark spreadsheet permission token.

**Solution:** 

The frontend page will display a QR code. The user can scan the code to register the token.

<span id="_1-2-数据口径常见问题"></span>
## 1.2 Common issues with data definitions

<span id="数据准确性和口径问题"></span>
### Data accuracy and definition issues

**Similar issues:** 

> The numbers for XXX are incorrect

> Data for the same dimension is inconsistent across different tables

> Links in charts or dashboard tables cannot be opened

> How to submit a data request

> Incorrect metrics


**Solution:** 

To understand the department's data situation, or if you have data requests, it is recommended to contact the department's analyst or data development for confirmation.

For issues regarding data table accuracy or data definitions, it is recommended to contact the corresponding data set owner for confirmation.

For issues with content display in charts or link redirection, it is recommended to contact the corresponding data set owner or the relevant business for confirmation.

<span id="_1-3-数据接入常见问题"></span>
## 1.3 Common issues with data integration

<span id="上传数据集提示格式错误"></span>
### Error message indicating incorrect format when uploading a data set

Please check whether the uploaded data set contains line breaks. Line breaks will be recognized as multiple data entries, which may result in a format error.

<span id="飞书表格上传失败-数据不符合预期"></span>
### Lark spreadsheet upload failed or data does not match expectations

**1. Permission\-related** (Common errors: Invalid connection information: invalid link; no permission)

(1) The person scanning the code must have read permission for the provided link.

(2) Providing a single link will import all sheets under that document.

**2. File requirements**

(3) Only standard spreadsheets are supported for recognition.

(4) The document must be named and cannot be "Untitled Spreadsheet". The document and sheet names must not contain an English period '.', otherwise the document schema may fail to be retrieved.

**3. Document format requirements**

(5) Only the first group of consecutive non\-empty column headers will be read; the first column header cannot be empty, otherwise an error will occur.

(6) Column headers should preferably be plain text, must not be all numbers, images, or hyperlinks, must not be named p_date, and must not contain $, `(backtick), or !, otherwise synchronization may fail. After creating the data set, do not modify the column headers in the Lark spreadsheet at will, otherwise synchronization may fail. Column headers that are too long may cause synchronization to fail.

(7) Column headers must not be duplicated, otherwise an error will occur.

(8) Rows should preferably not be empty. Completely empty rows will be counted in the total number of rows in the sheet and will be added to the data in a format such as [null, null, null, null].

(9) Merged cells and formulas are not supported.

(10) Try to avoid having different data types in the same column, otherwise synchronization may fail.

**Common error causes:** 

Invalid connection information: invalid link; no permission; untitled spreadsheet; expired token

Schema error: first column header is empty; invalid column header format

<span id="飞书表格上传显示应用非法"></span>
### Uploading a Lark sheet displays an illegal application error

Creating datasets from Lark sheets is supported.

To enable Lark datasets, you must first complete the basic configuration for Lark integration.

<span id="_1-4-数据集创建常见问题"></span>
## 1.4 Common issues in dataset creation

<span id="p-date-是什么"></span>
### What is p_date

p_date is the partition date field of the dataset. The product will rename both the date and p_date partition fields from the original Hive table to p_date.

p_date represents the data generation date in the upstream Hive table, or the date when data is synchronized to the dataset (if the upstream data does not have a date partition). In visual queries, you can use it to select and filter by the date dimension according to analysis requirements.

<span id="离线数据想要进行分析怎么办"></span>
### How to analyze offline data

Select "Dataset", then "Add Dataset", and choose the corresponding data source. To analyze offline data, you can upload files (Excel and CSV are supported) as a data source. For details, see [Local Excel/CSV Files](https://docs.byteplus.com/docs/DataWind/Local_Excel_CSV_Files).

<span id="申请具有行限制的数据表权限后，无法创建对应数据集"></span>
### Unable to create the corresponding dataset after applying for data table permissions with row restrictions

After applying for the corresponding row\-level permissions, you must add row restrictions in the filter conditions when creating the dataset. For example, if you only applied for data permissions where app_name='news', you must restrict the filter condition to app_name='news' when creating the dataset.

<span id="如何添加飞书表格"></span>
### How to add a Lark sheet

**Similar issues:** 

> Online form submission


**Operation steps:** 

Create a sheet in Lark; go to the dataset interface; click "New Dataset" in the left sidebar; select "Lark sheet"; and enter the document link to upload. See [Lark Sheets](https://docs.byteplus.com/docs/DataWind/Lark_Sheets).

<span id="为什么搜索不到数据表"></span>
### Why is the data table not found in search

The product only displays tables that the currently logged\-in user has permission to view. If you cannot find it, check whether the current data connection or login account has read permissions for the corresponding table.

<span id="_1-5-数据同步常见问题"></span>
## 1.5 Common issues in data synchronization

<span id="数据集一直显示等待执行"></span>
### The dataset keeps showing "waiting to execute"

Similar issues:

> Synchronization is not triggered after upstream data processing is completed

> Dataset synchronization is stuck

> Dataset synchronization is blocked

> The configured dataset synchronization task has not started yet


There are numerous projects within the product, and each project contains datasets with corresponding synchronization tasks. All synchronization tasks are randomly queued together to use queue resources.

**Data synchronization process:** 

At the scheduled time—all scheduled tasks within the product begin to queue and wait to submit YARN tasks—the YARN queue begins processing—calculation and scheduling are officially executed—synchronization succeeds

If concurrent tasks exceed the limit during the same period, data will remain in the waiting\-to\-execute state.

**Ways to accelerate:** 


* Adjust the dataset priority. Priority affects the scheduling order; the higher the priority, the easier it is to obtain resources.

* Set a non\-peak scheduled time. For example, 8:00–10:00 daily is peak time, so you can avoid scheduling during this period.


<span id="数据集同步慢"></span>
### Dataset synchronization is slow

**Possible causes:** 


* Incorrect dataset configuration

* Unreasonable parameter configuration


**Troubleshooting steps:** 


* Confirm whether the model configuration is correct, including connection method, join conditions, and so on [Model Configuration](https://docs.byteplus.com/docs/DataWind/Model_Configuration).

* Synchronization parameter configuration can be optimized to improve synchronization efficiency [Extraction Parameters](https://docs.byteplus.com/docs/DataWind/Extraction_Parameters).


<span id="飞书表格同步失败"></span>
### Lark spreadsheet synchronization failed

**Similar issues:** 

> Why does synchronization fail after modifying the Lark spreadsheet?

> Why is the modified Lark spreadsheet dataset unable to synchronize?


**Possible causes:** 

Deleting or renaming existing fields results in the inability to retrieve existing field information during synchronization.

**Recommended solution:** 

On the model configuration page, check whether the currently selected fields are consistent with the column names in the Lark spreadsheet.

If there are inconsistencies, click Edit to enter the dataset model configuration page and select the new fields.

Then match them on the field configuration page.

<span id="数据集显示等待执行，一直不同步"></span>
### The dataset shows 'waiting to execute' and never synchronizes

When the number of synchronization tasks within the product exceeds the concurrency limit, some tasks will be in the queue and will display 'waiting to execute' in the synchronization status. Please wait patiently. To increase task priority, adjust the scheduled synchronization time or change the priority.

<span id="数据超限怎么办？如何修改生命周期"></span>
### What should I do if the data exceeds the limit? How to modify the lifecycle

Path: Data Management \- Details \- Synchronization Settings \- Settings \- Edit

Lifecycle restriction: For a single partition, if the data volume is less than 30T, the lifecycle can be set to 1–1500 days.

<span id="数据集历史数据消失"></span>
### Historical data in the dataset has disappeared

Please check the lifecycle set for the dataset. After expiration, partition data will be deleted; however, synchronization records will still be retained.

<span id="数据集如何添加url链接描述"></span>
### How to add a URL link description to a dataset

Select the dataset, click ⋮, and select "Create Example" to add a link description.

<span id="查询前一天的数据，第二天什么时候更新"></span>
### When is the data for the previous day updated on the next day

The dataset will synchronize according to the configured synchronization time. If synchronization is set for 00:00 each day, updates will start at 00:00.

<span id="同步配置保存时显示数据量超量，要求缩小数据范围或缩短保留天数怎么办"></span>
### When saving the synchronization configuration, if the data volume exceeds the limit and you are prompted to reduce the data range or shorten the retention period, what should you do?

Change the lifecycle to 7 days. After creation, then go to Synchronization Status to modify the desired lifecycle.

<span id="_1-6-数据集编辑-修改-删除常见问题"></span>
## 1.6 Common issues with editing, modifying, or deleting datasets

<span id="底表字段更新后数据集未更新"></span>
### After updating the base table fields, the dataset is not updated

**Similar issues:** 

> Fields have been added to the upstream data, but they do not appear in the dataset

> After modifying the base table field type, the dataset field type is not synchronized

> After the underlying table is updated, there is no data in visual queries.

> Newly added fields in the dataset are not visible


After adding or modifying fields in the underlying table, update the selected fields in the dataset model configuration. After updating, resynchronize the dataset so that the new fields will have data. Once the new fields for the corresponding dates have data, perform the corresponding visual queries.

<span id="已经建好的看板对应的数据集能改吗"></span>
### Can the dataset associated with an existing dashboard be modified


1. Non\-performance settings of the dataset can be modified directly. After modification, wait for the execution to complete, then query in the dashboard (historical data needs to be resynchronized manually).

2. Performance settings of the dataset cannot be modified

3. If you change fields, ensure that the field names used in the dashboard remain unchanged to avoid query failures.


<span id="数据集删了图表还在吗"></span>
### If the dataset is deleted, will the charts remain?

After a dataset is deleted, the corresponding chart is also deleted from the chart list page. The chart still occupies its position on the dashboard, but a "No record found in the database" message is displayed.

After a dataset is restored from the recycle bin, the chart is restored in the chart list, and the chart remains in its position on the dashboard as normal.

If a chart is deleted from the chart list, it is permanently deleted. The chart disappears from the dashboard, which affects the layout.

<span id="数据集删除字段后无法保存"></span>
### After deleting a field from a dataset, saving is not possible.

Please check the following: 1. If the deleted field is a join field, replace the join field. 2. If other fields depend on the deleted field, delete those fields or modify the dependencies.

<span id="_1-7-其他数据集管理常见问题"></span>
## 1.7 Other common issues in dataset management

<span id="创建类目之后如何对字段进行分类"></span>
### How to categorize fields after creating a category

Go to the corresponding dataset, click Edit Field, and select a category for the fields that need to be categorized.

<span id="可视化查询界面如何查看数据集owner"></span>
### How to view the dataset owner in the visual query interface

Click the ⋮ next to the dataset name and select View Dataset to see the dataset details and owner.

<span id="数据集的底表名如何查"></span>
### How to find the base table name of a dataset

Go to the visual query interface for the dataset, click View Query History in the upper right corner, and select the SQL details of any historical query to see the corresponding ClickHouse table name for the dataset.
