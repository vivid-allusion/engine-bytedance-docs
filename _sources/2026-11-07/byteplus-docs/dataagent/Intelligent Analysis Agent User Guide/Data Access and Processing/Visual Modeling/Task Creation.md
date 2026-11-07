---
title: "Task Creation"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Task_Creation"
---

<span id="_1-功能概述"></span>
# 1. Function overview

Task creation refers to the process of creating a visual modeling task, which typically includes steps such as creating a new task and connecting to data sources. Visual modeling tasks support extracting data from data sources, adding data processing nodes by dragging and dropping, and outputting the processed data to the target source.


* Task type: offline task

* Supported input data sources for offline tasks: Hive, MySQL, ClickHouse, Kafka, HttpAPI, Feishu, CSV/Excel, Oracle, Impala, PostgreSQL, Hbase, SQLServer, MaxCompute, ADB, MongoDB, Hana, Teradata, Db2, Vertica, GreenPlum, and more than 20 mainstream data sources

* Supported data cleansing nodes: field settings, row filtering, adding calculated columns, aggregation, join, merge, row\-column transpose, and more

* Supported AI modeling capabilities: feature engineering, machine learning, natural language processing, and many other operators

* Supported output built\-in data sources: datasets stored in Hive, ClickHouse, and ByteHouse


<span id="_2-使用说明"></span>
# 2. Instructions for use

<span id="_2-1-新建任务"></span>
## 2.1 Create a task

After clicking into "Visual Modeling", click "Task List" — "Create" — "Create Offline Task" to navigate to the task creation page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24c2a95a9ecb4b4885584b23deb2c6fe~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-数据连接"></span>
## 2.2 Data connection

On the task creation page, click the plus sign in the upper left to add a data connection. You can choose to add various types of data connections, and the platform supports custom SQL for most offline storage types.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/162c5b815ee3407f8628c487a33aaf8e~tplv-goo7wpa0wc-image.image) </span>

**Caution**:

If a dataset is selected, the left canvas will load: custom SQL (displayed for offline tasks), visual modeling datasets, intelligent data insight datasets, and customer data platform datasets (if this product is purchased and deployed). The introduction is as follows:


* **Hive**/**ClickHouse** custom SQL:

   * Hive: Visual modeling outputs and stores data as Hive\-type datasets. You can write SQL, as long as it conforms to Hive syntax.

   * ClickHouse: Visual modeling outputs and stores data as ClickHouse datasets. You can write SQL, as long as it conforms to ClickHouse syntax.

* **Visual modeling dataset**: The dataset output by visual modeling, regardless of whether the output storage type is Hive or ClickHouse

* **Intelligent data insight dataset**: The dataset output built through the "Dataset" module;

* **Customer data platform dataset**: If the customer data platform is purchased and deployed simultaneously, this type of dataset can be used here.

   On the data connection list of the visual modeling task creation page, click the delete button on the right side of a specific data connection to remove the data connection.


<span id="_2-4-处理节点"></span>
## 2.3 Processing nodes

Click the plus sign on the right side of a node to add and configure a processing node. Drag a line from the plus sign on the right side of the previous node to the origin on the left side of the next node to configure the node flow relationship. After clicking "Apply", a preview of the processed data results will be displayed.

As shown in the figure below, click the output plus sign of the input data operator block to expand five types of operation nodes: output, data cleansing, AI feature engineering, AI machine learning, and AI natural language. Click one of these types to view the available operators. Operators are nodes for data processing.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b0f93e87bc34de29e17aaa91864ace8~tplv-goo7wpa0wc-image.image" width="610px" /></div>


**Description of commonly used operators**


* [Data Output](https://docs.byteplus.com/docs/dataagent/Data_Output_): Indicates that after the canvas flow is executed, the data is output to the specified location and the task execution logic is configured.

* [Data Cleaning](https://docs.byteplus.com/docs/dataagent/Data_Cleansing): Mainly responsible for model building (such as multi\-table joins and merges), field format conversion (such as field settings, row\-to\-column, column\-to\-row), data computation (such as calculated fields, aggregation, top K values), and data filtering (such as deduplication and sampling), and more.

* [Feature Engineering](https://docs.byteplus.com/docs/dataagent/Feature_Engineering)/[Machine Learning](https://docs.byteplus.com/docs/dataagent/Machine_Learning): Indicates AI algorithm capabilities such as principal component analysis, feature importance, clustering, classification, regression, and more.

* [Natural Language Processing](https://docs.byteplus.com/docs/dataagent/Natural_Language_Processing): Indicates NLP natural language processing capabilities. For word segmentation and stop word removal, open\-source word packages are used.

> * Feature engineering, machine learning, and natural language processing operators can only be used together with the "prediction" operator.


Operators are visible not only on the canvas, but you can also click "Operators" in the left tab bar to select available operators. Click "AI models" to select available models. The application method for each operator and model differs. The "Data Processing" section will provide a detailed introduction to the four types. This article only introduces the main process for task creation.

In actual use, visual modeling operators support adding text descriptions to help users better understand the remarks of the current operator.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39c1f36b1f3742c89b2f31f7def2a254~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b686d1fab874ca5888c47a6e7d1d3a3~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The visual modeling task creation page supports switching between free layout and grid layout, allowing flexible adjustment of the layout of each node in the task.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b77adb76dba4a35b27cb8713d2d2a01~tplv-goo7wpa0wc-image.image) </span>

The visual modeling new task page supports unified display of abnormal nodes in the task, assisting in troubleshooting task issues.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d36edf7d8bad43f9a1ea821db088c310~tplv-goo7wpa0wc-image.image) </span>

The visual modeling task creation page also supports deleting operators by pressing the Back or Delete key, improving data cleansing efficiency.

<span id="_2-5-数据预览"></span>
## 2.4 Data preview

<span id="_2-5-1-查看预览"></span>
### 2.4.1 View preview

**Step 1**: On the editing page of a visual modeling task, after selecting a data connection, you can conveniently preview data. You can preview **detailed data, table structure, and data profiling**.


* It supports setting whether to expand the data preview panel of the current type of operator by default and applying the setting to all operators, accommodating different user habits.

* The preview panels for "data profiling" and "detailed data" are merged to achieve centralized information display, simplify operations, and increase feature utilization.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9700f75acae4e5ba86c7cbe092a17ed~tplv-goo7wpa0wc-image.image) </span>


**Step 2**: Click the  **"▼"**  button for each column of data to quickly select an operator for data processing. As shown in the following figure:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94f0b58b1b124136ae2edb40503cffe4~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-5-2-采纳建议"></span>
### 2.4.2 Adopt suggestions

In the preview, data cleansing suggestions are provided. Users can complete cleansing with a single click, improving the efficiency of data cleansing. As shown in the following figure:

<span id="_2-5-3-即时设置"></span>
### 2.4.3 Instant settings

On the editing page of a visual modeling task, when opening data preview, you can instantly edit or configure the preview in the lower left corner of the interface. Users can configure the amount of data to be previewed (default is no more than 1,000,000 rows), supporting custom row counts or selecting all data. After configuration, the preview will refresh in real time. As shown in the following figure:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69cec5449349462aa47e6daedb28c480~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-6-节点执行"></span>
## 2.5 Node execution

In the configuration, a node can be selected and run to check its execution. Caution: When an upstream node is modified, the upstream node must be re\-executed before the current and downstream nodes can be executed.


* Execute this node: Run the current node. All upstream nodes must be executed first.

* Execute up to this point: Sequentially run any upstream nodes that have not been executed, followed by the current node.

* Start execution from here: Sequentially run the current node and subsequent nodes. All upstream nodes must be executed first. Typically used after the current node is modified.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7921686966744cadbb1ac1f45133781a~tplv-goo7wpa0wc-image.image) </span>

After a node is executed, a green check mark appears next to the node, indicating that the current node has been executed.

<span id="_2-7-输出数据集"></span>
## 2.6 Output datasets

Add an output node and choose to output to an existing dataset or create a new dataset. For details on configuring output datasets, see [Data Output](https://docs.byteplus.com/docs/dataagent/Data_Output_).

> Currently supported [Data Output](https://docs.byteplus.com/docs/dataagent/Data_Output_): Datasets stored in Hive, ClickHouse, and ByteHouse.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b85845936804e7ea380d88699a87150~tplv-goo7wpa0wc-image.image) </span>

Finally, you can open the run configuration dialog to edit the run schedule or run manually. The run frequency can be set to "Exact time" or "Interval duration".


* Exact time: Hourly, daily, weekly, or monthly

* Interval duration: 10 minutes, 20 minutes, or 30 minutes


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a6c1933ce7f4f8ba5dcaaa7e1cb4c36~tplv-goo7wpa0wc-image.image) </span>

When model configuration is complete, click Save or Save as in the upper right corner. If the model is not complete, you can also set the run frequency to manual, then click Save or Save as.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dcf8b248c6a448efa35ea18b9feb1e6b~tplv-goo7wpa0wc-image.image) </span>

Save the task configuration. Click Return in the upper left corner to go to the task details page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6dba662a52bb4be9acb0982ccdfaa649~tplv-goo7wpa0wc-image.image) </span>

Return to the visual modeling page and click "Run records" for the current task to run it manually. For more task management capabilities, see [Task Management](https://docs.byteplus.com/docs/dataagent/Task_Management).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cff4434823fa40daa25f4db3105f72a9~tplv-goo7wpa0wc-image.image) </span>

<span id="ef695a0a"></span>
## 2.7 Data download

On the dataset details and data preview pages, click "Download" to download data. The supported data formats are CSV and Excel. Preset options for the number of data rows include 100, 500, 1000, 5000, and the current previewed data. Custom row counts are also supported.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63b05fa363634abfba48353111205801~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


**Note:** 

Currently, the visual modeling module only provides offline tasks. To use real\-time tasks, the data source supports Kafka. (To use the real\-time task feature, you must purchase the DataAgent on\-premises version, Customer Data Platform (CDP), and Kafka simultaneously. For purchase inquiries, please contact your company's sales representative or customer success manager.)
