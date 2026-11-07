---
title: "LAS Dataset"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/LAS_Dataset"
---

<span id="a36e2747"></span>
# 1. Overview

The agent supports connecting to the lakehouse analytics service LAS to obtain data, create datasets, and perform further analysis.

If your Volcano Engine account has purchased LAS resources, a default LAS storage data connection will appear when creating a new dataset, which can be used for modeling and data extraction.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24fe95ef20f74465a4d6e0be89f3e46f~tplv-goo7wpa0wc-image.image" width="2682px" /></div>


<span id="e716ddab"></span>
# 2. Quick start

(1) Click Data Preparation \-\> Dataset, click the plus sign on the left, and select "Create dataset".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bea6e2f199ab45cf835ccbd229ff164b~tplv-goo7wpa0wc-image.image) </span>

(2) Click LAS.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc07e5ecaeb84c388018fd69bd15a5d8~tplv-goo7wpa0wc-image.image) </span>

(3) Select table creation.


* On the model configuration page, select a custom SQL or a table from the database on the left, and drag it to the canvas on the right using the mouse.

* In the Hive table list, only tables you have access to are visible.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/672112a0c41d4d7e8dd065f7e3644163~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(4) To join LAS with other data, after selecting the LAS data source, click the plus sign again to add a new data source.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac4d29740c444d5c94d5d099352b5961~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span id="70fecef1"></span>
# 3. Feature introduction

<span id="a8329ff3"></span>
## 3.1 Model configuration

In model configuration, you can set field retention, filter data, set extraction parameters, and more. For details, see [Model Configuration](https://docs.byteplus.com/docs/dataagent/Model_Configurations).

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/938cf64d3ea8420eae2f9b433754753e~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span id="b07118a3"></span>
## 3.2 Data filtering

In data filtering, you can filter data from the data source and retain only the data that meets the criteria. For details, see [Data Filtering](https://docs.byteplus.com/docs/dataagent/Data_Filtering).

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fbcab76abb50450fad3c8b5b0076c16f~tplv-goo7wpa0wc-image.image" width="2132px" /></div>


<span id="01a1c3d6"></span>
## 3.3 Field configuration

Field configuration allows you to add complex calculated fields based on model fields or perform other configurations. For details, see [Field Configuration](https://docs.byteplus.com/docs/dataagent/Field_Configuration).

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b51e75e42b244a70b08c697a31f3371d~tplv-goo7wpa0wc-image.image" width="2559px" /></div>


<span id="be3de775"></span>
## 3.4 Synchronization settings

In synchronization settings, you can configure synchronization frequency and timing, dependency settings, synchronization monitoring, performance settings, and other settings for the dataset. For details, see [Synchronization settings](https://www.volcengine.com/docs/4726/47764).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/338fad22ba2a4d06beffe6dc972d0240~tplv-goo7wpa0wc-image.image) </span>

<span id="16219220"></span>
## 3.5 Recommended dependencies

This product provides a flexible **task scheduling dependency configuration** feature. Scheduling dependencies usually refer to the upstream and downstream dependencies between nodes scheduled periodically during data synchronization and data development. By scheduling tasks to run upstream and downstream nodes in order according to node dependencies, downstream nodes will only start running after upstream nodes have successfully run, ensuring timely output of effective business data.

**Recommended dependency** refers to the automatic construction of data source partition detection tasks and automatic configuration of scheduling dependencies in LAS data sources with **partitions** by the system. **The task instance for the day will only be triggered when the detection task detects that the upstream partition is ready.**  (Recommended dependency configuration is not supported for data sources without partitions.)

Note: After the system wakes up the Sensor task at the scheduled time, it checks every 5 minutes whether the specified partition table of the data source has been generated. If the partition table is generated, the current task will be executed immediately. If the partition is not produced for more than 50 hours, the Sensor task will be marked as failed.

> Sensor definition: Sensor tasks mainly refer to scheduled tasks generated by system scripts to discover partitions, not referring to the current task. For user\-configured settings, the system will automatically **detect and check** whether the partition table required by the task exists in the user's data source. If it exists, it means that the upstream data preparation is complete and the downstream data can begin processing.


The system will automatically discover Sensor tasks for dependencies that have already been created for the current table and recommend them as options. If there are no recommendations, the list will be empty, and the user can configure dependencies manually.

**Configuration method**: Confirm that the data source is a partitioned table, set the filtering criteria for partition data in the model configuration, and you will see recommended dependencies in Synchronization Settings \> Dependency Configuration \> System Automatic Configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b90ad42c8f04cb8a45a53c686fbd142~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7bf6d07c5b524d7b970ab55078fbd977~tplv-goo7wpa0wc-image.image) </span>
