---
title: "Overview"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/data-development-overview"
---

DataLeap, the Data Development integrated development environment (IDE) for Big Data, consolidates batch and flow development to provide developers with an efficient and intelligent development environment. Supports quick creation of development tasks, code development, and running queries. The main modules include Data Development, Ad\-hoc Query, Database, Resources Library, and Function Library.

<span id="_2-支持引擎介绍"></span>
## 1 Supported Engine Introduction


* **E\-MapReduce (EMR)** : BytePlus E\-MapReduce builds enterprise\-level big data analytics systems using the open\-source Hadoop ecosystem, fully compatible with open\-source and includes integration and management of big data components like Hadoop, Spark, Hive, Flink, StarRocks, Doris, as well as supports [EMR Serverless](https://docs.byteplus.com/en/docs/E-MapReduce/Product_Overview) forms to help users easily build enterprise big data platforms, reduce operation thresholds, and quickly develop big data analysis capabilities.

* [BytePlus Flink](https://www.byteplus.com/en/product/flink) **:**  BytePlus Flink Edition is a fully managed, cloud\-native real\-time data platform that delivers out\-of\-the\-box Apache Flink compatibility, serverless elasticity, and end\-to\-end observability—enabling unified stream and batch processing with minimal TCO and enterprise\-grade reliability.

* [ByteHouse Enterprise Edition (ByteHouse CE)](https://docs.byteplus.com/en/docs/bytehouse/reference-reference),[ ByteHouse Cloud Data Warehouse Edition (ByteHouse CDW)](https://docs.byteplus.com/en/docs/bytehouse/docs-docs): ByteHouse, optimized and modified from open\-source ClickHouse by BytePlus, offers stronger query and data writing performance for massive data, supporting applications like multi\-dimensional analysis of vast data, machine learning model evaluation, microservice monitoring, and statistics.


<span id="_3-数据开发流程概述"></span>
## 2 Data Development Process Overview

DataLeap data development, supported by various engine capabilities, offers multiple data development node types. You can choose engine\-bound nodes, generic nodes, data integration nodes, interactive analysis nodes, or workflow task modes for data development work and combine them with resource functions to develop more complex tasks. Once job configurations are complete, you can use platform scheduling capabilities to execute jobs periodically, set scheduling\-related parameters, and deploy the job to a production environment for regular scheduling.

Below is a brief overview of the data development process.

<span id="_3-1-新建任务"></span>
### 2.1 Create a New Task


1. Log in to the [DataLeap Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/overview?).

2. In the **Overview** interface, click **IDE** to enter the corresponding project.

3. In the **Data Development** interface, click **New Task** button in the left navigation bar to enter the **New Task** page.

4. After configuring the task parameters below, click **OK** button to complete the creation of the new task.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">To create an engine\-driven data development node, it is necessary to bind the engine at the time <a href="https://docs.byteplus.com/docs/dataleap/create_project">Create a Project</a> bindings are made.</div>


2. <div data-tips="true" data-tips-type="warning">The following binding engines, associated instances, and configuration parameters only need to be selected when the task classification selected is <strong>Data Development</strong>.</div>




|Parameters |Description |
|---|---|
|Select Task Type ||
|Task Mode |Supported to choose **Single Node Mode:** <br><br><br>* Single Node Mode: Choose specific single tasks based on specific task types. |
|Classification |Supported classifications: Data Development, Data Integration, Interactive Analysis. |
|Bind Engine |EMR Serverless, BytePlus Flink, ByteHouse CE,ByteHouse Cloud Data Warehouse Edition(ByteHouse CDW), Generic. |
|Associated Instance |Determined by the chosen bind engine:<br><br><br>* When the engine selects **EMR, ByteHouse CE,ByteHouse CDW**, the dropdown will display all bound EMR/ByteHouse CE clusters in the current project. Click to select. A single project can bind multiple EMR/ByteHouse CE clusters. See details [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project).<br><br>* When the engine selects **BytePlus Flink**, the dropdown will display the engine projects bound to the current project. Click to select.<br><br>* When the engine selects **Generic**, there is no need to select a related associated instance. |
|Select task |Choose the appropriate task type based on actual scenarios. |
|Basic Task Info ||
|Task name |The name of the current data development task, which only allows characters such as periods(.), letters, numbers, underscore (_), hyphens (\-), [], 【】,（）,(),and Chinese characters, cannot exceed 127 characters. |
|Save directory |Task save path. |
|Task description |Enter the description of the content of the task for easier subsequent management. |


<span id="_3-2-任务类型分类"></span>
### **2.2 Task Type Classification**


* Single Node Mode:

   DataLeap single node mode currently supports the following three types of nodes: Data Development, Data Integration, Interactive Analysis.


<span id="_3-2-1-数据开发类节点"></span>
#### 2.2.1 Data Development Nodes

Select the corresponding engine type node under the engine selection, and deploy the relevant code to the respective data cleaning engine for execution.

Data development nodes currently support selecting **EMR Serverless, BytePlus Flink, ByteHouse CE, ByteHouse CDW** and **Generic** engine types, with the supported task types listed as follows:


* **EMR Serverless Engine**

   
   |Engine Classification |Supported task types |
   |---|---|
   |EMR Serverless Spark |Batch data:<br><br><br>* [EMR Serverless Spark SQL](https://docs.byteplus.com/docs/dataleap/emr_serverless_spark_sql): Processing EMR Serverless Data with Spark SQL Statements<br><br>* [EMR Serverless Spark Java/Python](https://docs.byteplus.com/docs/dataleap/emr_serverless_spark_java_and_python) : Implement timed execution of EMR Serverless Spark Java/Python tasks |
   

* **BytePlus Flink Engine**

   
   |Engine Classification |Supported task types |
   |---|---|
   |BytePlus Flink |* Batch data:<br><br>   * [Flink Batch SQL](https://docs.byteplus.com/docs/dataleap/flink_batch_sql) : Execute Batch SQL through the Flink engine, which is consistent with Flink Streaming SQL to achieve stream\-batch integration.<br><br>   * [Java Flink Batch](https://docs.byteplus.com/docs/dataleap/java_flink_batch): Execute resource tasks of Flink Batch Jar through the Flink engine.<br><br>* Streaming Data<br><br>   * [Serverless Flink SQL](https://docs.byteplus.com/docs/dataleap/serverless_flink_sql): Implement ETL between different storage systems through Serverless Flink SQL.<br><br>   * [Serverless Java Flink](https://docs.byteplus.com/docs/dataleap/serverless_java_flink)：Hosting and operations for Serverless Java Flink native tasks. |
   

* **ByteHouse CE Engine**

   
   |Engine Classification |Supported task types |
   |---|---|
   |ByteHouse CE Engine |Batch Data:<br><br>[ByteHouse CE SQL](https://docs.byteplus.com/docs/dataleap/bytehouse_ce_sql)Processing ByteHouse CE data through ByteHouse CE SQL statements. |
   

* **ByteHouse CDW Engine**

   
   |Engine Classification |Supported task types |
   |---|---|
   |ByteHouse CDW Engine |Batch Data:<br><br>[ByteHouse CDW SQL](https://docs.byteplus.com/docs/dataleap/bytehouse_cdw_sql)Process ByteHouse CDW data with ByteHouse CDW SQL. |
   

* **Generic**

   
   |Engine Classification |Supported Task Types |
   |---|---|
   |Generic |* [Python](https://docs.byteplus.com/docs/dataleap/python)Perform data analysis using Python syntax.<br><br>* [Shell](https://docs.byteplus.com/docs/dataleap/shell)Meet Shell development business scenarios and implement data development using Shell syntax. |
   


<span id="_3-2-2-数据集成类节点"></span>
#### 2.2.2 Data Integration Nodes

Providing a stable and efficient data synchronization platform, committed to offering fast and reliable synchronization capabilities between diverse data sources.


* Single\-channel task nodes for data integration now support batch integration and streaming integration:

   * [Batch data synchronization](https://docs.byteplus.com/docs/dataleap/batch_data_synchronization): Offline (Batch) Data Synchronization involves defining data sources for both the origin and destination to achieve data transmission between heterogeneous data sources.

   * [Streaming data synchronization](https://docs.byteplus.com/docs/dataleap/streaming_data_synchronization): Real\-time synchronization supports reading data from databases like Kafka, MySQL, BMQ, and others to target databases such as Hive, HDFS, LAS, Doris, CFS, etc., maintaining real\-time data correspondence between the source and target databases.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In data integration tasks, EMR clusters involving Hive, HDFS, Doris, StarRocks data sources, currently support cluster versions other than EMR\-2.X.   </div>
   

* DataSail supports real\-time whole database synchronization, real\-time sub\-database sub\-table, batch whole database synchronization, and real\-time data collection solutions:

   * [Real-time full database synchronization (new version)](https://docs.byteplus.com/docs/dataleap/69148): The one\-click real\-time whole database synchronization solution supports integrated full\-incremental data synchronization between various data sources, where initially the entire source data is migrated via a batch task and then incremental data is collected through real\-time synchronization tasks to the target data source.

   * [Real-time database and table sharding (new version)](https://docs.byteplus.com/docs/dataleap/69139): The one\-click real\-time sub\-database sub\-table solution supports synchronizing multiple sub\-table data from multiple databases under multiple instances with the same Schema to a single table at the target end.

   * [Offline full database synchronization (new version)](https://docs.byteplus.com/docs/dataleap/69144): The batch whole database synchronization solution allows periodic and one\-time synchronization of entire database table data to the target end, including types like batch whole database synchronization (one\-time full), batch whole database synchronization (periodic full), batch whole database synchronization (one\-time incremental), batch whole database synchronization (periodic incremental),and batch whole database synchronization (one\-time full periodic incremental).

   * [Real-time data collection plan (new version)](https://docs.byteplus.com/docs/dataleap/69108): The real\-time data collection solution supports real\-time collection of incremental data from the source database to the message queue; it is advisable to first perform a data caching intermediate step when the incremental data is large or has peaks and troughs.


See details for supported datasource types:[Supported data sources](https://docs.byteplus.com/docs/dataleap/supported_data_sources)

<span id="_3-2-3-交互式分析节点"></span>
#### 2.2.3 Interactive analysis node

[Notebook](https://docs.byteplus.com/docs/dataleap/notebook)Provides an interactive development environment for user data development and data exploration scenarios. Supports data and algorithm development using Python, Markdown languages, and third\-party libraries.

<span id="_3-3-调度设置"></span>
### 2.3 Schedule Settings

After setting the task type, you need to configure the relevant attributes for scheduling the task to run. The DataLeap platform offers scheduling options by minute, hour, day, week, and month. See details[Basic Task Attributes](https://docs.byteplus.com/docs/dataleap/basic_attribute_of_task).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b094f2a5b2364bf3bfa3f7818123ded7~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-任务操作栏说明"></span>
### 2.4 Task Action Bar Explanation

In the task action bar, you can perform the following actions:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For different task types, the action bar features vary, subject to the interface display.</div>


The following example uses a ByteHouse CDW SQL task:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22a5de4ab5e84fde97dbe182f4b934ca~tplv-goo7wpa0wc-image.image) </span>


|No. |Action |Description |
|---|---|---|
|1 |Save |Perform the save action for the current node, saving the current node's code and related configuration. |
|2 |Run/Terminate |Run or terminate the current node's code. When running SQL code, it supports running selected parts of the code. |
|3 |Lock |Lock the task, which can be locked by the current task editor. Other collaborators need to click "unlock" before editing the code. |
|4 |Save and Submit |Submit the task for deployment to the operations production environment for scheduled execution. See details below on submitting for deployment. |
|5 |Format |Based on the [Personalize settings](https://docs.byteplus.com/docs/undefined/682aa7e55df38404fda1396d) SQL formatting style settings, format the written code to make its syntactic structure clean and clear.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This capability is not available yet, please stay tuned.</div><br> |
|6 |Parse |Parse and check the syntactical and semantic correctness of the written SQL code, inspect syntax errors before running to prevent runtime issues. |
|9 |Execution Engine |Different task types of engines have different execution engines. |
|10 |Parameter description |The platform provides descriptions of variable parameters and the rules for parameter operations. See details [Description of platform time variables and constants](https://docs.byteplus.com/docs/undefined/689d96727654f3051453d252). |


<span id="_4-流水线管理"></span>
## 3 Pipeline Management

Different business scenarios have different requirements. Combining business requirements, DataLeap supports the development of pipelines aimed at overall task processes. For example, in the submission scenario, different business sides hope that pre\-launch check items vary, so it's possible to use pipeline capabilities to integrate submission jobs into pipeline checks by hitting trigger conditions, thereby realizing different business side scenario checks for different contents.

Pipelines can complete manual checkpoints, execute releases, trigger debugging, selectors, and CodeCT verification steps in an automated way, achieving continuous and efficient data delivery. In the pipeline, you can add multiple node processes, which are the extensions provided in the Smart Markets, to overall control the data development process.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Pipeline requires the tenant’s main Account Or Project Administrator to first create the corresponding pipelines in the <strong>Project Console \> Pipeline Management</strong>, see details <a href="https://docs.byteplus.com/docs/dataleap/pipeline_configuration">Pipeline Configuration</a>.</div>


After the pipeline is created, hitting the corresponding trigger actions during the data development process will activate the pipeline. Trigger events currently support **debugging, submission, and release** as trigger events.

<span id="_4-1-调试、提交触发"></span>
### 3.1 Debugging, Submission Trigger

Click the **debug** or **submit for deploy** button in the task toolbar. If the task is within the range of pipeline\-trigger subjects and the trigger events are **task debugging** or **task submission**, then the pipeline will trigger. You can see the notification of pipeline activation at the top right of the interface and view pipeline records below.


1. Click the "View details" button in the pipeline trigger recording to view the configuration of the current pipeline's internal processes.

2. In the pipeline details interface, you can perform the following actions:

   * Plugin details: Click on each node plugin in the pipeline process configuration to view its execution details, input, output, and other information.

   * Approve/Reject: For plugins with manual breakpoints associated with appointed reviewers, you can click the "Approve/Reject" button based on actual conditions to carry out the pipeline's flow operations.

   * Terminate: If the pipeline's execution time is too long, you can click the "Terminate" button on the plugin to terminate the pipeline. After termination, the pipeline status will be set to Failed.

   * Set to "Success": If the pipeline fails due to some reason, you can click the "Set to "Success"" button in the plugin node to mark the pipeline as successful, allowing the failed pipeline to continue executing.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Whether the plugin node allows the "<strong>Set to "Success"</strong>" action, go to the <strong>Pipeline \> Process Configuration \> Extension Configuration \> Operations Configuration</strong> interface and select "<strong>Allow set success</strong>" before proceeding with the operation. For operation details, see <a href="https://docs.byteplus.com/docs/dataleap/pipeline_configuration">Pipeline Configuration</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For branch plugin nodes after the <strong>selector</strong> extension, branches in the "Skip" state cannot be terminated or set to succeed.   </div>
   


<span id="_4-2-发布触发"></span>
### 3.2 Commit for Deploy

In the project console, pipelines triggered by the deploy package release event have been created, and the deployed tasks fall within the scope of the pipeline trigger objects. When the deployment center creates a deploy package or selects "Commit and Release" in the task submission interface, the pipeline will be triggered. You can enter the **Publish Center \> Package management** interface to view the pipeline progress.

Click the **Pipeline Status Details** button to view the configuration of the pipeline's internal processes in the popup window.

<span id="_5-提交上线"></span>
## 4 Commit for Deploy

After editing and saving the task, click the **Commit for Deploy** button in the action bar. In the pop\-up window, complete the following **Commit for Deploy** content configuration and then click the **Confirm** button to submit the job.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">During the submission for activation Or Posting, if the pipeline management is triggered, you need to ensure that the pipeline runs successfully before the task can truly be committed to the Operations Center.</div>


<span id="_5-1-离线任务提交"></span>
### 4.1 Submit Batch Task


|Parameters |Description |
|---|---|
|Backfill data |When committing for deployment, whether to rerun historical data, this action only backfills the current task itself.<br><br><br>* No: Do not backfill<br><br>* Yes: Rerun historical data is required<br><br>   * Backfill business time: Choose the start and end time for the backfill business.<br><br>   * Max parallelism: Set the maximum number of parallel instances. In this backfill operation, which includes all instances, the number of instances that can run simultaneously should be set to 1 for tasks using dynamic partition.<br><br>   * Generated instance state:<br><br>      * Get real execution results after running<br><br>      * Set to "Success"<br><br>      * Set to "failed"<br><br>   * Dependency check:<br><br>      * Follow the dependency settings and start execution when the upstream task is complete<br><br>      * Ignore upstream dependencies and execute immediately<br><br>   * Specify a schedulable time period: After specifying the running period, all backfill instances generated in this backfill operation will be executed during that period.<br><br>      Beijing time: specify time period, such as:<br><br>      * If the time is set to 06:00 to 22:00, the backfill instances will be executed from 6 AM to 10 PM on the current day.<br><br>      * If the time is set to 22:00 to 06:00, the backfill instances will be executed from 10 PM on the current day to 6 AM the next day.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">"00:00 to 08:00" is the peak period for core task execution. To avoid the impact of backfill/rerun on routine operations and global incidents, it is advised to activate this setting and avoid this period.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">"Scheduling" is not equivalent to "execution". The system is only responsible for submitting the corresponding instances to the engine for scheduling. The engine decides whether to execute them.   </div><br>    |
|Monitor Settings |* Default monitoring rules:<br><br>   * Currently, the default monitoring rules are provided by the system and cannot be modified by users.<br><br>   * Default monitoring rules:<br><br>      * Ordinary Batch task: If the task still fails after retry attempts, an alarm is sent to the task owner via email and only sent once.<br><br>      * Near\-real\-time task: If the task fails three consecutive times, an alarm is sent to the task owner via email and is only sent once.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Default monitoring rules, you need to activate the <strong>Default Monitoring Rules</strong> button when creating a project, before you can choose it when committing tasks. See details <a href="https://docs.byteplus.com/docs/dataleap/create_project">Create a Project</a>.   </div><br>   <br><br>* Custom Monitoring Rules:<br><br>   * Select applicable rules from the monitoring rules created in the project to monitor the task execution.<br><br>   * Multiple monitoring rules can be selected to monitor the task execution.<br><br>      Monitoring rule creation, for details see [Monitoring rules](https://docs.byteplus.com/docs/dataleap/monitor_rules)<br><br>   * Baseline monitoring rules:<br><br>      * Select a suitable baseline from the established baselines in the project, and monitor this task along with all its upstream tasks.<br><br>      * A task allows only one baseline to be added.<br><br>         Baseline monitoring creation, for details see: [Baseline management](https://docs.byteplus.com/docs/undefined/689b106ca5abd9051f272182) |
|Submit Settings |* Submit Settings<br><br>   * Commit Only: Tasks are only committed; for posting, proceed to **Publish Center** to release.<br><br>   * Commit and Release: Submit and directly post tasks to the Operations Center.<br><br>   * Reviewer: When configuring a review strategy under the project, a reviewer must be selected, see details for the review configuration [Configuration Review Strategy](https://docs.byteplus.com/docs/dataleap/release_review_strategy).<br><br>* Submission description: Enter the submission note for easy version management later on. |


<span id="_5-2-流式任务提交"></span>
### 4.2 Submit Streaming Task


|Parameters |Description |
|---|---|
|Online Check |* Configuration check: Check the basic configuration, Streaming SQL, PB (if PB data types are involved in the task), and other configurations.<br><br>* Lineage check:<br><br>   * Data source registration check: To ensure subsequent data source monitoring can be added, task lineage must be completely filled out.<br><br>   * Data source registration information integrity check: Check whether the data source's registration information is completely filled out. After passing the lineage check, proceed directly to the online submission settings.<br><br>* Resource check: Check the upper and lower resource configuration limits for the Flink task. |
|Commit Settings |* Commit Settings:<br><br>   * Commit Only: Tasks are only committed, to post, please go to **Publish Center** to perform the posting.<br><br>   * Commit and Release: Submit and directly release tasks to the Operations Center.<br><br>   * Reviewer: Visible when configuring the review strategy under a project, it is required to select review personnel, see details at [Configuration Review Strategy](https://docs.byteplus.com/docs/dataleap/release_review_strategy).<br><br>* Submission Description: Enter this submission description for subsequent version management. |
|Start Settings |* After the streaming task goes online, does it start running directly?<br><br>* Restart Mode: The streaming computing Flink Edition and EMR streaming task types support setting these three restart modes.<br><br>   * Restart with the latest state: Restart using the most recent available snapshot of the Streaming task.<br><br>   * Restart with historical snapshots: If historical snapshots are saved for the current task, you can choose the saved snapshot information to restart. For snapshot operations, see details [Operations and maintenance of tasks](https://docs.byteplus.com/docs/undefined/689b13f8a8453604ecb6069e).<br><br>   * Stateless restart: Restart without using snapshot information.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In Flink operation parameters for streaming tasks, it is required to add the "execution.checkpointing.interval" parameter to set the time interval for task checkpoints. When a task restarts in the "Restart with latest state" mode, it can check and restart with the latest state.\*\*\*\* If this parameter is not set, the task will start anew without checking the saved latest state.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Restart configuration for EMR streaming task types (EMR Flink SQL, EMR Java Flink) is currently available on an allowlist basis. You need to <a href="https://console.byteplus.com/workorder/create">submit a ticket</a>, consult DataLeap and EMR support personnel, and obtain approval to use it.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">EMR streaming task types (EMR Flink SQL, EMR Java Flink) currently do not support the manual creation of snapshots, so they cannot use the "Restart with historical snapshot" mode.   </div><br>    |


<span id="_6-发布中心"></span>
## 5 Publish Center

The main goal of the Publish Center module is to improve data research and development efficiency, standardize the task release process, distinguish between development and production environments, enhance production safety and stability, and build a complete data warehouse research and development capability.

If you choose **Commit Only** when committing for deployment, you need to enter the **Publish Center** and perform operations such as [To be published](https://docs.byteplus.com/docs/undefined/682aa7eae5760f053010d166) and [Package Management](https://docs.byteplus.com/docs/undefined/682aa9151fc42b04fb08d9e4).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f93db3c4fbb4c40a8ba6cc17d01abc2~tplv-goo7wpa0wc-image.image) </span>

<span id="_7-运维查看"></span>
## 6 View Operations

After successfully releasing the task submission, you can go to the **Operations Center** to check the task operations. In the top navigation bar, enter Batch Task Maintenance and Stream Task Maintenance. You can monitor the task situation as needed in operations, set monitoring alarms, start tasks, stop tasks, and view run logs among other operations activities.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e89de49bef6f4d3380784518912f2cd5~tplv-goo7wpa0wc-image.image) </span>

See details：[Task Operation](https://docs.byteplus.com/docs/dataleap/task_operation)、[Operations and maintenance of tasks](https://docs.byteplus.com/docs/undefined/689b13f8a8453604ecb6069e)。
