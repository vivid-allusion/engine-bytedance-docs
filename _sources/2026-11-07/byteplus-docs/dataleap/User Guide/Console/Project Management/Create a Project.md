---
title: "Create a Project"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/create_project"
---

DataLeap divides and manages tasks by project. This article will introduce you to how to create a new project.

<span id="28a26f92"></span>
## Constraints


* Only the main tenant account or IAM sub\-accounts with **DataLeapFullAccess** permission can create projects. For detailed information about accounts, please see [Account authorization](https://docs.byteplus.com/docs/undefined/689ae8792450980504c8cbdb).

* If a sub\-account binds ByteHouseCE engine service, it must have **ByteHouseCEStandardAccess** permission and added authority to bind the cluster for binding to be successful. For instructions related to adding permissions, please refer to [ByteHouse CE SQL](https://docs.byteplus.com/docs/dataleap/bytehouse_ce_sql).


<span id="_2-前提条件"></span>
## Prerequisites

The required engine must be activated, and a cluster or instance must have been created on the engine side.


* Serverless Flink engine project and resource pool have been created. For details, see [Import Project](https://docs.byteplus.com/en/docs/flink/Import_Project_From_BytePlus) and [Create VCI Resource Pool](https://docs.byteplus.com/en/docs/flink/Create_VCI_resource_pool).

* ByteHouse CE cluster created. For details, refer to [Create a Cluster](https://docs.byteplus.com/en/docs/bytehouse/create-a-cluster).

* ByteHouse Cloud Data Warehouse Edition service instance created. For details, refer to [Manage Environment](https://docs.byteplus.com/en/docs/bytehouse/manage-environment) and [Create/Edit virtual warehouse](https://docs.byteplus.com/en/docs/bytehouse/create-edit-virtual-warehouse) of ByteHouse Cloud Data Warehouse Edition.


<span id="_3-操作步骤"></span>
## Operation Steps


1. Log into the DataLeap console.

2. Click on **Projects** in the left navigation bar to enter the project management page.

3. From the top of the page, select the BytePlus project to which the project should be categorized from the **All resources** dropdown.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c884b3b5af0f432088c60e23d2d404a6~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If not selected, it will be classified under <strong>default(Default project)</strong> by default.   </div>
   

4. Click the **Create Project** button to enter the **Create Project** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c6421eacf7d45dc8f564897862a24cc~tplv-goo7wpa0wc-image.image) </span>

5. See [Parameter Description](https://docs.byteplus.com/docs/dataleap/create_project#ac72063e) After setting the following project configuration information, click the **Create now** button to complete the project creation.

   * Basic Information

   * Project Control

   * Service Binding


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also create a project through the <strong>Create Project</strong> button on the overview page.</div>


<span id="ac72063e"></span>
## Parameter Description

<span id="11164498"></span>
### Configure Basic Information

The parameters related to basic information are listed in the table below. Parameters marked with an \* are required, and those without an \* are optional.


|Parameters |Description |
|---|---|
|\*Current Region |The region information currently belongs to the DataLeap service, by default it is the region selected at the time of activating the DataLeap service, and cannot be edited here.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If multiple regions are activated, you can select the region closest to your business through the dropdown in the top navigation bar of the page.</div><br> |
|\*Project Name |Name the project as needed.<br><br>Only consist of Chinese characters, letters, numbers, underscores, or special characters such as ., [], 【】, ( ), (). |
|\*Project Type |Divided into public and private.<br><br><br>* Public: As long as you are a tenant member, you can enter the project and view the task information under the project.<br><br>* Private: Only members under a specific project can enter the project and view the task information under the project. |
|\*Project Mode |Currently only **Simple mode** is available. |
|\*Owner |Tenant main account, cannot be modified. |
|\*Project description |Description about the project. |
|Project account number |If tasks under the project require unified account submission for authentication, the tenant's main account/a sub\-account under the tenant can be set as the project account.<br><br>Configure the project account and when **Authentication Configuration \> Production Environment** is enabled below, different tasks will have different permission verification scenarios:<br><br><br>* For development task types like SQL, Shell, Python, the Operations Center will use the project account to submit the tasks and authenticate;<br><br>* Data Integration task type:<br><br>   * If user information is configured in the data integration source, it will use this configured user information for authentication access.<br><br>   * If the data source is not configured with user information, the operations center will use the configured project account to submit the task and perform authentication when executed. |
|BytePlus Project |This DataLeap project belongs to the current selected BytePlus project and cannot be edited here. To select a different project, use the dropdown in the top navigation bar.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">BytePlus Project is managed through <strong>Access control</strong> system. This project management is a type of resource management provided by BytePlus, allowing you to group and manage cloud resources used by different businesses or projects. To modify the project to which resources belong, please go to <strong>Access control</strong>'s <a href="https://console.byteplus.com/iam/resourcemanage/project">Project Management</a>.</div><br> |


<span id="e95d9312"></span>
### Configure Project Control Information

The parameters related to project control are listed in the table below.


|Parameters |Description |
|---|---|
|\*Authentication Configuration |Settings for the authentication account in development and production environments.<br><br><br>* Not configured project account: Development and production environment authentication, only **User account** can be used.<br><br>* Configured project account: Production environment authentication; you can choose to use either **User account** or **Project account.** <br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For development environment authentication, the <strong>User account</strong> is used by default.</div><br> |
|\*Project Backfill Control |Users without edit permissions can backfill tasks under the project from upstream and decide if approval is required.<br><br><br>* Direct execution: Users without edit permissions can directly generate and execute a backfill instance for tasks under the project upstream.<br><br>* Execute after approval: Users without edit permissions can generate and execute a backfill instance for tasks under this project from upstream, but only after the task owner or project administrator approves it. |
|\*Default for task dependence |Default configuration method for task dependency relationships when deciding task scheduling settings under a project. Supports **specify offset dependency** and **proximity dependence** options, with **specify offset dependency** selected by default.<br><br><br>* Specify offset dependency: When dependencies have different scheduling frequencies or scheduling dates show deviations, a manual setting of the offset is required.<br><br>* Proximity dependence: When downstream instances look for upstream dependencies, they follow proximity principles, depending on the upstream instance that is closest in time to its scheduled run time (equal to or earlier than the timing of this instance). |
|Project maximum parallelism |The maximum number of tasks that can run concurrently within the project ranges from 1 to 5000 integers. The maximum parallelism of the project should be greater than or equal to the max rerun parallelism.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Since we currently use a public scheduling resource group, the maximum parallelism for a single tenant is 100, meaning the maximum parallelism limit for each project under a tenant is 100.</div><br> |
|Maximum parallelism of rerun |The maximum number of concurrent task reruns is set between 1 and 5000. The max rerun parallelism should be less than or equal to the project's max parallelism.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The max rerun parallelism for projects at this stage also has an upper limit of 100.</div><br> |
|Default monitoring rules |The system provides basic monitor rules. If a task continues to fail after retries, an alarm will be sent to the task owner via email, only once.<br><br>If enabled, monitoring rules will be automatically applied when tasks in the project are deployed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Default monitoring rules are provided by the system and cannot be modified by the users.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When deploying a task, either before or after, you can choose whether to use the default monitoring rules.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If a selected task includes the Kafka2HDFS task, the default monitoring rules do not apply to this task type.</div><br> |
|Data security settings |Security settings related to query data results in the project.<br><br><br>* Task query results show maximum records: The maximum number of records that can be displayed from the task query results. The settings can be adjusted, with a range from 1 to 10000 as integers.<br><br>* Select query result settings: Options to enable or disable downloading and copying of query results. |
|Message notification settings |You can select under which conditions to send notification messages. The following options are supported and can be selected multiple times.<br><br><br>* Temporary query ran successfully<br><br>* Temporary query failed to run<br><br>* The practice ran successfully<br><br>* Task practice run failed |


<span id="54f5e209"></span>
### Configure Service Binding Information

The parameters related to the service binding information are as described in the table below.


|Parameters |Description |
|---|---|
|Computing resource group |Used for executing tasks such as Notebook, Python, Shell, etc.<br><br>Supports options for both common computing resource groups and exclusive computing resource groups. Dropdown to select **Running** resource groups, with the ability to set multiple groups.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you choose the <strong>Exclusive computing resource group</strong>, you can only select resource groups that belong to the <strong>current BytePlus project</strong>.</div><br> |
|\*Scheduling resource group |Supports public scheduling resource groups and exclusive scheduling resource groups. Allows selection of **Running** resource groups from a dropdown menu and the setting of multiple groups.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you choose the <strong>Exclusive scheduling resource group</strong>, you can only select resource groups that belong to the <strong>current BytePlus project</strong>.</div><br> |
|Integration resource group |Allows binding to activated data integration resource groups, with the option to select **Running** resource groups from a dropdown menu and set multiple groups.<br><br>If the required option is not available, click **Go Create** to jump to the exclusive resource group management page and create a new group.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can only select resource groups that belong to the <strong>current BytePlus project</strong> for data integration.</div><br> |
|Engines |Displays a list of connected engines, including EMR Serverless Spark, Stream Computing Flink Edition, etc., and can be bound as needed. If the engine is not activated, click **Go Buy** to jump to the appropriate page to purchase and then bind.<br><br><br>* EMR Serverless Spark: This is a serverless\-based Spark service that can read and write Serverless Hive tables, and supports Spark SQL and Spark Jar to meet the differentiated demands of medium and large customers for resources in different states. Settings include **Service instance** and **Resource queue**.<br><br>   * Service instance: Dropdown to select the running default instance **serverless_spark_default**.<br><br>   * Resource queue: Under the service instance, resource queues have been created. They are selectable via dropdown and support binding to multiple.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">A queue can contain multiple different computation groups, supported by selecting according to computation group.      </div><br>      <br><br>* EMR Serverless Presto: This is a serverless\-based Presto service that reads and writes Serverless Hive tables and provides interactive SQL queries. Settings include **Service instance** and **Resource queue**.<br><br>   * Service Instance: You can select the running default instance **serverless_presto_default** from the dropdown menu.<br><br>   * Resource Queue: You can select from the calculation groups of resource queues that have been created under the service instance, supporting the binding of multiple queues.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">A queue can contain multiple different computation groups, supported by selecting according to computation group.      </div><br>      <br><br>* ByteHouse CE: It's an enterprise\-grade analytical database built on open\-source ClickHouse, supporting interactive analysis of PB\-scale data through various proprietary table engines, flexible for various data analysis and applications. Settings include **ByteHouse CE clusters**, from which you can select the created clusters and support binding multiple ones.<br><br>* ByteHouse CDW: A self\-service data analysis platform that supports both real\-time and batch data import, capable of efficiently analyzing PB\-scale massive data. Settings include **service instances** and **calculation groups**, and support configuring multiple settings.<br><br>   * Service Instance: You can select from active instances dropdown.<br><br>   * Calculation Group: Calculation groups created under the service instance; you can select from the dropdown and bind multiple ones.<br><br>* Serverless Flink: An enterprise\-level, fully\-managed stream computing platform, supporting out\-of\-the\-box operation, extreme Serverless elasticity, simple SQL development, and stream\-batch integration features. Settings include **Engine project** and **Resource pool**.<br><br>   * Engine Project: Refers to projects that have been created on the engine, selectable from a dropdown menu. After binding, tasks under the current project will map to the corresponding engine project.<br><br>   * Resource Pool: You can select from the created resource pools under the engine project and bind multiple ones. |


<span id="f512a6f4"></span>
## Subsequent Operations

After creating a project, you can continue to enhance other configurations such as review configuration, queue management, synchronization settings, and more, and go to **Data Development** page to perform task development activities under this project.
