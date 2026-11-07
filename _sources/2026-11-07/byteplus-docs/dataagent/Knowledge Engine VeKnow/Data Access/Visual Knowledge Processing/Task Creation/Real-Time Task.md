---
title: "Real-Time Task"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Real-time_Task"
---

<span id="3c2967bf"></span>
# Feature Overview

Task creation refers to the creation of visual knowledge processing tasks, which usually includes new tasks, data connection, and other steps. The visual knowledge processing task supports extracting data from the data source, adding data processing nodes by dragging and dropping, and outputting the processed data to the target source.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Task type: real\-time task, offline task (task type cannot be switched after task creation)</div>


   * <div data-tips="true" data-tips-type="tip">Real\-time tasks refer to tasks that can be executed in real time following real\-time updated data sources and output as real\-time updated data. Real\-time task support input data sources are: Kafka, Pulsar;</div>


   * <div data-tips="true" data-tips-type="tip">Offline tasks refer to tasks that follow offline updates to a data source and can be set to be executed manually and periodically, with output as regularly updated data or model files. The data sources supported for offline tasks are: Hive, MySQL, ClickHouse, Kafka, HttpAPI, Feishu, CSV/Excel, Oracle, Impala, PostgreSQL, Hbase, SQLServer, MaxCompute, ADB, MongoDB, Hana, Teradata, Db2, Vertica, GreenPlum and more than 20 mainstream data sources;</div>



This article will introduce the creation steps of **real\-time tasks** in combination with the product practical interface.

<span id="8349c95a"></span>
# Usage restrictions


* Users need to have **project editing** permissions or **new task permissions in the Visual Knowledge Processing section** to use this feature.

* Some of the features in visual knowledge processing are **paid capabilities** , please contact your business manager if necessary.


<span id="3ca9e8a7"></span>
# Operation steps

<span id="b3bea2d4"></span>
## **Step 1: Create a new task**


1. In the left navigation bar, select **Data Access** \> **Visual Knowledge Processing** .

2. On the **task list** page, click **New** in the upper left corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc188678551049fc9695c6b4860560e1~tplv-goo7wpa0wc-image.image) </span>

3. Select **New real\-time task** .

   After selecting, you will enter the task editing page, and you can edit the task name in the upper left corner of the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/244fdccd1af74e6eaea853b3f0275eb3~tplv-goo7wpa0wc-image.image) </span>


<span id="51f14348"></span>
## **The second step: data connection**


* **Create a new data connection.** 

   Create a new task page, click the plus sign at the top left, and add a data connection;

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d07e4c85f7864ed4aba3da1df04ba371~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The real\-time task supports Kafka and CDC MySQL, which are not enabled by default. If you want to use it, please contact your account manager and complete the following pre\-operations:   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">SaaS environment: Purchase <a href="https://www.byteplus.com/en/product/kafka?_vtm_=a38233.b40801.0_0.0_0.0.531_7651452472122639877">BytePlus Kafka </a>and connect to the Volcano Engine Kafka data source in the data connection.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Private deployment: Have your own open source Kafka, Pulsar, and connect to the Kafka data source in the data connection.   </div>
   

* **Remove data connection**

   In the data connection list of the visual knowledge processing task creation page, click the delete button on the right side of a specific data connection to remove the data connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3aae4557bcf48fe9b2fad371c6ccd30~tplv-goo7wpa0wc-image.image) </span>


<span id="b917dadc"></span>
## **Step 3: Process the node**

Add and configure the processing node by clicking the plus sign on the right side of the node, and drag the plus sign on the right side of the previous node and the origin on the left side of the next node to connect to configure the node circulation relationship. Click "Apply" to expand the preview of the processed data results.

As shown in the figure below, click the output + sign of the input data operator block to expand the operation node: **output, data cleaning** , and click one of them to see the operators that can be used.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88f7be1e133c4e8db9f33e77a4d87755~tplv-goo7wpa0wc-image.image) </span>

**Common operator description**


* **Output:**  It indicates that the data output of the canvas process is completed to the specified location and the task execution logic is configured, including outputting real\-time data sets, outputting real\-time labels, and shunt output.

* **Data cleaning:**  Support calculated columns, filtered rows, field settings, IDM multi\-subject transformation relationship operator, ID Mapping operator, split fields.


<span id="b8a5bacb"></span>
## **Step 4: Node Execution**

In the configuration, you can select a node and run the node for operation inspection. It should be noted that when the upstream node is changed, the upstream node must be re\-executed before the current and downstream nodes can be executed.


* Execute this node: Run the current node, and all upstream nodes need to be executed

* Execute to here: Run the upstream unexecuted node and the current node in turn

* Execution starts from here: Run the current node and subsequent nodes in sequence, and all upstream nodes need to be executed. Generally, it is used after the current node is changed.


<span id="8bb2d7f9"></span>
## **Step 5: Output the dataset**


1. **Add an output node** and select Output to an existing dataset or New dataset.

> Supported output datasets: Datasets stored ClickHouse


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ea7ebc208cc45d7af2fe5777a48c9f6~tplv-goo7wpa0wc-image.image) </span>


2. **Configure the data life cycle,**  that is, the number of valid retention days extracted from the data in the system storage, the non\-partitioned table retains the data according to the data update time, the date partition retains the data according to the partition date, and the data outside the life cycle will be automatically cleared at 0 o'clock every day.


**Advanced settings for data lifecycle:**  that is, on the basis of the number of retention days, you can selectively retain historical data.


* Example 1: If the last 7 days are selected, the data of the last 7 days will be retained, and the data beyond 7 days will be cleared according to the data update time.

* Example 2: (Advanced function): If you select the last 7 days + keep the data of the last day of the month when it expires, the data of the last day of the month in the historical data will also be retained in addition to the last 7 days data


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Quarterly is the natural quarter (e.g. January\-March is the first quarter)</div>


<span id="4b52903e"></span>
###### <div data-tips="true" data-tips-type="warning">Suggestion:</div>


<div data-tips="true" data-tips-type="warning">The longer the retention period, the more system storage resources will be occupied. Please choose a reasonable lifecycle range according to your needs</div>


<div data-tips="true" data-tips-type="warning">After completing the configuration, click the <strong>Save</strong> button in the upper right corner.</div>



3. After completing the configuration, click the **Save** button in the upper right corner.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/beb647c234184db18f674ce3812cee20~tplv-goo7wpa0wc-image.image) </span>

**Output monitoring rules**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e686d5f59e3d4896bacaa0625c29d6b4~tplv-goo7wpa0wc-image.image) </span>


1. Task running status monitoring: Send an alarm when the task becomes suspended while running (excluding the case of manually stopping the task running).

2. Dirty data quantity monitoring: Dirty data refers to data that has not been successfully written within a period of time due to non\-compliance with data rules (data loss). The current missing links include:

   A. The push data of the input node is different from the structure of the topic table;

   B. Processing stage: OneID is not associated;


Configurable alarm rules: "For XX minutes in a row, alert when there are more than one piece of dirty data".
