---
title: "DataLeap on EMR Quick Start"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/DataLeap_EMR_Quick_Start_"
---

This article introduces how to use the DataLeap suite for big data development and governance to implement data integration, development, metadata management, and quality monitoring for Volcano Engine E\-MapReduce (EMR) clusters, for example:


1. Import data from a MySQL data source into an EMR Hive database through a data integration task.

2. Create and execute jobs through data development tasks.

3. Monitor fluctuations in Hive table data and perform data profiling through data quality monitoring.

4. View Hive database and table information in the EMR cluster through the data catalog.


<span id="_1-前提条件"></span>
## prerequisites


1. The EMR service has been enabled and the service account authorization has been completed. For details, see [Preparation](https://docs.byteplus.com/docs/E-MapReduce/118287).

2. The DataLeap service has been enabled and the service account authorization has been completed.

3. A data integration resource group has been created in the same VPC as the EMR cluster. For details, see [Resource Group Management](https://docs.byteplus.com/en/docs/dataleap/public_resource_group).

4. Prepare the source MySQL data source. This example uses Volcano Engine Cloud Database MySQL Edition. For details, see [Quick Start](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).


<span id="_2-创建集群及项目"></span>
## Create a cluster and project

<span id="_2-1-创建-emr-hadoop-集群"></span>
### Create an EMR\-Hadoop cluster


1. Log in to the [EMR Console](https://console.byteplus.com/emr).

2. In the left navigation pane, click **Cluster List \> Create Cluster** to start creating a cluster.

3. Click the **Quick Create** button in the upper right corner to complete configuration items such as Software configuration\*\*,**Payment settings**,**Availability zone**,**Network configuration**,**Instance Settings**,\*\*basic information and other configurations. For detailed configuration information, see: [Create a cluster](https://docs.byteplus.com/docs/E-MapReduce/ecs_create_a_cluster_3190_and_later).

4. After filling in the configuration parameters, select **I agree to the EMR Service Terms,**  and click the **Create now**button to complete cluster creation.

5. Go to **Cluster Console \> Cluster List** to view the created cluster. When the cluster status updates to **Running**, the creation is successful.


<span id="_2-2-创建-dataleap-项目"></span>
### Create a DataLeap project


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/r).

2. Click **Project Management** in the left navigation pane to enter the **Project Management** page.

3. Click the **Create Project** button to enter the **Create Project** page and complete the project basic information, project governance, service binding, and other project configurations. For configuration details, see [Create Project](https://docs.byteplus.com/en/docs/dataleap/create_project).

4. When binding services, select the data integration resource group and EMR cluster that have been successfully created.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">DataLeap currently supports quick mode binding of EMR clusters. In this mode, <strong>all EMR tasks under the project are executed by flowagent (for versions above 3.4.0, the execution user changes to admin)</strong>.   </div>
   

<span id="_3-配置数据集成任务"></span>
## Configure a data integration task

Data integration is a stable and efficient data synchronization platform dedicated to providing high\-speed and stable data synchronization capabilities among a wide range of heterogeneous data sources.

<span id="_3-1-配置数据源"></span>
### Configure data sources

After the DataLeap project is created, you can proceed with the following operations:


1. In the project management list, click **Configuration Information** to enter the project console.

2. On the **Project Console** page, in the left navigation bar, click the **Data Source Management** button to go to the **Data Source Management** page.

3. On the **Data Source Management** page, you can start adding MySQL and Hive data sources.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The data integration resource group selected for data source connectivity testing must be in the same VPC as the MySQL and EMR Hive databases to ensure successful network access. If the data source is in a different network environment, you can access it via the public network or consult DataLeap technical support by <a href="https://console.byteplus.com/workorder/create/">submitting a ticket</a>.   </div>
   

<span id="_3-2-配置数据集成同步任务"></span>
### Configure data integration synchronization tasks

After the data source connectivity test is successful, you can continue to configure data integration synchronization tasks.


1. In the upper left corner of the project console, under **All Products**, go to the **Data development**page.

2. On the Data Development page, click the **Create Task** button to enter the task creation page.

3. Select **Data Integration \> Offline Integration** as the task type.

4. Enter the task name and select the target folder.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Caution:</strong> Task names are limited to the following characters: ., letters, numbers, underscores, hyphens, [], 【】, （）, (), and Chinese characters, with a maximum of 127 characters.   </div>
   

5. Click the **OK** button to complete task creation and enter the task configuration page.

6. Use the interface wizard to configure the MySQL_to_Hive integration task.

   After the integration task configuration is complete, you can continue with the following operations:

   1. Scheduling settings: Set up periodic scheduling and upstream/downstream dependencies for the task to automatically trigger execution at specified times, improving execution efficiency. For details, see [Scheduling Settings](https://docs.byteplus.com/en/docs/dataleap/scheduling_dependencies).

   2. Save: Save the task, including the current node code and related configurations.

   3. Debug: Run the current node's task configuration to test task execution in the data development environment.

   4. Submit for production: Submit the job to the production environment for periodic scheduling execution .


<span id="_4-数据开发"></span>
## Data development

DataLeap data development is a big data development IDE that integrates batch and stream development, providing developers with an efficient and intelligent development environment. Supports rapid creation of development tasks related to the EMR engine, code development, running queries, and more. You can directly operate EMR\-related data on the DataLeap platform.

<span id="_4-1-数据开发类型"></span>
### Types of data development tasks

Data development tasks are used for periodic scheduling and manual scheduling/execution. The EMR engine supports the following task types:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The EMR engine currently supports binding to several cluster types, including <strong>Hadoop, TensorFlow, Flink, StarRocks, Doris</strong>. Among these, StarRocks and Doris clusters only support binding to EMR\-3.2.1 and later cluster versions.</div>


* <div data-tips="true" data-tips-type="warning"><strong>To create an EMR streaming data task, at least one of the following conditions must be met:</strong></div>


   * <div data-tips="true" data-tips-type="warning">Hadoop clusters of EMR\-3.2.1 and later versions that include Flink and GTS component services are supported.</div>


   * <div data-tips="true" data-tips-type="warning">Hadoop or Flink clusters of EMR\-1.3.1 version with Flink component services included are supported.</div>


* <div data-tips="true" data-tips-type="warning">If the Flink component service is added after the EMR cluster is successfully created via <a href="https://docs.byteplus.com/docs/E-MapReduce/ecs-add_or_restart_services">Add/restart services</a>, you must first restart the OSSA service on the EMR management side before continuing to use the related functions of the corresponding service.</div>


* <div data-tips="true" data-tips-type="warning">If the project is bound to EMR\-3.4.0 or later versions, you can accelerate the execution efficiency of EMR Spark tasks by adding the Kyuubi service and restarting the OSSA service.</div>


* Offline data:

   * EMR HSQL: Process EMR data by editing EMR HSQL statements.

   * EMR Spark: Use Java Spark to process data, primarily for large\-scale data analysis and processing and more.

   * EMR HDFS\-sensor: Monitor data in upstream HDFS file paths.

   * EMR Hive\-sensor: Monitor partitioned data in upstream Hive tables.

   * EMR report task: The EMR report task sends the results of EMR SQL queries via email to external recipients.

* Streaming data:

   * EMR Flink SQL: Use EMR Flink SQL to perform ETL and many other operations between different storage systems.

   * EMR Java Flink: Host, manage, and operate native EMR Java Flink tasks.


<span id="_4-2-临时查询类型"></span>
### Temporary query types

Temporary query types are used for simple, one\-time test queries based on EMR engine capabilities. For example, after a data integration task is successfully debugged, you can create a query task in the temporary query interface to query EMR Hive table data. For details, see [Temporary query](https://docs.byteplus.com/en/docs/dataleap/ad_hoc_query).

Temporary queries support the following query types:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To support each query type, the EMR cluster must include the following four components: <strong>Presto, Trino, Spark, Hive</strong>. This enables the creation of query types corresponding to each component.</div>


* <div data-tips="true" data-tips-type="warning">If the Presto or Trino component service is added after the EMR cluster is successfully created via <a href="https://docs.byteplus.com/docs/E-MapReduce/ecs-add_or_restart_services">Add/restart services</a>, you must first restart the OSSA service on the EMR management side before continuing to use the related functions of the corresponding service.</div>


* <div data-tips="true" data-tips-type="warning">If the project is bound to EMR\-3.4.0 or later versions, you can accelerate the execution efficiency of EMR Spark tasks by adding the Kyuubi service and restarting the OSSA service.</div>


* EMR Hive SQL: Supported since EMR\-1.0.0.

* EMR Spark SQL: Supported since EMR\-1.0.0.

* EMR Presto: Supported since EMR\-1.3.0.

* EMR Trino: Supported since EMR\-1.3.0.

* EMR Doris: Supported only on Doris clusters, available since EMR\-3.2.1.

* EMR StarRocks: Supported only on StarRocks clusters, available since EMR\-3.2.1.


<span id="_4-3-发布中心"></span>
### Release center

The main objective of the Release Center module is to improve data development efficiency, standardize the task release process, distinguish between development and production environments, enhance production security and stability, and strengthen end\-to\-end capability building for data warehouse development. To bring data development tasks online, if you select **Submit only**, you need to go to the **Release Center** and , , Perform code submission, release package management, and other operations here.

<span id="_4-4-运维中心"></span>
### Operations Center

After the task is successfully submitted and released, you can go to **Operations center** to view task operations. In the top navigation bar, go to Offline Task Operations and Real\-time Task Operations. In Operations, you can view the task running status as needed, and perform operations such as setting up monitoring and alerts, starting tasks, stopping tasks, and viewing operation logs.

For details, see: [Offline Task Operations](https://docs.byteplus.com/en/docs/dataleap/task_operation), [Streaming Task Operations](https://docs.byteplus.com/en/docs/dataleap/task_operation).

<span id="_5-数据质量"></span>
## Data quality

The Data Quality Platform is a data quality management platform for data and its production pipeline. Its features include monitoring data volume, fluctuations in personalized indicators, abnormal alerts, data content exploration, and difference comparison, ensuring the reliability and validity of data in production and usage processes.

<span id="_5-1-新建监控规则"></span>
### Create a monitoring rule


1. In the upper left corner of the interface, under **All Products**, go to the **Data Quality** interface.

2. On the **Offline Data Monitoring \> Monitoring Object** page, select the EMR engine bound to the project as the engine type from the dropdown list.

3. Click the **Monitoring Object** button on the right to create a new monitoring object.

4. You can configure the types of data monitoring rules for EMR Hive tables as needed.

5. After completing the monitoring configuration, click the **Complete** or **Complete and Test Run** button in the lower right corner to finish creating the rule.


<span id="_5-2-查看试跑结果"></span>
### View test run results

When configuring monitoring rules, click the **Complete and Test Run** button to start the rule test run.


1. Click **Test Run Results** in the left navigation bar to view the test run results page.

2. In the action bar, you can view the rules, executed SQL, operation logs, and other information for the current Hive table test run. For details, see [Manage Test Run Results](https://docs.byteplus.com/en/docs/dataleap/Manage_Hive_Template_Rules_Run_Results).


<span id="_5-3-数据探查"></span>
### Data exploration

When using EMR Hive tables, you can perform data exploration, generate exploration reports with one click, and view the results.

Currently, support is provided for [full exploration](https://docs.byteplus.com/en/docs/dataleap/Full_probe) and [dynamic exploration](https://docs.byteplus.com/en/docs/dataleap/Dynamic_Probe) capabilities for databases and tables under the EMR engine.

<span id="_6-数据地图"></span>
## Data Map

Data Map uses a graphical end\-to\-end data table management tool, provides field\- and partition\-level metadata lineage visualization, and enables you to obtain the entire data production chain information through data lineage relationships, addressing the difficulty in finding and understanding data.

You can perform **data search, metadata collection, table management** and **view lineage graph** operations for EMR engine databases and tables on Data Map:


* On the [data search](https://docs.byteplus.com/en/docs/dataleap/Search_Data) interface, you can directly search for Hive table keywords to retrieve table data, view table details, preview data exploration, and view the table's DDL.

* On the [lineage graph](https://docs.byteplus.com/en/docs/dataleap/Lineage_Application) interface, you can analyze upstream and downstream lineage information that Hive tables depend on, locate the impact level of the current table, and identify task dependencies and scheduling.

* On the [metadata collection](https://docs.byteplus.com/en/docs/dataleap/Metadata_Ingestion) interface, you can perform metadata collection operations for EMR clusters, synchronizing metadata information to Data Map for viewing related metadata.

* On the [table management](https://docs.byteplus.com/en/docs/dataleap/my-db-table) interface, unified management capabilities are provided for creating, editing, deleting, and assigning permissions for EMR cluster metadata tables.
