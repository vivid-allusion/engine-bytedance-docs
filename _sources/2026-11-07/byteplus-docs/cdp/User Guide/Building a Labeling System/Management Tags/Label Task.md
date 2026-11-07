---
title: "Label Task"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Label_Task"
---

<span id="_1-功能概述"></span>
# 1. Function Overview

Supports viewing an overview of all tag tasks, including the running status, duration, operation records, etc., to help users better understand and manage tag tasks globally, improving troubleshooting and operation efficiency of tag tasks.

<span id="_2-使用限制"></span>
# 2. Usage Restrictions


1. Project administrators need to enable the permissions for the corresponding user in **Project Center\-Permissions** to use the **Labeling System** module. Once enabled, users can access this feature.

2. Users need to complete the preparatory work in the **Data Fusion** module and finish label construction before they can view and manage tag tasks in this module.


<span id="_3-功能介绍"></span>
# 3. Feature Introduction

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_381c26fbb0c2a74edc4c7126fe4b9e8d) </span>

①Supports viewing the total number of tag tasks under the current project and the number of tag tasks in various running statuses in the top indicator bar.

②Support viewing tag task information on the list page, including tag name, running period, running status, creator, recent running time, and tag type information.

③Support managing tag tasks, users can set to start running tasks, view running records, and edit tags in the operation bar.

<span id="_4-操作步骤"></span>
# 4. Operation Steps

<span id="_4-1-查看标签任务概览"></span>
## 4.1 View Tag Task Overview

The steps are as follows:


1. Click **Label System\-Task Overview** to enter the function page.


<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_12a967a219097b3f8e42c3eb4c2ce3c8) </span>


2. Users can view the total number of all tag tasks under the current project, the number of tag tasks in each running status in the top indicator bar, the calculation logic is as follows:



|**Operating Status** |**Calculation Logic** |
|---|---|
|Operation data |The total number of label tasks with calculation statuses of "Check Dataset", "Run Data", "Wait for Import", and "Importing". |
|Operation successful |The total number of label tasks with a calculation status of "Success". |
|Operation failed |The total number of label tasks with a calculation status of "Run Failed". |
|Waiting for upstream to be ready |The total number of label tasks with a calculation status of "waiting for upstream to be ready". |
|Other |The total number of label tasks with calculation statuses of "Manually Terminated" and "None" |


<span id="_4-2-查看标签任务列表"></span>
## 4.2 View Tag Task List


1. Users can view tag task information on the **Task List Page**, including:

   * Tag Name: Display the tag name. Click to jump to the tag details page for more information about the tag situation.

   * Running Cycle: Display the frequency of label updates, support filtering by "day, week, month, real\-time, manual", where the running cycle for manual labels is "real\-time".

   * Status: Divided into several task states such as "manually terminated, operation failed, importing, waiting for upstream readiness, running data, operation succeeded, checking dataset, waiting for import, none", and supports filtering.

   * Creator: Display the label creator.

   * Recent Run Time: Display the recent run time of the label status, and support sorting.

   * Label Type: Display how the labels are created, and support filtering.

      <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_6f1140e45e3ed8a4316feeb25d615692) </span>

2. Users can **search** for corresponding label tasks by entering "label name, creator" in the search box to view task information.


<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_52fb9ed0e0d66aed40549af9f898c2d6) </span>

<span id="_4-3-管理标签任务"></span>
## 4.3 Manage Label Tasks


1. Click **Start** to start the task.

2. Click **Run Records** to navigate to the label details page to view detailed operation records.

3. Click **Edit** to go to the label editing page for information modification.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_5c8520834ea25db823a7dbb649f08a82) </span>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Label tasks with an operating cycle of "real\-time" do not support task execution, nor do they support viewing the operation records.</div>


* <div data-tips="true" data-tips-type="warning">The operations of label tasks are affected by label permissions. Only those with label viewing permissions can perform operations such as running tasks and viewing records, and only those with label editing permissions can edit labels.</div>



<span id="_5-特殊情况说明"></span>
# Special Cases Description

When users enable multi\-subject or multi\-environment configurations, please note:

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_aa82cf75e4fdb73c20d8c1843cd77561) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the customer has enabled multi\-environment configuration, the tag task overview can only be used in the testing environment. This function is not available in the formal environment.</div>
