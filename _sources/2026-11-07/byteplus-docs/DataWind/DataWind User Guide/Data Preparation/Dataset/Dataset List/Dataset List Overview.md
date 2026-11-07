---
title: "Dataset List Overview"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Dataset_List_Overview"
---

<span id="_1-数据集列表概述"></span>
# 1. Overview of the dataset list

In the dataset list area, you can see three sections: overview, list, and list operations. You can perform management actions such as editing and modifying for each section. This article will introduce the specific operations for the first section, the "Overview" page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb392d5e47a746228845da831eb101f2~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-数据集概览具体介绍"></span>
# 2. Detailed introduction to the dataset overview

<span id="_2-1-数据集搜索"></span>
## 2.1 Dataset search

You can query based on basic information such as dataset name, data source name (base table), owner, and permissions (view, edit, manage).


* Source: You can query datasets output by the visual modeling module or datasets created directly through data connections.

* Type: Query based on whether the dataset is directly connected or extracted.

* Status: You can query the status of the last synchronization for each dataset.


Click the expand button to trigger more filter conditions. This includes dataset category, sensitivity classification, storage type, alert recipient, priority, queue, and execution frequency.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e312e6502c8e40b39122893df11a872a~tplv-goo7wpa0wc-image.image) </span>


* Category: You can select personal datasets, shared datasets, or public datasets.

* Sensitivity classification: You can select all, unclassified, sensitive but not desensitized, sensitive and desensitized, or not sensitive.

* Storage type: You can select different storage types for existing datasets.

* Alert recipient: You can find the corresponding alert recipient by searching for users.

* Priority: You can select all, normal priority, high priority, or ultra\-high priority.

* Queue: You can select all or offline.

* Execution frequency: You can select all, minute\-level, hour\-level, day\-level, week\-level, month\-level, manual, or other.

* Tag: You can select all tags or all tags under the project group.


<span id="_2-2-标签管理"></span>
## 2.2 Tag management

Datasets in a project are often in different business states and need to be identified during use. **For example: deprecated, pending transformation, completed data warehouse construction, and others.**  Through tag management, datasets within a project can be categorized by tags, and the corresponding tags can be displayed in downstream charts and dashboards, enabling readers to quickly identify the status of the data. Tag management consists of three parts: project tag configuration, dataset tagging, and tag display, among which only project administrators can configure tags.

For details, see [Tag Management](https://docs.byteplus.com/docs/DataWind/Tag_Management).

<span id="_2-3-参数管理"></span>
## 2.3 Parameter management

In the parameter management module, users can view public and personal parameters configured in the project, or create new parameters.

A parameter is a variable that can be flexibly adjusted. This variable can be used in calculated fields to implement dynamic logic for a single calculated field or even an entire chart. When a parameter takes different values, the field expression will correspond to different calculation logic.

For details, see .

<span id="_2-4-类目管理"></span>
## 2.4 Category management

**Create project\-level categories,**  which allows unified management of dataset field categories within the project. You can choose to disallow the creation of dataset categories.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af95524c474d4e2985d08f95ee13ba1d~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-5-数据集分类"></span>
## 2.5 Dataset classification

In V2.58.0 and later versions, the dataset module adds two types of dataset classifications: personal datasets and public datasets. Clicking the personal datasets and public datasets folders allows users to select the required type of dataset.

The main value of personal datasets is that users can create personal datasets for analysis without needing to apply for project editing permissions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1f5c9fc860740359151f3f1de6d65eb~tplv-goo7wpa0wc-image.image) </span>
