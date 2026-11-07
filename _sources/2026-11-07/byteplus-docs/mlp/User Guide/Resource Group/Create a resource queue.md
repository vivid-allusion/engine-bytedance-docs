---
title: "Create a resource queue"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Create_a_resource_queue"
---

A resource group can be divided into several queues, each of which contains a partial quota allocated from the resource group, and users use the quota to create workloads (Dev boxes, training tasks, inference services).

<span id="相关概念"></span>
# Related concepts


* Resource Group

* Queue

* IAM


<span id="使用前提"></span>
# Premise of use


1. The current user has `MLPlatformAdminAccess`IAM policies (see [rights management](https://docs.byteplus.com/docs/mlp/54011)b for how to configure policies).

2. There is \> = 1 resource group in [Resource Group].


<span id="操作步骤"></span>
# Procedure


1. Log in to the Machine Learning Platform and click Resource Group Management in the left navigation bar to go to the listing page.

2. Click [Create Queue] in the operation area of the corresponding resource group to enter the creation page. Or go to the details page of the resource group and click [Create Queue] at the top right to enter the creation page.

3. Fill in the relevant parameters on the creation page, the specific parameters are as follows:



|**Parameter** |**Parameter Description** |
|---|---|
|Resource Group |Select a resource group for creating the queue, **required** . |
|Concept |* Fill in the name of the queue. Required.<br><br>* Supports 1 to 200 visible characters, and only includes uppercase and lowercase letters, Chinese, numbers, dashes, and underscores. |
|Description |* Fill in the appropriate description of the queue, **optional** .<br><br>* Supports 1 to 500 visible characters. |
|administrator |* Select the administrator in the queue, **optional.** <br><br>* The queue creator defaults to the administrator of the queue. |
|load type |* Select the payload type supported by the queue, **required** .<br><br>* When multiple types are checked, the queue can be used to simultaneously submit payloads of the corresponding type. |
|Availability Zone |* Select to divide resources into queues from an Availability Zone of a resource group, **required** .<br><br>* Each queue only supports resource partitioning from a single Availability Zone. |
|calculation specification |* Configure the instance size and number of queues, **required**.<br><br>* The maximum number that can be selected for each instance specification does not exceed the remaining amount of the current specification in the Availability Zone.<br><br>* **Only GPU instance specifications of the same type are supported in a queue** . |



4. After completing the above configuration, click [Confirm Creation] in the lower right corner to complete the creation of the queue in the resource group. Subsequent **queue administrators** can manage queues on the Queues list/details page.

5. If you need to obtain the queue ID to submit a training task using a command\-line tool, you can view the queue ID in the queue name area on the list page or in the queue details page.
