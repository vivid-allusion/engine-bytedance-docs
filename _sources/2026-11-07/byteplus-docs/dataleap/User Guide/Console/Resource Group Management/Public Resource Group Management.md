---
title: "Public Resource Group Management"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/public_resource_group"
---

DataLeap supports two main resource group types: public resource groups and exclusive resource groups. This article explains how to choose and use public resource groups.

After activating the DataLeap product service, you automatically receive public resource groups, including public scheduling resource groups, public computing resource groups, and public data services resource groups.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Since all DataLeap users share the public resource group, resource contention may occur during peak task periods, which can prevent timely task completion. For many tasks or high\-priority assured tasks, purchasing an <a href="https://docs.byteplus.com/en/docs/dataleap/resource_group_management">exclusive resource group</a> is recommended.</div>


<span id="_1-费用说明"></span>
## Fee Description

Public resource groups support the pay\-per\-volume model. For detailed fee descriptions, see [Public resource group billing instructions](https://docs.byteplus.com/docs/dataleap/Billing_Instructions_for_Public_Resource_Group).

<span id="_2-适用场景"></span>
## Applicable Scenarios

Commonly used in test environments, low concurrency, and lower priority task scenarios.

<span id="_3-管理公共资源组"></span>
## Managing Public Resource Groups

After activating DataLeap product service, the system automatically provides public resource groups and displays them in the public resource group management list, with no need for purchase or manual management.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac47616e7f0747cfb4515ea713bad373~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-后续操作"></span>
## Subsequent Actions

Resource groups in the **Running** state can be bound to the corresponding projects and used for different task scenarios.


* Public scheduling resource group: Dispatches tasks to the corresponding engine or resource group for execution through the scheduling resource group.

* Public computing resource group: Provides public computing resources for tasks such as Notebook, Python, and Shell.

* Public Data Services Resource Group: Used for calling data services APIs and querying data.


For detailed operating instructions on binding resource groups to projects, see [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project) and [Modify Project Configuration Information](https://docs.byteplus.com/docs/dataleap/modify_project).
