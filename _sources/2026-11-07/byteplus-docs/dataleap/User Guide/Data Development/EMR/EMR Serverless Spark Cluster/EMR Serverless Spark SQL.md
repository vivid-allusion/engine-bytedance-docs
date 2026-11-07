---
title: "EMR Serverless Spark SQL"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/emr_serverless_spark_sql"
---

DataLeap supports integration with Serverless Spark Instances in BytePlus E\-MapReduce (EMR), allowing users to develop jobs using Spark SQL within DataLeap Data Development and enabling customized data processing and query analysis through periodic scheduling. The following is a detailed description of the EMR Serverless Spark SQL task configuration in DataLeap

<span id="27081bf1"></span>
## 1 Background information

In the field of big data processing, enterprises have a growing demand for efficient, convenient, and open source\-compatible computing tools. The fully managed EMR Serverless Spark data product has emerged in response to market demand. Features include out\-of\-the\-box readiness, no additional cluster management required, and full compatibility with the open\-source Spark engine. EMR Serverless Spark SQL tasks can be used to process data in metadata tables within the LAS Catalog database. They support SQL job development using Spark SQL and perform the parsing and submission of Spark SQL tasks. The syntax is 100% compatible with the open\-source Spark 3.5.1 version. For detailed syntax, refer to [Spark 3.5.1 version](https://spark.apache.org/docs/latest/sql-ref-ansi-compliance.html).

<span id="85cd347b"></span>
## 2 Use restrictions


1. You must enable the DataLeap service version that includes either both **Big Data Analytics and DataOps Development** services, or the **Distributed data autonomy** service, before the project can continue binding **EMR Serverless Spark** instances. See details [Billing Instructions for Version Services](https://docs.byteplus.com/docs/dataleap/Billing_Instructions_for_Version_Services).

2. The SQL query results may display less data than the actual data volume because the results page has a preview data limit of 1000, and all project data security settings impose restrictions. It is recommended to handle as follows:

   1. Go to [Project Console](https://console.byteplus.com/dataleap/studio/console/config?project=) to set the upper limit for project data security settings to 10,000 rows.

   2. **Project Console \> Configuration information \> Data security settings** \> In the query results, select **Enable Download**. You can then click the **download** button in the query results area to download the complete data to your local device for viewing.

      For details about the action, see: [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project).

3. This task type does not yet support sending message notifications after a debug execution succeeds or fails.


<span id="10599a24"></span>
## 3 Use prerequisites


1. A queue resource instance for **EMR Serverless Spark** has been enabled. See [Queue management](https://docs.byteplus.com/en/docs/E-MapReduce/Serverless_Queue_management) for details.

2. In the DataLeap Project Console, the relevant EMR Serverless Spark service instance has already been bound. See details[Create a Project](https://docs.byteplus.com/docs/dataleap/create_project).

3. When sub\-users access EMR Serverless Spark queue resources, they must ensure they have the EMRServerlessFullAccess or EMRServerlessReadOnlyAccess permission policy. Sub\-users can request the main account to add the permission policy to the access control interface, or configure the corresponding permissions through a custom policy.


<span id="573df877"></span>
## 4 New Task


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc).

2. In a specific project, go to the **Data Development** interface and click the **New Task** button to create a task.

3. Go to **Data Development \> EMR Serverless Spark \> EMR Serverless Spark SQL** and select the task type.

4. Fill in the Basic Task Info, click the **Confirm** button, and complete the task creation.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">In the project console management interface, if you add or modify an engine, you need to refresh the entire DataLeap data development interface while in the task creation window. Only then will you be able to see the newly added or modified engine task type.</div>


2. <div data-tips="true" data-tips-type="warning">The task name may contain only periods, letters, numbers, underscores, hyphens, square brackets, full\-width square brackets, parentheses, and Chinese characters, and must not exceed 127 characters.</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c493bb6656fd401cb3707e04859a50ac~tplv-goo7wpa0wc-image.image) </span>

<span id="1dad948d"></span>
## 5 Task configuration description

<span id="d5f2be9d"></span>
### 5.1 Edit SQL code

After the task is created successfully, the code editor interface opens. An example SQL statement is shown below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you do not specify a TOS bucket path when creating a database, it will be created by default in the specified Hive database storage location configured in the LAS Catalog Console.</div>


* <div data-tips="true" data-tips-type="tip">SQL statements support the capability for time parameters and custom parameters. For details on time parameters, see <a href="https://docs.byteplus.com/docs/undefined/689d96727654f3051453d252">Description of platform time variables and constants</a>. For details on the context parameter passing operation, see <a href="https://docs.byteplus.com/docs/dataleap/input_and_output_parameter_settings">Input and Output Parameter Settings</a>.</div>


* <div data-tips="true" data-tips-type="tip">In the following example statements, to access a custom Catalog, you can specify the <code>set spark.hadoop.hive.metastore.catalog.default=catalog_name</code> parameter, where catalog_name should be replaced with the actual Catalog name. Alternatively, in DML and DQL statements, you can access multiple Catalogs using the three\-part naming convention, for example: Catalog_name.db_name.table_name.</div>


* Access Hive table types in Spark:

   ```SQL
   --Create a database and specify a custom TOS bucket path for storage. You must ensure that the TOS bucket exists and that the current user has read and write permissions for the bucket path.
   create database db_demo location 'tos://your tos bucket name/warehouse/';
   
   -- Create Table
   CREATE  TABLE db_demo.table_01 (`id` INT, `name` STRING, `age` INT) PARTITIONED BY(date STRING);
   
   --insert data
   INSERT INTO TABLE db_demo.table_01 PARTITION (date = '20240403') VALUES(1, 'testyw', 26),
   (2, 'zhangsan', 26),
   (3, 'lisi', 23),
   (4, 'wangwu', 24),
   (5, 'liuliu', 23),
   (6, 'qiqi', 88);
   
   -- Data check
   SELECT  * FROM    db_demo.table_01;
   ```
   

* Accessing Iceberg table types with Spark:

   ```SQL
   -- Default parameters (required)
   set spark.sql.catalog.iceberg=org.apache.iceberg.spark.SparkCatalog;
   set spark.sql.catalog.iceberg.type=hive;
   set spark.sql.storeAssignmentPolicy=ansi;
   use iceberg;
   
   --Default: Create Iceberg tables in the Hive data directory:
   create database if not exists test_iceberg_db;
   create table if not EXISTS test_iceberg_db.test_tb(id int, name string);
   
   --Write and query Iceberg data:
   insert into table test_iceberg_db.test_tb values(1, 'hehe'),(2, 'haha');
   select * from test_iceberg_db.test_tb;
   
   ```
   

* Access Paimon table types with Spark:

   ```SQL
   -- Default parameters (required)
   set spark.sql.catalog.paimon=org.apache.paimon.spark.SparkCatalog;
   set spark.sql.catalog.paimon.metastore=hive;
   set spark.sql.storeAssignmentPolicy=ansi;
   -- Custom warehouse path, if not specified, the default is to use the TOS Storage Path corresponding to the current first Hive directory.
   set spark.sql.catalog.paimon.warehouse=tos://your tos bucket name/warehouse;
   use paimon;
   
   --Default: create Paimon tables in the Hive data directory:
   create database if not exists test_paimon_db;
   create table if not EXISTS test_paimon_db.test_tb(id int, name string);
   
   --Write and query Paimon data:
   insert into table test_paimon_db.test_tb values(1, 'hehe'),(2, 'haha');
   select * from test_paimon_db.test_tb;
   ```
   


<span id="c2950363"></span>
### **5.2 Parse the navigation bar function area**


|Function name |Description |
|---|---|
|Format |Format the code according to the SQL formatting style settings in [Personalize settings](https://docs.byteplus.com/docs/undefined/682aa7e55df38404fda1396d), so that its syntax is clear and concise. |
|Parse |Parse and check the syntactic and semantic correctness of the written SQL code. Check for syntax error messages before execution to prevent runtime errors.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If a task uses the <strong>Project parameters</strong> type in <strong>Schedule Settings \> Task Input parameters</strong>, and the encryption option is selected in <strong>Parameter Setting</strong>, an exception message will be displayed when someone other than the Project Administrator parses the task, because the encrypted parameters cannot be parsed. If you ensure that SQL matches the execution logic, you may skip this parse exception prompt.</div><br> |
|Execution engine |By default, you can choose the Spark Engine. |


<span id="fd77fcc2"></span>
## 6 Schedule settings

After the SQL task configuration is complete, click the **Scheduling Configuration** button in the right navigation bar to open the scheduling configuration window. Here, you can set the task **Basic Info, Scheduling attributes, dependencies**, and other information. For detailed parameter settings, see [Schedule Settings](https://docs.byteplus.com/en/docs/dataleap/scheduling_settings).


* When choosing **Scheduling Basic Info \> Compute Queue**, you can use the dropdown to select a bound Spark Compute Queue in the Project Console. SQL tasks support selecting the **Public queue**, **SQL Dedicated Resource**, or **Generic Resource** queue to execute EMR Serverless Spark SQL tasks.

   For more compute queue actions, see [Queue management](https://docs.byteplus.com/en/docs/E-MapReduce/Serverless_Queue_management).

* When selecting **Scheduling Basic Info \> Use project template?** , you can choose whether the current task uses a template that has already been created in **Template management** of the Project Console, as needed. In template management, you can create generic template content such as execution queue, priority, parameter setting, and more to improve the efficiency of daily task configuration. See details[Template Management](https://docs.byteplus.com/docs/dataleap/template_management).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For tasks that use a project template, the configuration specified in the template will overwrite the task's original configuration. The template configuration cannot be modified within the task. If you need to modify template parameters, you need to go to <strong>Project Console \> template management</strong> to make changes. This operation will affect all tasks that use this template, so please operate with caution.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c52e9848bbe42f9a467adb4e756a4ea~tplv-goo7wpa0wc-image.image) </span>


<span id="ef6b0b02"></span>
### 6.1 **Register the data produced by the task**

Register the data produced by the task to record task and data lineage information; this does not affect code logic. You can configure output registration information in the **Schedule Settings \> Register the data produced by the task** section.

For other tasks where the system cannot obtain output information by parsing, EMR Serverless Spark SQL tasks can register their output information automatically or manually. If a task involves the output of LAS Catalog Database & Table Data, it is strongly recommended to fill in this information to facilitate subsequent maintenance of task data lineage.


* Automatic registration:

   When task output data uses the automatic registration mode, each time the task is activated, the system will automatically update based on the code parsing results. You can click the **View output data for the "Production version"**  or **View output data for the "Draft version"**  button to view the automatic registration results of output data for different versions of the current task.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When choosing Automatic registration, if a field name in the SQL code query contains an SQL keyword, you must escape it by adding escape characters. For example, escape group as `group` and order as `order`. If escaping is not performed, it will affect the display of data lineage graphs, table production information, and other content in the Data Catalog. Alternatively, you may use the <strong>Manual registration</strong> option below to manually register task output data.   </div>
   

* Manual registration:

   The content you manually fill in will be the task output. You can fill in multiple entries. When configuring other task dependencies, you can go to the **Schedule Settings** page and use either **Dependency Recommendations** or **Add manually** to search for and add dependencies based on the Database/Table names produced by this EMR Serverless Spark SQL task. The specific registration content includes the following data types:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have just created tables via SQL and cannot select tables during manual registration, you can first go to <strong>Data Catalog \></strong> <strong>Metadata Ingestion</strong> and manually execute metadata ingestion. After that, you can continue with manual registration and select tables. For details on manually executing the collection operation, see <a href="https://docs.byteplus.com/docs/dataleap/Metadata_Ingestion">Metadata Ingestion</a>.   </div>
   

   * EMR Serverless Spark: This task logic will write data to a LAS Catalog table. You need to fill in the LAS Catalog data directory, database name, table name, and partition name. Partition content can use variables, for example, in the form of ${date}, ${hour}.

   * Other: The logic of this task does not write data to the LAS Catalog table.


<span id="bd996a75"></span>
## **7 Debug**

Once the code logic and parameter configuration are complete, click the **Save** and **Debug** buttons, and you can start running the task. You can also view debug records below:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Caution: Debug actions that use online data directly require careful handling.</div>


* <div data-tips="true" data-tips-type="warning">This task type does not yet support sending message notifications after a debug execution is successful or fails.</div>


* <div data-tips="true" data-tips-type="warning">Debug log data in the Data Development interface is retained for 15 days. You can view the corresponding debug log details within 15 days.</div>


* On the left side of the Debug records, you can filter historical executions by selecting **Debug status** to display records for different debug statuses.

   * Move the mouse pointer over the debug record to view information including state, business time, committer, and more.

   * **Double\-click** Debug records, then you can edit the debug name and press Enter to save.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4d23ed7b73f485cb00dfb28075e7ceb~tplv-goo7wpa0wc-image.image) </span>

* Click Debug records. On the right side of Debug records, you can view the log, results, and other detailed information for Executions.

   * Overview: View an overview of the run result, including the debug business date, execution duration, the Tracking URL for execution details, and other information.

   * Log: View task execution log details. Here, you can view log details for the engine's JobManager, Submit, and Driver. You can also go to [EMR Serverless Spark Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/serverless/queue_manage?StatusesInclude=0) \> Queue Details \> calculation group \> Job instance management tab to view more detailed log information about the task run.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can use the Engine Instance Name or Engine Instance ID information from the DataLeap execution log to search for related log information in the EMR Serverless Spark job instance management interface.      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85fc6e693b3444da9e918c5cac619142~tplv-goo7wpa0wc-image.image" width="1276px" />      </div>
      

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b7b8e349cc594ef191d59ca851aa1a63~tplv-goo7wpa0wc-image.image) </span>

   * Results: View the query results after running the code.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Because the preview data on the results page is limited to 1000 and there are restrictions in project data security settings, the data displayed in query results may be less than the actual data volume. It is recommended to handle as follows:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Go to the <strong>Project Console</strong> and set the upper limit for project data security settings to 10,000 rows.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Project Console \> Configuration information \> Data security settings</strong> \> In the query results, select <strong>Enable Download</strong>. You can then click the <strong>download</strong> button in the query results area to download the complete data to your local device for viewing.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For details, see <a href="https://docs.byteplus.com/docs/dataleap/create_project">Create a Project</a>.   </div>
   


<span id="c6ce3d65"></span>
## **8 Commit task**

After the debug task is successful, click the **Save** and **Commit for Deploy** buttons in the top action bar. In the **Commit for Deploy** dialog box, select parameters such as **Backfill data, Monitor Settings, and Commit settings**. Finally, click the **Confirm** button to complete the job submission. For deploy instructions, see [4 Commit for Deploy](https://docs.byteplus.com/docs/dataleap/data-development-overview#_5-%E6%8F%90%E4%BA%A4%E4%B8%8A%E7%BA%BF).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the tenant main account or project administrator has enabled pipeline process validation in <strong>Project Console\>Pipeline Management</strong>, you need to ensure that the submitted task complies with the validation rules of the pipeline extension in order to submit successfully. See details <a href="https://docs.byteplus.com/docs/dataleap/data-development-overview#_4-%E6%B5%81%E6%B0%B4%E7%BA%BF%E7%AE%A1%E7%90%86">3 Pipeline Management</a>.</div>


See details of subsequent task operations: [Task Operation](https://docs.byteplus.com/docs/dataleap/task_operation).

&nbsp;
