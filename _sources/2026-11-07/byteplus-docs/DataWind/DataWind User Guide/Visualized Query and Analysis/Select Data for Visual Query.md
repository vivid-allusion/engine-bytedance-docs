---
title: "Select Data for Visual Query"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Select_Data_for_Visual_Query"
---

Visual query allows users to query relevant data content based on existing datasets or by temporarily uploading local files. In the field list area, users can select datasets, view dataset details, and query data from local files. This article describes how to select and view the data needed for visual query.

<span id="47f9ff3b"></span>
# Function overview

Currently, visual query methods are divided into the following two types based on different data sources:


* Query dataset data. For datasets that have already been created, users can select datasets and view dataset details in the field list.

* Query local file data. For temporary offline data query needs, users can click to upload or drag and drop data files in the chart preview area to perform queries.



|Query method |Applicable scenario |Caution |
|---|---|---|
|Query dataset data |Stable, high\-frequency, and reusable data queries |Dataset construction in [Dataset Creation Overview](https://docs.byteplus.com/docs/DataWind/109998) must be completed first |
|Query local file data |Temporary or ad hoc offline data queries |Only quick queries for Excel/CSV files are supported, with a maximum file size of 500 MB |


<span id="_2-功能介绍"></span>
# Query dataset data

<span id="_2-1-切换数据集"></span>
## Select a dataset


1. If the dataset currently being analyzed is not the target dataset, click the dataset name to switch datasets.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2a24e6efb3e4023be7cfca66fadbbf6~tplv-goo7wpa0wc-image.image) </span>

2. After clicking to switch datasets, other target datasets can be selected.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28c3a1652b93446fa6527e248d6c62f2~tplv-goo7wpa0wc-image.image) </span>

   * You can sort and select by recent access (the time when you last opened the dataset), popularity (number of clicks within the project), and latest (creation time).

   * Searching by dataset name and creator is supported.

   * Selecting "Created by me" is supported for quickly filtering datasets created by the user.

   * Selecting "Favorited by me" is supported for quickly filtering datasets favorited by the user.


<span id="_2-2-查看数据集"></span>
## View dataset details


1. To view dataset details, click "View dataset" in the settings to the right of the dataset name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1614ae63e890414f88029552c5fc3bef~tplv-goo7wpa0wc-image.image) </span>

2. Clicking "View dataset" will redirect to the dataset details page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/473ae84dc14740eabd91da5f0894c61f~tplv-goo7wpa0wc-image.image) </span>


<span id="9a59a68a"></span>
# **Query local file data**

Local Excel/CSV files can be quickly queried by clicking to upload or dragging and dropping to upload. The available upload methods differ between the "blank visual query page" and the "visual query page for an existing dataset".


* On the blank visualization query page, both click\-to\-upload and drag\-and\-drop upload methods are supported.

   * Click to upload. Click "Click here or drag files to this page to upload" to upload a local file directly:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c74c3d0f37545babf44b0202f450cf7~tplv-goo7wpa0wc-image.image) </span>

   * Drag\-and\-drop upload. Drag and drop a local file to upload directly:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51cc7b88472d4b5daa0e8a5d47ebbf93~tplv-goo7wpa0wc-image.image) </span>

* On the visualization query page for an existing dataset, only direct drag\-and\-drop of local Excel/CSV files is supported to trigger the quick upload and analysis workflow.

   * Drag\-and\-drop upload. After dragging and dropping a local Excel/CSV file, a confirmation dialog will appear asking whether to switch the dataset.
