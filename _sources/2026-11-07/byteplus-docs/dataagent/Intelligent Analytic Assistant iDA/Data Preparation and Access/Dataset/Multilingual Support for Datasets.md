---
title: "Multilingual Support for Datasets"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Multilingual_Support_for_Datasets_"
---

<span id="634ea235"></span>
# 1. Overview

When there are members using different languages in a project, multilingual configuration is required to help members understand the data content in datasets and dashboards. After enabling multilingual display configuration, modifications to dataset and field information by users in different language environments do not affect each other. Changes to dataset and field configurations are saved only in the current language environment.

Currently, **Chinese/English** configuration is supported, and multilingual configuration is available for **dataset name**, **display name**, and **description**.

<span id="_2-前置操作"></span>
# 2. Prerequisites

<span id="_2-1-开启多语言配置"></span>
## 2.1 Enable multilingual configuration

Go to Project Center \- Project Information, and enable the Configure Multilingual Display option. (This operation requires **project management permissions**)

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee621a1143564a168c0f826c7ea83756~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-切换系统语言环境"></span>
## 2.2 Switch the system language environment

Click the language option button in the upper right corner, select a different language, and switch the system language environment to another language.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce6b370491d8400f9d1791bb2223208b~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-关闭多语言配置"></span>
## 2.3 Disable multilingual configuration

Note that after **enabling** multilingual configuration and configuring field content, **disabling** the project's multilingual configuration will **clear** the existing configuration. After **enabling** multilingual configuration again, **reconfiguration** is required.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43e572c4d8a144d9b0eb3fb08215d494~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30afb3fd9a3a433187de51cde0b40633~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

**The following operations demonstrate the effects of enabling multilingual configuration.** 

<span id="_3-1-修改数据集名称"></span>
## 3.1 Modify the dataset name

After configuring the dataset name in both Chinese and English language environments, switching the language environment will show only the dataset name configured for the current language environment.

The configuration can be done as follows. The operation process is described below:

(1) Enable multilingual display configuration in Project Center

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee621a1143564a168c0f826c7ea83756~tplv-goo7wpa0wc-image.image) </span>

(2) Switch the language environment to English. At this point, the dataset name is still in Chinese

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f2e9f47b003411eb241234e1baa4e1a~tplv-goo7wpa0wc-image.image) </span>

(3) As shown in the figure below, select the edit option for the corresponding dataset and click [Basic Information]

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f297a7873f074107863cda822bd1a382~tplv-goo7wpa0wc-image.image) </span>

(4) Delete the original Chinese name, change it to the required English name, and click "Confirm."

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f665adf2ad1460eb7786da0eb99def6~tplv-goo7wpa0wc-image.image) </span>

(5) When switching between Chinese and English again, you will find that the Chinese environment displays the Chinese name [测试数据_抽取], while the English environment displays the English name [Test Data_Extraction].

<span id="_3-2-修改显示名称、（字段）描述"></span>
## 3.2 Modify display name and (field) description

Similarly, when editing the dataset's **display name** and (field) **description** in both Chinese and English environments, the display will adapt to the actual language environment during use.

(1) In the English environment, select the dataset (Note: The operation process is the same as steps (1) and (2) in section 2.1 for modifying the dataset name), and click Modify Field under Data Preview.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a9a5a42e60d24dad8a9344fbbdee3228~tplv-goo7wpa0wc-image.image) </span>

(3) Directly modify the English name and description corresponding to the field name, then select Save at the top right of the dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/384eb466fb984c5383bd28ba5fde5af3~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Caution: After enabling multilingual configuration, once the <strong>display name</strong> is configured, the field preview, visualization, and other pages will use the <strong>display name</strong> instead of the field name for display.</div>


For example, when creating a new field expression "test", if no modifications are made, its display name will default to the field name, such as "User ID".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e1de3995dc004d37992c72ff6a45d210~tplv-goo7wpa0wc-image.image) </span>

We manually change the **display name** of this field in the Chinese environment to "显示名称1".

Therefore, in the field preview interface, it will be displayed as "显示名称1".

To facilitate differentiation, we change the display name of this field in the English environment to "show_name1".

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In addition, when editing field information, <strong>display names</strong> must not be duplicated; otherwise, a red prompt message will be displayed.</div>


<span id="_3-3-excel-批量修改"></span>
## 3.3 Excel batch modification

Suppose we already want others to directly define the English field names and descriptions. We can also download the Excel template of the dataset, give it to others, and upload it after modification.

(1) After switching to the English language environment, in Dataset \- Data Preview, click Excel batch modification (Excel 批量修改) to download the current field list and edit the display name (display name) and description (desc).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d10f0c2e8e154288a12eb4bbca8baacd~tplv-goo7wpa0wc-image.image) </span>

(2) After completing the batch modification, save the Excel file and upload it.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b1211f5bf604b2e88e61f930aa6a79c~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0c32418dd78440eb037dae68f8b6b98~tplv-goo7wpa0wc-image.image) </span>

(3) After the upload is successful, click Confirm. The display names, descriptions, and so on modified via Excel will be synchronized to the current language environment.
