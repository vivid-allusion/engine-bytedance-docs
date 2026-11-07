---
title: "Create Offline Tasks"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Create_Offline_Tasks"
---

Task creation refers to the process of creating a visual modeling task, which typically includes steps such as creating a new task and establishing data connections. This article introduces the general process for task creation.

<span id="_1-功能概述"></span>
# Feature overview

Visual modeling tasks support extracting data from data sources, adding data processing nodes by dragging and dropping, and outputting the processed data to the target source.


* Task type: Offline task

* Supported input data sources for offline tasks: Hive, MySQL, ClickHouse, Kafka, HttpAPI, Feishu, CSV/Excel, Oracle, Impala, PostgreSQL, Hbase, SQLServer, MaxCompute, ADB, MongoDB, Hana, Teradata, Db2, Vertica, GreenPlum, and more than 20 mainstream data sources

* Supported data cleansing nodes: field settings, row filtering, adding calculated columns, aggregation, join, merge, row\-column transposition, and more

* Supported AI modeling capabilities: operators for featured areas, feature engineering, machine learning, natural language processing, and more

* Supported output built\-in data sources: datasets stored in Hive, ClickHouse, and ByteHouse


<span id="d56da9c2"></span>
# Usage restrictions

The trading calendar and multiple synchronization features in Save Task \- Run Type \- Run Frequency are currently only supported in on\-premises deployment version V2.83.0 and above. To enable this feature, please contact the Volcano Engine product team.

<span id="_2-1-新建任务"></span>
# Create a new task

After entering "Visual Modeling", click "Task List" — "New" — "Create Offline Task" to navigate to the task creation page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/344fd8e4705741bda7d30885f071b59d~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-数据连接"></span>
# Data connection

On the new task page, click the plus sign in the upper left to add a data connection. You can choose to add various types of data connections, and the platform supports custom SQL for most offline storage types.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c5326201d8b4a9f83f7c78fb640be5a~tplv-goo7wpa0wc-image.image) </span>

If a dataset is selected, the following will be loaded in the left canvas: custom SQL (displayed for offline tasks), visual modeling datasets, intelligent data insight datasets, and customer data platform datasets (if the product is also purchased and deployed).


* **Hive**/**ClickHouse** custom SQL:

   * Hive: When the visual modeling output is stored as a Hive\-type dataset, you can write SQL as long as it complies with Hive syntax.

   * ClickHouse: Visual modeling output with data stored as a ClickHouse dataset. You can write SQL as long as it complies with ClickHouse syntax.

* **Visual modeling dataset**: The dataset output from visual modeling, regardless of whether the output storage type is Hive or ClickHouse.

* **Intelligent data insight dataset**: The dataset output built through the "Dataset" module.

* **Customer data platform dataset**: If the customer data platform is also purchased and deployed, this type of dataset can be used here.


In the data connection list on the visual modeling task creation page, click the delete button to the right of a specific data connection to remove the data connection.

<span id="_2-4-处理节点"></span>
# Processing node

Add and configure processing nodes by clicking the plus sign on the right side of a node. Drag a line from the plus sign on the right side of the previous node to the origin on the left side of the next node to configure the node flow relationship. After clicking "Apply", you can expand to preview the processed data results.

As shown in the figure below, click the output plus sign of the input data operator block to expand six types of operation nodes: output, data cleansing, featured operator zone, AI\-feature engineering, AI\-machine learning, and AI\-natural language. Click one of the categories to see the available operators.

Operator refers to a data processing node.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3262d6947be74556b018601b09afb779~tplv-goo7wpa0wc-image.image" width="610px" /></div>


**Description of common operators**


* [Data Output](https://docs.byteplus.com/docs/DataWind/109994): Indicates that after the canvas flow is executed, data is output to the specified location and the task execution logic is configured.

* [Data Cleaning](https://docs.byteplus.com/docs/DataWind/110020): Mainly responsible for model building (such as multi\-table joins and merges), field format conversion (such as field settings, pivoting rows to columns, and columns to rows), data computation (such as calculated fields, aggregation, top K values), and data filtering (such as deduplication and sampling).

* Featured operator zone: Includes large model operators such as Volcano Ark large models.

* [Feature Engineering](https://docs.byteplus.com/docs/DataWind/110014)/[Machine Learning](https://docs.byteplus.com/docs/DataWind/109990): Represents AI algorithm capabilities such as principal component analysis, feature importance, clustering, classification, and regression.

* [Natural Language Processing](https://docs.byteplus.com/docs/DataWind/109983): Represents NLP natural language processing capabilities. For tokenization and stop word removal, open\-source word packages are used.

> * Feature engineering, machine learning, and natural language processing operators can only be used in conjunction with the "Prediction" operator.


Operators are visible not only on the canvas, but you can also click "Operator" in the left tab bar to select from the available operators. The way each operator and model is applied differs. Detailed explanations are provided in the corresponding operator documentation; this article focuses only on the main process for creating a task.

In practice, visual modeling operators support adding text descriptions, helping users better understand the notes for the current operator.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/533248ad853f4718a4c0867db4e4ff37~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64b8844a635a49b39688347293d5a12d~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The visual modeling task creation page allows you to switch between free layout and grid layout, making it easy to adjust the layout of each node in the task.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2cc798d2fcdc46cfafe54d35ec7bf7ec~tplv-goo7wpa0wc-image.image) </span>

On the visual modeling new task page, all abnormal nodes in the task are displayed together to help troubleshoot task issues.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49d8657159b443139a5267acafdd0265~tplv-goo7wpa0wc-image.image) </span>

The visual modeling task creation page also allows you to delete operators by pressing the delete key, improving data cleansing efficiency.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ba030ce8b714eca88514a05995d4a0c~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-5-数据预览"></span>
# Preview data

<span id="_2-5-1-查看预览"></span>
## View preview


1. On the editing page of a visual modeling task, after selecting a data connection, you can conveniently preview the data. You can preview **detailed data, table structure, and data exploration**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74255d1dced24f3480c835c4b3eee415~tplv-goo7wpa0wc-image.image) </span>


* You can set whether to expand the data preview panel for the current type of operator by default, and whether to apply this setting to all operators, to suit different user preferences.

* The preview panels for "data exploration" and "detailed data" are merged to provide centralized information display, simplify operations, and make features easier to use.

2. Click the  **"▼" button** for each column of data to quickly select an operator for data processing. As shown in the figure below:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93c657b4ad344505a9951df5eed03533~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-5-2-采纳建议"></span>
## Apply suggestions

In the preview, data cleansing suggestions are provided. Users can click to apply a suggestion with one click, improving the efficiency of data cleansing.

<span id="_2-5-3-即时设置"></span>
## Instant settings

On the editing page of a visual modeling task, when the data preview is open, you can instantly edit or set preview options in the lower left corner of the preview interface. Users can configure the amount of data involved in the preview calculation (by default, no more than 1,000,000 rows). You can specify a custom number of rows or select all data. After configuration, the preview will be refreshed in real time. As shown in the following figure:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1887239e5ca84cc9ae9da75d260097e2~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-6-节点执行"></span>
# Execution node

In the configuration, you can select a node and run it to verify execution. Caution: When an upstream node is changed, you must rerun the upstream node before you can execute the current and downstream nodes.


* Run this node: Runs the current node. All upstream nodes must have been executed.

* Execute up to this point: Sequentially runs any upstream nodes that have not been executed and the current node.

* Execute from this node: Sequentially runs the current node and subsequent nodes. All upstream nodes must have been executed. Typically used after modifying the current node.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2df519e64bdd42f5b2d1d41b74fcbef2~tplv-goo7wpa0wc-image.image) </span>

After a node is executed, a green check mark will appear next to the node, indicating that the node has been executed.

<span id="_2-7-输出数据集"></span>
# Output dataset

Add an output node and choose to output to an existing dataset or create a new dataset. For detailed settings of the output dataset, see [Data Output](https://docs.byteplus.com/docs/DataWind/109994).

> The following are now supported [Data Output](https://docs.byteplus.com/docs/DataWind/109994): datasets stored in Hive, ClickHouse, or ByteHouse.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53cc3a65cdad4e45bc14223c55ac79fe~tplv-goo7wpa0wc-image.image) </span>

<span id="692601af"></span>
# Save task


1. After building the visual modeling task, you can click "Test run" to verify the execution result.

2. After a successful test, you can open the "Edit task information" dialog to set the task name, description, path, and execution type.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6fb40c4f1b2a4e3ab11a0373f3436d2a~tplv-goo7wpa0wc-image.image) </span>

The parameter configuration instructions are as follows:


|Parameters |Configuration description |
|---|---|
|Name |Visualization modeling task name |
|Description |Description of the visualization modeling task, which may include information such as task objectives, task content, and more. |
|Path |You can choose to save it to a specific task list folder for future reference. |
|Run type |The task run schedule can be configured.<br><br><br>* Manual run: The system will not run automatically. Users must manually select the task in the task list and click "Run".<br><br>* Scheduled run: The system automatically runs the visualization modeling task according to the configured schedule, without requiring manual execution by the user. |


Scheduled run—run frequency provides two configuration methods, as described below:


|Exact time |Interval duration |
|---|---|
|* Includes hourly, daily, daily (based on trading calendar), daily (the day after the trading calendar), weekly, and monthly.<br><br>* Multiple times can be set. When multiple times are selected, the scheduler will execute multiple times. For example, if 9:00 and 10:00 are set for each day, the task will run twice daily.<br><br>* For daily (based on trading calendar) and daily (the day after the trading calendar), selecting the trading calendar type is supported. For trading calendar settings, see **Volcano Engine "System Configuration" \- "Enterprise Calendar" \- "Tag Management"** . |* Execution every 10, 20, or 30 minutes is supported.<br><br>* It is possible to set the effective time for each day, which must include both a start time and an end time. If left blank, the effective time is all day.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Full synchronization or large\-volume synchronization using minute\-level synchronization will consume a large amount of resources and result in poor performance. Please use as needed.</div><br> |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">After modifying the run frequency, check whether the output\-dependency configuration (such as dependency information) needs to be updated accordingly.</div>


* <div data-tips="true" data-tips-type="warning">The trading calendar and multiple synchronization features in Save Task \- Run Type \- Run Frequency are currently supported only in on\-premises deployment products version V2.83.0 and above. To enable this feature, contact the Volcano Engine product team.</div>


3. When the model configuration is complete, you can click "Save" or "Save as" in the upper right corner. If the model is not complete, you can also set the run frequency to manual run and then click "Save" or "Save as".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/741648a3c596449ca73efde5c5c3d90e~tplv-goo7wpa0wc-image.image) </span>


4. After saving the task configuration, click "Return" in the upper left corner to go to the task details page.

5. Return to the visual modeling page and click "Run records" for the current task to manually run it. For more task management capabilities, see [Task Management](https://docs.byteplus.com/docs/DataWind/109973).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/78f43644b9004a59aaf3ce0a8b85755f~tplv-goo7wpa0wc-image.image) </span>

<span id="ef695a0a"></span>
# Download data

On the dataset details and data preview pages, click "Download" to download the data. The supported data formats are CSV and Excel. The number of data records includes several preset options: 100, 500, 1000, 5000, and the current previewed data. Custom record counts are also supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/214ebba5eda948b6bff2b0ddba32e9f4~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, the visual modeling module only provides offline tasks. To use real\-time tasks, the data source supports Kafka. (The real\-time task feature requires purchasing the DataWind on\-premises version, Customer Data Platform (CDP), and Kafka. To use this feature, please contact your company's sales representative or customer success manager for purchase information.)</div>
