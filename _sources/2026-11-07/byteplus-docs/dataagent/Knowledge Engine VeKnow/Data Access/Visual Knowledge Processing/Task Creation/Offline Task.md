---
title: "Offline Task"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Offline_Task"
---

<span id="6b0ab68d"></span>
# Feature Overview

Task creation refers to the creation of visual knowledge processing tasks, which usually includes new tasks, data connection, and other steps. The visual knowledge processing task supports extracting data from the data source, adding data processing nodes by dragging and dropping, and outputting the processed data to the target source.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Task type: real\-time task, offline task (task type cannot be switched after task creation)</div>


   * <div data-tips="true" data-tips-type="tip">Real\-time tasks refer to tasks that can be executed in real time following real\-time updated data sources and output as real\-time updated data. Real\-time task support input data sources are: Kafka, Pulsar;</div>


   * <div data-tips="true" data-tips-type="tip">Offline tasks refer to tasks that follow offline updates to a data source and can be set to be executed manually and periodically, with output as regularly updated data or model files. The data sources supported for offline tasks are: Hive, MySQL, ClickHouse, Kafka, HttpAPI, Feishu, CSV/Excel, Oracle, Impala, PostgreSQL, Hbase, SQLServer, MaxCompute, ADB, MongoDB, Hana, Teradata, Db2, Vertica, GreenPlum and more than 20 mainstream data sources;</div>



This article will introduce the creation steps of **offline tasks** in combination with the product practical interface.

<span id="169e63c8"></span>
# Usage Restrictions


* Users need to have **project editing** permission or **visual knowledge processing module of the new task** permission to use this function.

* Some of the features in visual modeling are **paid capabilities** , please contact your commercial manager if necessary


<span id="c3458c43"></span>
# Operation Steps

<span id="0dbb27de"></span>
## **Step 1: Create a new task**


1. In the left navigation bar, select **Data Access** \> **Visual Knowledge Processing** .

2. On the **task list** page, click **New** in the upper left corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2273a4aa47e44393a2edc75dad55f8b7~tplv-goo7wpa0wc-image.image) </span>

3. Select **New Offline Task**.

   After selecting, you will enter the task editing page, and you can edit the task name in the upper left corner of the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/952741b8391f4123ab461d8085f695e2~tplv-goo7wpa0wc-image.image) </span>

4. (Optional) Use the application sample template.

   In the visual knowledge processing task editing page, provide a variety of operator templates, click on **all templates** to quickly view.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/826199a28fd747fe9fe35244b43d0844~tplv-goo7wpa0wc-image.image) </span>

   Each template supports **preview** or **application**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59a96ff3ccf04649aa1afc4abd4b1fd8~tplv-goo7wpa0wc-image.image) </span>

   Click **Preview** , will introduce the current operator template built\-in sample data, scene description, the operator used, click **Use template** can be quickly applied.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/312b5ad8f62b4fc193ac5a253f767960~tplv-goo7wpa0wc-image.image) </span>

   After using the template, the system will display the detailed configuration of the corresponding application scenario using the system sample data processing, helping users to further understand the capabilities and usage of the current operator.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49b1c96ed8574a458edb2f6c0146f705~tplv-goo7wpa0wc-image.image) </span>


<span id="bbe43ace"></span>
## **The second step: data connection**


* **New data connection**

   On the New Task page, click the **plus sign** at the top left to add a data connection; you can choose to add multiple types of data connections, and the platform supports custom SQL for most offline storage.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5c08d8005ab44e4bc018eb905372e8e~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If a dataset is selected, it loads in the left canvas: custom SQL, visual modeling dataset, customer data platform dataset:   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Hive</strong> / <strong>ClickHouse</strong> custom SQL:   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Hive: Visual modeling interface, showing the hive database & table that the currently logged in user has permissions:   </div>
   

         1. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Based on the permissions of the currently logged in user, the database & table list is obtained through API calls;   </div>
   

         2. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you need to use a specific table to build a visual modeling etl task, you need to authorize the kerbros account of the volcano base for the specific database & table. For example, if the user wants to use db1.tbl1, in the uat environment, you need to authorize minibase_uat;   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">ClickHouse: Visualize the modeling output and store the data as a Clickhouse dataset, you can write SQL and meet ClickHouse syntax   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Visual modeling dataset</strong> : The dataset of visual modeling output, regardless of the output storage type is Hive/ClickHouse   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Customer Data Platform Datasets</strong> : Purchase and deploy customer data platforms, system\-produced datasets.   </div>
   

* **Remove data connection**

   In the data connection list of the visual modeling task creation page, click the delete button on the right side of a specific data connection to remove the data connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53d25b25a5a741bd94a382f56c5eb18c~tplv-goo7wpa0wc-image.image) </span>


<span id="7b9f8b0e"></span>
## **Step 3: Process the node**

Add and configure the processing node by clicking the plus sign on the right side of the node, and drag the plus sign on the right side of the previous node and the origin on the left side of the next node to connect to configure the node circulation relationship. Click "Apply" to expand the preview of the processed data results.

As shown in the figure below, click the output + sign of the input data operator block, expand the operation node: **output, data cleaning, special area operator** , click one of them, you can see the operator that can be used.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd3e2bb7b4f24935803349b10a3a282e~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Common operators are as follows:</strong></div>



* <div data-tips="true" data-tips-type="tip">Output: Indicates that the canvas process has finished executing the data output to the specified location and configures the task execution logic</div>


* <div data-tips="true" data-tips-type="tip">Data cleaning: mainly responsible for model building (such as multi\-table joining, multi\-table merging), field format conversion (such as field setting, row to column, column to row), data calculation (such as calculating fields, aggregation, top K values), data filtering (such as deduplicate, sampling), etc</div>


* <div data-tips="true" data-tips-type="tip">Feature engineering/machine learning: representing AI algorithm capabilities such as principal component analysis, feature importance, clustering, classification, regression, etc</div>


* <div data-tips="true" data-tips-type="tip">Natural language processing: represents NLP natural language processing capabilities, in which word segmentation, removal of stop words, and word packages are open\-source word packages</div>



<span id="692eaba6"></span>
## Step 4: Canvas Configuration

**General data processing**


1. Add input operator: Drag and drop data from the left to connect to the canvas

2. Add intermediate operators: add data processing operators (data cleaning operators, AI class operators)

3. Add an output operator: Select the "output" operator to output data to the dataset


**AI Data Mining**


1. Add input operator: Drag and drop data from the left to connect to the canvas

2. Add intermediate operators: Add AI class operators (AI\-feature engineering, AI\-machine learning, AI\-natural language, AI\-prediction)

3. Add an output operator: Select the "Save Model" operator to save the data to the model


**Add Node**


* Method 1: Click "+" in the operator card, expand the drop\-down menu and add a node.

* Method 2: Drag the operator from the left into the canvas.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a990d7acac447fda2427bbad05d50f1~tplv-goo7wpa0wc-image.image) </span>

**Add Branch:**  Click "+" in the operator card to expand the drop\-down menu and add a new branch.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8faf6a40f2f04729b3a560bfceabecdf~tplv-goo7wpa0wc-image.image) </span>

**Insert Node:**  Click "+" in the connection, expand the drop\-down menu and insert the node

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/245ec43ca09147cf8c6448c2100ab5bb~tplv-goo7wpa0wc-image.image) </span>

**Add a wire:**  Hold the output point to the right of the previous operator and drag the wire to the input point to the left of the next operator

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3908b805571e40d7b8e050c10abc30dd~tplv-goo7wpa0wc-image.image) </span>

**Switch Nodes:**  Click the More button in the operator card or the right\-click operator card to expand the drop\-down menu and switch nodes **Delete Nodes:**  Click the More button in the operator card or the right\-click operator card to expand the drop\-down menu and delete nodes

In practical use, the visual modeling operator supports the addition of text descriptions to help users more clearly understand the remarks of the current operator.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/171f8090a8a34347bdf2f02c15aa256c~tplv-goo7wpa0wc-image.image) </span>

The visual knowledge processing task creates a page, supports free layout and grid layout switching, and flexibly adjusts the layout of each node of the task.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/119d4736ec2f4c2abf56bb7abbc1395c~tplv-goo7wpa0wc-image.image) </span>

Visualize knowledge processing to create a new task page, support unified display of task abnormal nodes, and assist in troubleshooting task problems.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6d8bdaff58a46cb8297c39208f11fed~tplv-goo7wpa0wc-image.image) </span>

Visual knowledge processing tasks create pages, and also support operator deletion operations by clicking the Back or Delete keys to improve data cleaning efficiency.

<span id="25d84d04"></span>
## **Step 5: Data Preview**


1. **View preview**


On the edit page of the visual knowledge processing task, after selecting the data connection, it supports convenient preview capabilities. Users can preview **detailed data, table structure, data profiling** . Click the  **"▲" button** of each column of data to support quick selection of operators for data processing. As shown in the following figure:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11f564366eda4150b1ad657499b45cf2~tplv-goo7wpa0wc-image.image) </span>


2. **One\-click cleaning**


In the preview, data cleaning suggestions are provided, allowing users to complete the cleaning with one click, thus enhancing the efficiency of data cleaning. As shown in the following figure:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acb655919280415eba9a156aa0f1f8dd~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53671a7ca8754b498b707ac7d6c255e9~tplv-goo7wpa0wc-image.image) </span>


3. **Instant setup**


On the edit page of the visual knowledge processing task, when you open the data preview, you can make instant edits or settings for the preview at the bottom left of the preview interface. Users can configure the amount of data participating in the preview calculation (no more than 1,000,000 rows by default), support custom row counts, or select the full amount of data. Once configured, the preview will be refreshed in real time. As shown in the following figure:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/438e6be2dee24e1bbfc5e751ced00231~tplv-goo7wpa0wc-image.image) </span>


4. Download the dataset


When creating offline visual knowledge processing tasks, click the **Download** button on the operator preview and dataset details page to download offline datasets, which is convenient for users to export data for local analysis or further processing, and improve the scalability of data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b92c735c2d734368a12fd46c835a1025~tplv-goo7wpa0wc-image.image) </span>

<span id="2fb6463d"></span>
## **Step 6: Node execution**

In the configuration, you can select a node and run the node for operation inspection. It should be noted that when the upstream node is changed, the upstream node must be re\-executed before the current and downstream nodes can be executed.


* Execute this node: Run the current node, and all upstream nodes need to be executed

* Execute to here: Run the upstream unexecuted node and the current node in turn

* Execution starts from here: Run the current node and subsequent nodes in sequence, and all upstream nodes need to be executed. Generally, it is used after the current node is changed.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/743ce336d6164c8dbeebabb70875293d~tplv-goo7wpa0wc-image.image) </span>

After the node execution is completed, there will be a green checkmark next to the node, indicating that the current node has completed the execution.

<span id="318badf4"></span>
## **Step 7: Output**

The output methods are: output dataset, output label, import knowledge engine

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6e070227f5e45049af65cc588450d39~tplv-goo7wpa0wc-image.image) </span>

**Output dataset**


1. Add an output node and choose to output to an existing dataset or create a new dataset.

> Supported output datasets: Hive, ClickHouse


Stored dataset

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72edb93bb4c7486b948ec449e1be235d~tplv-goo7wpa0wc-image.image) </span>


2. You can open the run configuration pop\-up window, edit the run cycle, or run it manually. The running frequency can be selected as "Exact Time" or set as "Interval Time".

* Exact time: hour level, sky level, week level, month level

* Interval time: 10 minutes, 20 minutes, 30 minutes


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31c0009f1c754337bfc0e57e2d429b2c~tplv-goo7wpa0wc-image.image) </span>

**Monitoring configuration**

You can set **data result alarm rules:** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9b84188b81e4ab0854a87427a21aec3~tplv-goo7wpa0wc-image.image) </span>


|Monitor item |Explain |
|---|---|
|**Percentage difference (compared to the previous day)**  |Calculation formula: (the number of data rows yesterday \- the number of data rows the day before yesterday)/the number of data rows the day before yesterday;<br><br>Yesterday and the day before yesterday refer to the business date, not the running date. For example, if the instance was running on May 7, then yesterday refers to the number of data rows on the business date on May 6. |
|**Percentage difference (compared to the previous seven\-day average)**  |Calculation formula: (the number of data rows yesterday \- the average number of data rows in the past 7 days)/the average number of data rows in the past 7 days; |
|**Percentage difference (compared to the same period last month)**  |Calculation formula: (the number of data rows yesterday \- the number of data rows in the same period last month)/the number of data rows in the same period last month;<br><br>Definition of the same period last month: For example, if this month is run on the 1st of each month, then the same period last month is the 1st of the previous month; this month is run on the 31st of each month, and if there is no 31st of the previous month, take the last day of the previous month. |
|**Percentage difference (compared to the same period last week)**  |Calculation formula: (the number of data rows yesterday \- the number of data rows in the same period last week)/the number of data rows in the same period last week;<br><br>Definition of the same period last week: For example, this week is Wednesday, and the same period last week refers to last Wednesday. |



3. When the model configuration is complete, you can click **Save** or **Save As in the upper right corner** . If the model is not completed, you can also adjust the running frequency to save or save as after manual operation.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae0fdba04908496a8c5376b39ce29db2~tplv-goo7wpa0wc-image.image) </span>

Save the task configuration and click Return in the upper left corner to jump to the task details.

Return to the visual knowledge processing page and click the  **"Run Record"**  of the current task to run it manually.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a94d76fd2f4c499a8f10cbb878426d43~tplv-goo7wpa0wc-image.image) </span>

**Common problem**

**Q1: When creating an offline visual knowledge processing task, does the system time parameter support the ${month}, ${year} system parameters?** 

A: Support. As shown in the following figure:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a9936d56ddfc4a248dc2252f708885ce~tplv-goo7wpa0wc-image.image) </span>
