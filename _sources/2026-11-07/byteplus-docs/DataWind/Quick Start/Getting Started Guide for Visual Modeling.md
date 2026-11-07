---
title: "Getting Started Guide for Visual Modeling"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Getting_Started_Guide_for_Visual_Modeling"
---

Visual modeling is a data processing and modeling feature provided by Smart Data Insight. This article introduces the core workflow for using visual modeling to help you quickly understand the overall process. For detailed instructions on each step, you can refer to the various specific documents on visual modeling.

<span id="_1-创建任务"></span>
# 1. Create a task


* **On the visual modeling page, click "New Task"** 

* Define the task name, description, and save path. The save path refers to the folder name in the task navigation on the left. If there is no suitable folder, click "Task" to create a folder.

* Task type: The timeliness of the task data source and data processing workflow. Common offline task data sources include Hive, and real\-time data sources include Kafka.

> Note: The task type determines the types of data connections available, as well as the operator functions that can be used on the canvas.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c679c1c9615d4ef39cda750bbfae6f1f~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-添加数据连接"></span>
# 2. Add a data connection


* **Click the Add Data Connection + icon**

* **Select connection**: You can select an existing dataset, or choose a pre\-configured connection from existing data connections to read data from the corresponding connection (data source).

* If there is no available data connection, click "New Configuration" or quickly create a data connection in "New Data Connection".

> Before version V2.50, the page was as follows:

> <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13d5b0c881c041d59b8abfe9daeac8a6~tplv-goo7wpa0wc-image.image) </span>

> In version V2.50.0 and later, the interface is as follows:

> <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/860e4c1b07eb4d0e908f15adf386f112~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-添加输入节点数据"></span>
# 3. Add input node data


* **Drag the specific table name from the data connection to the canvas**

* Select the specific table name and drag it to the canvas to use it


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb04f6d66b1341898a8760c75cf88fa1~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-配置输入节点数据字段及数据抽取方式"></span>
# 4. Configure input node data fields and data extraction method


* Click the input node operator to expand the drawer at the bottom, which provides the configuration page for data reading

> The height of the page can be adjusted by dragging the upper boundary of the drawer, or you can scroll to display more content


* Extraction settings: These are the filter parameters for reading the input node's data table. If partitions exist, the partition fields are displayed by default

* Preview settings: This refers to the preview data involved in the canvas execution process (does not affect the final task execution). In theory, the less preview data there is, the faster the canvas preview execution speed. However, some AI operators depend on more data. It is recommended that the default preview data should not be less than 2,000 rows.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d74c40efbfa46ab81cc69cecaf3e3d5~tplv-goo7wpa0wc-image.image) </span>


* After configuration is complete, click Execute: This will read data into the canvas according to the configuration items.

* Preview exploration: This refers to exploring the distribution of each field based on the preview data to determine whether the data is usable.

* Logs: This refers to querying the execution logs of the task. If there is an execution failure, the reason for the failure can be viewed here.


<span id="_5-添加算子及连线"></span>
# 5. Add operators and connections


* Perform data cleaning and establish a directed cleaning workflow.

* Click the plus sign (+) at the output of the input data operator block to expand the available operators. Operator types include: data cleaning, output, feature engineering, machine learning, and natural language processing.

   * Data cleaning: See [Data Cleaning](https://docs.byteplus.com/docs/DataWind/Data_Cleansing). Mainly responsible for model building (such as multi\-table joins and multi\-table merges), field format conversion (such as field settings, pivoting rows to columns, and columns to rows), data computation (such as calculated fields, aggregation, Top K values), data filtering (such as deduplication and sampling), and many other tasks.

   * Output: Indicates that after the canvas workflow is executed, the data is output to the specified location and the task execution logic is configured.

   * Feature engineering/machine learning: Refers to AI algorithm capabilities such as principal component analysis, feature importance, clustering, classification, regression, and many other capabilities.

   * Natural language processing: Refers to natural language processing capabilities. Tokenization and stop word removal use open\-source word lists.

> Feature engineering, machine learning, and natural language processing operators can only be used in combination with the "prediction" operator.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ccd2023fa5cd42fe8fb17f08ce8cd62c~tplv-goo7wpa0wc-image.image) </span>


* When adding connections between operators, a connection can only be created if the output node of one operator and the input node of the downstream operator are the same color. In addition, the number of input nodes indicates how many upstream operators can be connected.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9e9cb94887443baaefa8fd44a6d34dc~tplv-goo7wpa0wc-image.image) </span>


* Add or remove operators between connections: Hovering over a connection allows you to add, that is, insert a new operator. Hovering over a connection also allows you to delete, that is, remove the connection and establish a new relationship.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abe357d21cf34bf3b4edd85a80b485d9~tplv-goo7wpa0wc-image.image) </span>

<span id="_6-配置输出"></span>
# 6. Configure output


* Save data to a dataset

* Select the "Output" operator: Determines where the data is output and how the output is performed, such as dependency relationships, monitoring alerts, priority, and more.

* Output dataset: You can select an existing dataset to write the newly created workflow into, or create a new dataset to store the output data.

> If you select an existing dataset, confirm whether the data structure of the existing dataset is consistent. If not, writing may fail.


* Dependency configuration: Establish the prerequisite dependency conditions for executing the output operator. For example, if the upstream table is A, after adding the dependency on A, the current operator task will execute again only after the A task is completed.

* Advanced configuration: Configure the execution priority order of the operator task and the concept of storage partitions.

* Monitoring configuration: Configure the rules and notification methods for monitoring alerts.

> To push alert information through the office platform, first confirm whether office platform integration has been configured.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73b126312ea04c62b13b9522c368e8b8~tplv-goo7wpa0wc-image.image) </span>

<span id="_7-任务运行配置"></span>
# 7. Task execution configuration


* **Execution methods for the canvas workflow**

* Manual execution: Task execution requires manual clicking to execute.

* Scheduled execution: The system automatically executes the task according to the specified frequency, such as daily execution, weekly execution, and more.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4499fc8226d64321a4745399c373a5a0~tplv-goo7wpa0wc-image.image) </span>

<span id="_8-输出数据集应用"></span>
# 8. Output dataset application

After a visual modeling task outputs to a dataset, you can filter all sources of "visual modeling" in the dataset sources to view all tasks output by visual modeling.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a1f005469cb44409657c5d5d71bd2e3~tplv-goo7wpa0wc-image.image) </span>


* Tasks output to Hive will indicate that they cannot be used for visual queries. Clicking edit will prompt the generation of the address of the visual modeling task, and clicking it will take you directly to the details page of the visual modeling task.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12a63b663bc84d9680c9890bf799befb~tplv-goo7wpa0wc-image.image) </span>


* After clicking a task that has been exported to ClickHouse, it can be used directly for subsequent visual queries. Clicking Edit will prompt the generation of the address for the corresponding visual modeling task, and clicking the address will take you directly to the details page of that visual modeling task.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5812f77f329442e3905124e51491f58f~tplv-goo7wpa0wc-image.image) </span>
