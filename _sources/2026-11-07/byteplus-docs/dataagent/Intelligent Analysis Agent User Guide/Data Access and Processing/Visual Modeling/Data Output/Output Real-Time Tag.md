---
title: "Output Real-Time Tag"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Output_Real-Time_Tag"
---

<span id="_1-概述"></span>
# 1. Overview

If you have also purchased the Volcano Engine VeCDP product, you can view and use the "Output real\-time tag" operator in the data intelligence visual modeling module, under the output operator category. If not purchased, this operator will not be visible. The Output real\-time tag operator allows you to output data to the tag system, supports custom processing pipelines, and outputs the results to tags.

<span id="_2-功能介绍"></span>
# 2. Features

<span id="_2-1-添加“输出实时标签”"></span>
## 2.1 Add "Output real\-time tag"

In real\-time modeling tasks within visual modeling, click the operator add button to see "Output real\-time tag" under the output operator category, then click to select it.

<span id="_2-2-配置“输出实时标签”"></span>
## 2.2 Configure "Output real\-time tag"

As shown in the figure above, after the user clicks to add the "Output real\-time tag" operator, specific operations can be performed for the target subject, tag configuration, advanced configuration, and more. The definitions of each configuration item are as follows:

 **(1) Target subject**

Subject: The profile subject in CDP, which refers to the target object of ID\-Mapping OneID.

 **(2) ID\-Mapping type**

A. **Real\-time conversion**: Based on the ID type's corresponding ID type field data, the ID\-Mapping service queries in real time for an existing One\-ID (that is, the reference ID BaseID). If it is a completely new ID, meaning it has never participated in One\-ID (reference ID BaseID) generation, then the One\-ID (reference ID BaseID) data cannot be found.

B . **Real\-time generation**: Based on the ID type's corresponding ID type field data, the ID\-Mapping service participates in the generation of ID\-Mapping OneID in real time. If a One\-ID (reference ID BaseID) has already been generated historically, it will be queried directly; if it is a completely new ID, the ID\-Mapping service will generate a new One\-ID (reference ID BaseID). The One\-ID (reference ID BaseID) can be used across all CDP product features. For detailed generation strategies, refer to CDP [Data Integration \- ID Graph Construction \- Real\-time OneID Generation Strategy].

Note: Real\-time generation of ID\-Mapping will affect the usage of all subject data within CDP and is only supported for group administrators.

 **(3) ID type and associated fields**


* **ID type**: The ID Code for a certain type of ID of the subject in the ID\-Mapping graph. For details, refer to CDP [Data Integration \- ID Graph Construction \- ID Type Settings];

* **ID\-type field**: Select the field in the operator's input data source that corresponds to the ID\-Mapping ID type as the data input.


 **(4) Tag configuration**

Tag configuration: After a tag is submitted, the relevant tag will be automatically constructed in the tag system, and it will take effect only after the task is saved. Tag field: Please select the field name to be defined as a tag. Currently, special field types such as Map are not supported.

Tag name: Please define a name for the tag that can be easily understood, either in Chinese or English.

Tag description: Please define a description for the tag that can be easily understood. Online service: When enabled, the tag can be used to query relevant data in the high\-speed OpenAPI, enabling high\-concurrency queries.
