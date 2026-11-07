---
title: "Queue Configuration"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Queue_Configuration"
---

<span id="_1-概述"></span>
# 1. Overview

For certain business operations, reviewing long\-term data and comparing it with current business conditions are essential analytical methods. Therefore, it is often necessary to view long\-term data and perform relatively frequent dataset backfills, which can impact the scheduling and execution of scheduled datasets. For example, managers within the company frequently need to review long\-term data, or planning and operations personnel often compare data from different periods, resulting in at least 20 dataset backfills per month. To address this scenario, Intelligent Data Insight has introduced the capability for "backfill tasks to support a separate queue," enabling users to configure different queues for scheduled tasks and data backfill tasks based on business needs, thereby reducing the impact of data backfills on routine tasks.

<span id="_2-使用逻辑"></span>
# 2. Usage

In the current V2.56.1 version, queue configuration supports only one queue. The ability to select and configure multiple queues and other features will be introduced gradually. Please stay tuned.

The user workflow for the queue configuration feature is shown in the following diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83f15dcf1d1c46bdb44164da502a4856~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-队列管理"></span>
## 3.1 Queue management

In system management, click the system configuration button, and select the queue configuration module from the left sidebar to manage queues.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7780693649404569a9ce389f980013a6~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-1-默认队列"></span>
### 3.1.1 Default queue

Currently, only one queue is supported. This queue is the default queue and is named offline. As shown in the following diagram, the default queue information includes: queue name, queue resources, queue description, authorized project scope, group default queue, and applicable task types.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e486ce20d8634fd2adf95030e5bfcbbb~tplv-goo7wpa0wc-image.image) </span>

Click the edit button to modify the queue description. The specific operation is shown in the following diagram.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e301ee966d784b5093fb784b142e8e9a~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-2-适用任务类型"></span>
### 3.1.2 Applicable task types

The default queue offline applies to scheduled tasks and backfill tasks. Currently, each task type supports one backfill queue.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63361848194f478488327193fdae9fb7~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-3-默认策略"></span>
### 3.1.3 Default policy

As shown in the following diagram, the default policy is to prioritize the default queue. Hover the mouse over the information icon next to the default policy to view the detailed explanation of the default policy.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79e97fb9d330429490a4a6d99efcd147~tplv-goo7wpa0wc-image.image) </span>

<span id="6ab24cb6"></span>
### 3.1.4 Authorization scope

Authorization can be granted based on project scope or user scope. The available scope of the queue is the sum of the authorized project and user scopes.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58989645fb4d42a5ad0351bc78f6b618~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-任务配置"></span>
## 3.2 Task configuration

<span id="_3-2-1-数据集管理"></span>
### 3.2.1 Dataset management

Go to the dataset in the data preparation module, select the corresponding dataset, and go to the synchronization status bar. Click "Data Synchronization" in the upper right corner to configure synchronization.


* Basic settings: Set the range of data to be synchronized. Only data within the synchronization lifecycle is supported. You can choose whether to display this time range in the synchronization status list after enabling synchronization.

* Backtracking settings: Dependency check and queue can be configured. Dependency check can be set to execute according to dependencies or execute immediately. The queue supports selecting a backtracking queue.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/931351a0a7c94738a957f10afdb66c76~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-2-数据集编辑"></span>
### 3.2.2 Dataset editing

Click Data Preparation \- Dataset, select the corresponding dataset, then click Dataset Editing \- Synchronization Settings \- Advanced Settings to select a queue. The default option is the default queue. For more information about other synchronization settings, refer to the synchronization settings documentation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea20ad2967964f868d93595b26ecdd83~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-3-可视化建模管理"></span>
### 3.2.3 Visual modeling management

Click Data Preparation \- Visual Modeling, select the corresponding task, then click Run. In the pop\-up window under Backtracking Settings, you can select a queue. The default option is the default queue. For more information about other run configuration operations, refer to the task operation \- run documentation.

<span id="_3-2-4-可视化建模编辑"></span>
### 3.2.4 Visual modeling editing

Click Data Preparation \- Visual Modeling, select the corresponding task, then click Edit. In Output, select Advanced Settings to select a queue. The default option is the default queue. For more information about other output configuration operations, refer to the output documentation.
