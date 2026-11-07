---
title: "Allocate/transfer resources to the queue"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Allocate-transfer_resources_to_the_queue"
---

In the process of using queues, you may encounter situations where you need to adjust the number of queue resources or transfer some of the queue resources to other queues. This article will explain the relevant operation steps for users.

<span id="相关概念"></span>
# Related concepts


* Queue


<span id="队列的状态"></span>
# State of the queue


|Status |Note |
|---|---|
|Running |The status queue is **created** and the **resource group has not expired** and is in the normal availability phase. This state supports **adding users** , **editing** , **stopping** and **deleting** . |
|Stopped |The queue has been stopped, and the existing tasks using the queue will continue to run, but new tasks cannot be submitted. In this state, **adding users, editing** , **starting** , **matching** , **resource transfer** and **deletion** of the queue are supported. |
|Closed |This status indicates that the **resource group has expired** , and tasks running with the queue will stop immediately, at which point the queue only supports **deletion** . After the resource group where the queue is located is **renewed** , the queue will automatically turn to `running`. |


<span id="使用前提"></span>
# Premise of use


1. There is \> = 1 queue in [Queue].

2. The current user has administrative privileges on this queue.


<span id="队列更配"></span>
# Queue matching

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The status of the queue needs to be <code>stopped</code>.</div>


* <div data-tips="true" data-tips-type="tip">The availability area of the queue is not replaceable and can only be reconfigured in the current availability area.</div>


* <div data-tips="true" data-tips-type="tip">Queues only support GPU instance specifications that contain the same model.</div>


* <div data-tips="true" data-tips-type="tip">The remaining resources in the availability area where the queue is located in the resource group can be freely allocated, and the unused resources in the queue can be downallocated and put back into the resource group.</div>



<span id="操作步骤"></span>
## Procedure


1. \*\*The queue administrator \*\*logs into the Machine Learning Platform and clicks [Resource Group Management] \- [Resource Queues] in the left navigation bar to go to the list page. Click [Resource management] in the operation area of the queue to be matched to enter the matching page.

2. Select the corresponding instance specification on the matching page and adjust the quantity to complete the matching.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54c9a4f63991472faf3c0b20b2081bf3~tplv-goo7wpa0wc-image.image) </span>


&nbsp;


&nbsp;

1. 

2.
