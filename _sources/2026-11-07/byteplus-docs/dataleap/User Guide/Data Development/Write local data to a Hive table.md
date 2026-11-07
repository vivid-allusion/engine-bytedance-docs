---
title: "Write local data to a Hive table"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/write_local_data_to_hive_table"
---

When running EMR Hive, Serverless Spark, Presto, or Hive tasks in DataLeap, all internal tables are sourced from Hive tables in Volcengine E\-MapReduce (EMR) Hadoop clusters or Volcengine Serverless clusters. DataLeap data development supports importing data from local files, such as CSV files, into Hive tables via data integration tasks. This article will introduce the process for writing local data.

<span id="8e52e51e"></span>
## Function scenarios

DataLeap provides the capability to write local data to Hive tables, allowing you to upload local file data, such as CSV format files, to Volcengine Object Storage (TOS). By configuring offline integration tasks for TOS data sources, you can read data from TOS and securely and efficiently synchronize it to the target table in the Hive data warehouse. Applicable to the following scenarios:


* **Offline data migration**: Migrate historical business data stored on local servers, such as data exported from Excel, to the Hive warehouse for long\-term storage and analysis.

* **Batch data loading**: Local batch results generated daily by the business system, such as order summary data, are periodically written to Hive partition tables for subsequent use in BI reports and big data analysis tasks.

* **Test data import**: During business development and testing, locally constructed test data is quickly written to Hive test tables to verify the correctness of downstream analysis logic.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9765b9d96db47cb9737f17e0f995d01~tplv-goo7wpa0wc-image.image) </span>

<span id="2a9d9d2f"></span>
## Prerequisites for use


* Enable an EMR Serverless Spark \*\*\*\* queue resource instance, and bind it in the DataLeap project console. See [Queue management](https://docs.byteplus.com/en/docs/E-MapReduce/Serverless_Queue_management) and [Create a project](https://docs.byteplus.com/en/docs/dataleap/create_project).

* Enable the TOS service, create a TOS bucket, and grant the sub\-user operator the relevant TOS Console operation permissions. For details, see [Create a bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket) and [ACL policy management](https://docs.byteplus.com/en/docs/tos/docs-bucket-acls).

* Create a dedicated data integration resource group with appropriate resource specifications, and bind it under the successfully created DataLeap project. For details on purchasing operations, see [Exclusive Integrated Resource Group Management](https://docs.byteplus.com/docs/dataleap/exclusive_integrated_resource_group). For details on project binding operations, see [Data Integration Resource Group](https://docs.byteplus.com/docs/dataleap/datasail_resource_group).

* Before configuring a data integration task, you must prepare the data sources for the source TOS and the target Hive. For detailed instructions on creating data sources, see [Data source registration](https://docs.byteplus.com/docs/dataleap/69126#_3-1-%E6%95%B0%E6%8D%AE%E6%BA%90%E6%B3%A8%E5%86%8C) and [Data source registration](https://docs.byteplus.com/docs/dataleap/69123#_5-1-%E6%95%B0%E6%8D%AE%E6%BA%90%E6%B3%A8%E5%86%8C).

* Prepare your CSV file (skip this step if the file is already in Volcano Cloud TOS).


<span id="6fad3a69"></span>
## Cautions


* When configuring TOS data source field mappings, if the collection type for a TOS field with the same name is a generic type such as MAP, the automatically generated field type must be manually adjusted. MAPshould be changed to MAP<String,String\> format.

* CSV data files prepared locally for upload must use commas as delimiters and be saved in UTF\-8 encoding. The sample file is as follows:

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00856df6b2b149448709b880379d9fb6~tplv-goo7wpa0wc-image.image" name="csv_demo.csv">csv_demo.csv</Attachment>
   


<span id="8f4da48b"></span>
## Process overview

To write local data to a Serverless Hive table for big data analytics scenarios, you need to perform the following steps:


1. Step 1: Prepare your CSV file

   Imported CSV files must use the English comma as the delimiter and be encoded in UTF\-8 format.

2. Step 2: [Upload files to TOS](https://docs.byteplus.com/docs/dataleap/write_local_data_to_hive_table#7bd65600)

   If the file has already been uploaded to Volcano Cloud TOS, you may skip this step. Go to the [TOS Console](https://console.byteplus.com/tos/bucket?) and upload the CSV file to TOS.

3. Data source configuration: You must complete the data source configuration for both the source TOS and the target Hive. For details on creating a data source, see [Data source registration](https://docs.byteplus.com/docs/dataleap/69126#_3-1-%E6%95%B0%E6%8D%AE%E6%BA%90%E6%B3%A8%E5%86%8C) and [Data source registration](https://docs.byteplus.com/docs/dataleap/69123#_5-1-%E6%95%B0%E6%8D%AE%E6%BA%90%E6%B3%A8%E5%86%8C).

4. Step 3: [Integration task configurations](https://docs.byteplus.com/docs/dataleap/write_local_data_to_hive_table#196b209b)

   Create a data integration task for the TOS2Hive channel to write CSV file data located at the specified path in TOS to a Hive table. During task configuration, you can use the Hive **One\-Click Table Creation** feature to quickly create Hive tables in the EMR Serverless cluster for data that will be imported.

5. Step 4: [Verify the data lake ingestion results](https://docs.byteplus.com/docs/dataleap/write_local_data_to_hive_table#4bdde5b9)

   Once the data integration task has been successfully debugged, you can use the DataLeap temporary query feature to quickly verify whether the data has been successfully imported into the Hive tables of the EMR Serverless cluster.


<span id="7bd65600"></span>
## Upload files to TOS

Upload the locally prepared CSV file to the corresponding path under the already created TOS Bucket. Reference for upload operations as follows:


1. Log in to [TOS Bucket List Console](https://console.byteplus.com/tos/bucket?).

2. Click the information for the **Bucket name** you have created to view the file list, then click the **Upload file** button to perform the upload operation.

3. On the file upload interface, click the **Select File** button to choose a prepared local CSV file, then click the **Upload** button to complete the file upload operation.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9df45adb4ddd4046a63ba1c9adeb55a8~tplv-goo7wpa0wc-image.image) </span>

4. After the file is uploaded, click the **Actions** column in the list and then the **Details** button. Copy the suffix of the file URL so that you can fill it in when configuring the integration task.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c6ed3bfe8a2442094d21e0a17e6ae63~tplv-goo7wpa0wc-image.image) </span>

   For more instructions on upload operations, see [Upload files](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file).


<span id="a2b78c55"></span>
## Create a CSV import task

After successfully uploading a local file to TOS, you can access the data development interface and begin creating new TOS\-related channel tasks.


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc) **.** 

2. In a specific project, navigate to the **Data Development \> Metadata** interface, select the EMR Serverless Spark or EMR Serverless Presto engine type, and click the **More** button to create a CSV import task.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79d4d50ff44e49259149ecdfe85ded73~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By default, tasks are created in the "CSV file import" directory and named as "CSV import_username_${date}". You may manage the file name and directory as needed. When renaming a task, the name may only contain the following characters: period (.), letters, numbers, underscore (_), hyphen (\-), square brackets ([]), corner brackets (【】), parentheses (()), and Chinese characters. The task name must not exceed 127 characters.   </div>
   

<span id="196b209b"></span>
## Integration task configurations

<span id="71ce1d57"></span>
### Data sources and target configuration

By default, the CSV import task has preselected the data source types for the source and target, which are TOS and Hive, respectively.


1. **Configure reading from TOS data sources**

   
   |Parameters |Note |
   |---|---|
   |Data source types |TOS data source type is selected by default. |
   |Data source name |TOS data sources that have been successfully registered in data source management are available for selection from the dropdown menu.<br><br>If you have not yet created the corresponding data source, you can click the **Data source management** button to proceed to create a TOS data source. |
   |File paths |Enter the path to the TOS data file to be collected. Here, you can paste the file path that you copied after [Upload files to TOS](https://docs.byteplus.com/docs/dataleap/write_local_data_to_hive_table#7bd65600). Format (for example: doc_csv_demo/tos_test_csv.csv)<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The file path includes ^, \*, and ? Paths containing symbols such as , [ , ] , { ,</div><br><br><br>* <div data-tips="true" data-tips-type="tip">File path instructions</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">You do not need to include the Bucket name, and do not start with a slash (/).</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">You can configure the directory and specify the specific file name. If a directory is configured, only the files directly under the current directory are read; subdirectories are not processed recursively. If specific files are configured, filenames that begin with '.' or '_' are not supported.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Supports configuration file paths using the "\*" wildcard;</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Supports configuring date parameters in regular expression format, such as bigdata/t_user/${date</div><br> |
   |\*Data type |Supports selecting several data type, such as json, pb, parquet, csv, txt, etc. Here, the CSV type is selected. |
   |Delimiter |Select the delimiter for the original CSV file, such as ",", "Tab", ";", and so on, from the dropdown list, or specify a custom delimiter. Select "," as the separator. |
   |The original character set |You must select the character set for the original file; you can choose GBK or UTF\-8 format. Select UTF\-8 format here. |
   |Import the starting row |Indicate whether the uploaded CSV file contains header information: enter 0 if there is no header, or 1 if there is a header. |
   

2. **Configure Hive data source writing**

   
   |Parameters |Note |
   |---|---|
   |Target types |Hive data source type is selected by default. |
   |Data source name |Hive (EMR Serverless Hive) data sources that have been successfully registered in data source management are available for selection from the dropdown.<br><br>If the corresponding data source has not been created, you can click the **Data source management** button to go to the page for creating a Hive data source. |
   |Data table |Select the Hive table to write data into from the dropdown.<br><br><br>* One\-click table creation: For EMR Serverless Hive (LAS Catalog) table types only, when the target table has not yet been created and you have already selected the table or file to be collected from the source and have retrieved the field mapping from the source, you can click the "One\-click table creation" button. Based on the field information collected from the source, a pop\-up window will appear in the current window, allowing you to quickly edit and create the DDL statements for the target table within the pop\-up.<br><br>* Quick table creation: If the target table has not yet been created, you can also click the **Quick table creation** button to go to the data map interface. There, you can create EMR Hive and EMR Serverless Hive (LAS Catalog) tables based on the field information collected from the source.<br><br>* Modify the data table: If any fields collected from the source are updated, you can click the **Modify Data Table** button to promptly modify the target table fields. |
   |Partition settings |Partition fields are automatically retrieved from Hive tables.<br><br>The partition type supports selecting either a dynamic partition type or a specific partition field type:<br><br><br>* Dynamic partitioning: Data is written dynamically based on the values of source fields. The fields used for dynamic partitioning must exist in the source Columns. After selecting the dynamic partition type, the table partition fields can be automatically added to the field mapping below.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The source\-side value for the dynamic partition field can be empty. In this case, the synchronization task will write it as an empty partition in Hive, using "" as the value.   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Displayed as "<strong>HIVE_DEFAULT_PARTITION</strong>".   </div><br>   <br><br>* For details about parameter variables, see [Description of platform time variables and constants](https://docs.byteplus.com/docs/undefined/689d96727654f3051453d252). |
   |Data writing methods |Select the method for writing target data from the dropdown; the following two methods are supported:<br><br><br>* insert overwrite: Existing data is deleted before new data is written.<br><br>* insert into: Directly writes new data into the table. |
   


<span id="b189b888"></span>
### Field mapping

After configuring the data source and target, you need to specify the field mapping between the source and target. Based on this mapping, the data integration task writes data from the source fields to the corresponding target fields.

In basic mode, you can manage field mapping relationships in the following four ways:


* Same\-name mapping: After configuring the target field information, click the **Same\-name mapping** button in the source field mapping area to set up same\-name field mapping.

* Auto add: When the source TOS data type is **csv, txt, json, or pb**, click the **Auto add** button to automatically process the source field information.

* Manual add: Click the **Manual add** button to manually edit the field information for the source and target, and add each field individually.

* Move or delete fields: You can also change the order of field mappings or delete fields as needed.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When configuring TOS data source field mappings, if the collection type in a mapping with the same field name is similar to a generic MAP, the automatically generated field type must be manually adjusted. MAPshould be changed to MAP<String, String\> format.</div>


<span id="5d7c22fb"></span>
### Task runtime parameters

After completing field mapping configuration, you can configure task runtime parameters as needed, such as expected maximum concurrency, dirty data, custom parameters, and other task runtime parameters. For details on advanced parameters, refer to [Advanced parameters](https://docs.byteplus.com/docs/dataleap/advanced_parameters).

<span id="d0f9cf61"></span>
### Select a data integration resource group

Click the **Data Integration Resource Group** select button on the right. In the popup window, select the information of the dedicated integration resource group for which the data source connectivity test was successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f79ca2e5e07149d495278c7a62c35b58~tplv-goo7wpa0wc-image.image) </span>

<span id="a793bb8a"></span>
### Debug tasks

After completing the task logic and parameter configuration, you can click the **Save** and **Debug** buttons in the toolbar at the top of the editor to debug the task.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Debugging operations. Exercise caution when directly using live data for debugging.</div>


After the debugging task starts running, you can view the debug log below. Click the **Debug log** button to view the following details:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79e0b5100fd14cd08f2b61e271debd7f~tplv-goo7wpa0wc-image.image) </span>


* Overview: View task execution status, business date, runtime duration, start time, and other task overview information.

* Monitoring: Offline integration tasks support viewing read and write monitoring metrics. You can click the **Data Integration Monitoring** button to go to the cloud monitoring interface, where you can view integration read and write metrics, resource group usage rate, and other monitoring information.

* Scheduling log: View log information for tasks during the scheduling and dispatching phase.

* Execution log: View detailed execution log information for tasks running in a dedicated integration resource group. From these logs, you can check the actual size of data read, the number of data records, the reasons for failure, and other information. For details on viewing execution logs, see [DataSail log viewing and diagnostics](https://docs.byteplus.com/docs/undefined/68c04b5ad4b05a04fd3d9fcb).

* Run events: View event information during task execution, such as task status changes, task failures, and restarts


<span id="4bdde5b9"></span>
## Verify the data lake ingestion results

After the debugging task is completed, you can use the **Data Development \> Ad Hoc Query** capability to query the actual data stored in Hive tables.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e435852e6b6b4502ba040d58950c3ba5~tplv-goo7wpa0wc-image.image) </span>


1. In the left navigation bar of the task development interface, enter the **Temporary Query** interface.

2. Click the **New Query** button to create an EMR Serverless Spark or EMR Serverless Presto query task.

3. In the query editing interface, select the compute queue information for the EMR Serverless engine, and enter the following query statement:

   ```SQL
   SELECT * FROM doc_demo.doc_csv_demo2 WHERE dt = '${date}' LIMIT 1000;
   ```
