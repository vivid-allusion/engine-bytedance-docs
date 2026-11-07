---
title: "Description of common reasons for the status in the load queue"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Description_of_common_reasons_for_the_status_in_the_load_queue"
---

When the load in the current queue appears `in the queuing`state, there may be a variety of reasons. The following lists will explain which reasons may cause the load to be `in the queuing`state.

<span id="常见问题"></span>
# FAQs


|reason classification |Detailed description |
|---|---|
|Resource fragmentation |When the fragmentation phenomenon occurs in the resource group, it will cause the queue to have quotas but the load is `in the queued`state. At this time, you can see the prompt content in the load `queued`state:<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">There are quotas in the current queue, and there may be fragmentation issues. You can observe whether the queue is enabled for GPU defragmentation (for GPU resources only). You can also contact the resource group administrator to see if the node load panel is fragmented. (Only for GPU resources)</div><br> |
|There is a task to open resource reservation |When there is a task in the queue to start resource reservation and the task priority is higher than the current load, the queue has a quota, but the task is `in the queue`state. At this point you can see the prompt content `in the queue`status:<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">There is currently a high\-priority task resource reservation. You can choose to continue waiting for other resources to be released or turn the task into an idle task to borrow other queue resources (queues that support lending idle resources), but the task is created as an idle task. There is a risk of being preempted at any time.</div><br> |
|The personal remaining quota is not met |In "Queue Management" \- "Users in a Group", you can set the upper limit of the personal quota usage ratio for each user individually, so when the personal quota resource usage is insufficient, it will appear `in the queue`. At this point you can see the prompt content `in the queue`status:<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The current personal quota usage is insufficient. You can contact the queue administrator to adjust the upper limit of the usage ratio in "Queue Management \- Users in the Group". You can also choose to continue waiting for resource release or change the task to an idle task to borrow other queue resources (queues that support lending idle resources), but there is a risk of being preempted at any time after the task is created as an idle task.</div><br> |
|Queue remaining quota not met |When there are no remaining available quotas in the queue, the load is `queued`, and you can see the prompt content in the load `queued`status:<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The remaining quota of the current queue is insufficient. You can choose to continue waiting for resource release or change the task to an idle task to borrow other queue resources (queues that support lending idle resources), but there is a risk of being preempted at any time after the task is created as an idle task.</div><br> |
|Resource group remaining quota not met |When there are no remaining available quotas in the resource group, even if the task is idle, the task will be `queued`. At this point you can see the prompt content `in the queue`status:<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The quota in the current resource group is occupied and cannot be released. You can change the task to a non\-idle task to preempt or continue to wait for the resource to be released.</div><br> |


**Examples are as follows:** 

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4bc2e4d4b8dfd1e8b04f3aa3937a82a9.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">GPU defragmentation related operation instructions can refer to GPU defragmentation rule settings<a href="https://docs.byteplus.com/docs/mlp/GPU_defragmentation_rule_settings">GPU defragmentation rule settings</a></div>


* <div data-tips="true" data-tips-type="tip">How to view and transfer the fragmented load can refer to the node load details<a href="https://docs.byteplus.com/docs/mlp/Node_load_details">Node load details</a></div>



<span id="特例问题"></span>
# special case problem


|Problem classification |Detailed description |
|---|---|
|pure CPU task |When a pure CPU task is fragmented, it will occupy the queue Quota and not release it, blocking subsequent tasks from joining the queue.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can adjust the priority of the current task to bypass quota\-based pure CPU tasks</div><br> |
