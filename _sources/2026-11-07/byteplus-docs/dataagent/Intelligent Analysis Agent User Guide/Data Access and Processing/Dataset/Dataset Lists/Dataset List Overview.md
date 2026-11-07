---
title: "Dataset List Overview"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Dataset_List_Overview"
---

<span id="_1-数据集列表概述"></span>
# 1. Dataset list overview

In the dataset list area, you can see three sections: overview, list, and list operations. You can perform management actions such as editing, modifying, and other operations for each section. This article will introduce the specific operations of the first section, the "Overview" page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fdd49aac48cf4ab39ad03de9e9c532b6~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-数据集概览具体介绍"></span>
# 2. Detailed introduction of the dataset overview

<span id="_2-1-数据集搜索"></span>
## 2.1 Dataset search

Supports queries based on basic information such as dataset name, data source name (base table), owner, and permissions (view, edit, manage).


* Source: You can query datasets output by the visual modeling module or datasets created directly through data connections.

* Type: Query based on whether the dataset is directly connected or extracted.

* Status: You can query the status of the last synchronization for each dataset.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b6a13a56d6b4ec28e50e1e3cd7b8910~tplv-goo7wpa0wc-image.image) </span>

Click Filter to access more filtering options. These include dataset category, sensitivity classification, storage type, alert recipient, priority, queue, and execution frequency.


* Dataset category: You can select personal datasets, shared datasets, or public datasets.

* Storage type: You can select different storage types for existing datasets.

* Alert recipient: You can search for users to find the corresponding alert recipient.

* Priority: You can select all, normal priority, high priority, or ultra\-high priority.

* Queue: You can select all or offline.

* Execution frequency: You can select all, minute\-level, hour\-level, day\-level, week\-level, month\-level, manual, or other.


<span id="_2-2-标签管理"></span>
## 2.2 Tag management

Datasets in a project are often in different business states and need to be identified accordingly during use. **For example: deprecated, pending transformation, completed data warehouse construction, and more.**  Through tag management, you can categorize datasets in the project according to tags, and display the corresponding tags in downstream charts and dashboards. This helps readers quickly understand the data status. Tag management consists of three parts: project tag settings, dataset tagging, and tag display. Only project administrators can configure tag settings.

For details, see [Tag Management](https://docs.byteplus.com/docs/457/106420).

<span id="_2-3-参数管理"></span>
## 2.3 Parameter management

In the parameter management module, users can view public and personal parameters already configured in the project or create new parameters.

A parameter is a variable that can be flexibly adjusted. This variable can be used in calculated fields to implement dynamic logic solutions for a single calculated field or even an entire chart. When a parameter takes different values, the field expression will correspond to different calculation logic.

For details, see [Parameter Management](https://docs.byteplus.com/docs/457/106464).

<span id="_2-4-类目管理"></span>
## 2.4 Category management

**Create project\-level categories**, which enables unified management of dataset field categories within the project. You can choose to disallow the creation of dataset categories.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79dcb71bc9e544d2b7682d971f8d3cdd~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-5-数据集分类"></span>
## 2.5 Dataset classification

The dataset module includes four types of dataset classifications: personal datasets, public datasets, shared with me, and official datasets. Click each folder to select the types of datasets you need.

The main value of personal datasets is that users can create personal datasets for analysis without applying for project editing permissions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c91aee9db3a4b7587418741d12960f9~tplv-goo7wpa0wc-image.image) </span>
