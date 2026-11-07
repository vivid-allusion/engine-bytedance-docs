---
title: "Custom Model Tags"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Custom_Model_Tags"
---

<span id="_1-产品概述"></span>
# 1. Product Overview

Supports the creation of model tags, building AI prediction models, and obtaining tags based on analytical models.

<span id="_2-常见应用场景"></span>
# 2. Common Application Scenarios

In the automotive industry, sales require focused follow\-up on high\-intent car buyers. By using [model tags] to train models with purchased customer characteristics and optional package consumption levels using logistic regression multicategory training, intent prediction for non\-purchased customers is possible.

<span id="_3-名词解释"></span>
# 3. Noun Explanation


|Noun |Explanatory notes |
|---|---|
|Task |The process of loading data from input data sources, undergoing data processing and cleaning, and finally loading and outputting to the target data source. |
|Execution Records |Each task run generates a runtime record, which can be triggered manually by the user or automatically launched by the system based on periodic configurations. |
|Processing Flow |Shows the process and logic flow of the current model's data processing nodes. |


<span id="_4-操作步骤"></span>
# 4. Operation Steps

Go to the **Labeling System** module, click the **Create Tag** button, and select **Custom Model Tags** to access this functional module.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_122821925790ed8d9f9de9e60efb1756.png) </span>

<span id="_4-1-创建入口"></span>
## 4.1 Creation Entry

Click to create [model tags], navigate to [Visual modeling] page, which displays tag templates by default. You can directly reuse templates for data cleaning or machine learning modeling processes.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/510db9ad03014016a689b278b0d081af) </span>

<span id="_4-2-新建任务"></span>
## 4.2 Create Task

Click [Create Task] to add a data connection; currently supports adding various data connections such as Hive, Clickhouse, MySQL, and supports adding data connections in the form of uploading Excel, CSV, or importing from Lark tables.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/5713030b7ed042dfb473d3dfbdf17b8e) </span>

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/882702e37f6546318791a8d0a06a84fd) </span>

<span id="_4-3-建模配置"></span>
## 4.3 Model Configuration

Drag the data source table into the canvas area and configure it. Support adding multiple data filtering conditions in the lower configuration area, with logical relationships between rules being "AND"; also supports filling in the data quantity for calculation in [Preview Settings]; this setting does not affect the formal operation of the task, only as a row limit for detailed data in [Data Results].

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/368cb33ac57f4f3190ef682a052d2658) </span>

<span id="_4-4-配置处理节点"></span>
## 4.4 Configure Processing Nodes

Add and configure processing nodes, support data preprocessing, data cleaning, feature engineering, machine learning, etc. processing methods. After selecting and executing, you can expand the preview of the processed data results.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/978cbb6606334672a0345ec9296a716c) </span>

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/3ec2bfd15be14f84b73624d19590415f) </span>

<span id="_4-5-输出模型标签"></span>
## 4.5 Output Model Labels

Add an output node, choose and configure output labels.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/b28240aecd1f411bb0a550576349d7d3) </span>Configure the fields of the output labels, such as entity corresponding ID, output to the column of the label; complete the current label's name and description parameter supplement.

In the dependency configuration, the dependency table is enabled by default and can be manually modified and edited.

In advanced settings, you can configure priority levels such as normal, high, and very high, and also add runtime parameters to assist in improving synchronization success rates.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/1c6dba884b8f43a1b2635839ebaefe25) </span>Click [Save] to view [Processing Flow], [Data Preview], and [Execution Records] on the task details page.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/79755a5c0a194c02aa3a7045ac870088) </span>

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/a3a58c20d8154759ab90d994fad7fd2d) </span>

**Step Seven:**  View the model tags on the [Labeling System] page, and you can check the distribution of current tag population, historical details, and execution records on the tag details page.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f5a777b10597ee63438b9c9321c5b393.png) </span>

<span id="_5-模型标签案例"></span>
# 5. Model Tag Cases

[商业银行客户流失预测](https://docs.byteplus.com/docs/undefined/65f1580635802d04c87f1a67)

[汽车用户意向标签预测](https://docs.byteplus.com/docs/undefined/65f1580635802d04c87f1a6a)

[汽车用户关键行为统计](https://docs.byteplus.com/docs/undefined/65f1580735802d04c87f1a6d)
