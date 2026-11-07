---
title: "Dev boxes automatic shutdown rule settings"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Dev_boxes_automatic_shutdown_rule_settings"
---

The queue administrator can set a policy for the automatic shutdown of Dev boxes in the queue

<span id="使用前提"></span>
## Premise of use


* Owns one or more queues and is a queue administrator


<span id="操作步骤"></span>
## Procedure


1. Log in to the Machine Learning Platform and click [Resource Group Management] \- [Queue] in the left navigation bar to enter the list page

2. Click the queue name to enter the details page, click the [Rule Settings] tab, and click "Create New Rule". Currently only one rule is supported.

3. Fill in the relevant parameters on the creation page, the specific parameters are as follows



|Parameter |Parameter Description |
|---|---|
|Rule type |* Select the type of rule, **required** .<br><br>* Support selecting "idle shutdown" and "low utilization shutdown".<br><br>> **Idle shutdown** : that is, Dev boxes will shut down directly when they are idle (idle state refers to no running commands and network connections, while network connections refer to SSH connections or WebIDE connections)<br><br>> **Low utilization shutdown** : When the GPU utilization is lower than a certain threshold, an automatic shutdown notification will be triggered, and the shutdown can be cancelled within half an hour |
|Effective scope |* Select the scope of the rule to take effect, **required** .<br><br>   * GPU Dev boxes<br><br>   * CPU specification Dev boxes<br><br>> Low utilization shutdown only supports GPU specification Dev boxes settings. |
|Trigger rule |* Set trigger rules, **required** .<br><br>   * Idle shutdown: Set the allowed inactivity time according to the specifications, and it will automatically shut down after this time.<br><br>   * Low utilization shutdown: When the maximum utilization rate is not exceeded within the accumulated time period according to the specifications, the automatic shutdown rule will be triggered. |



4. After clicking Submit, you can create a rule for the automatic shutdown of Dev boxes, and the queue administrator can decide whether the rule will take effect at the operation

5. When the user creates a Dev box, if the queue is selected, the Dev boxes will automatically shut down according to the queue rules

6. The number of times the rule has been triggered, please go to the queue details page [Rule Settings] \- "Triggered Times" to view


<span id="注意事项"></span>
## Precautions


* The queue administrator needs to remind the users in the queue to configure the mailbox in advance, and can receive the email notification in time when the rule is triggered.

* Currently only one rule is supported.
