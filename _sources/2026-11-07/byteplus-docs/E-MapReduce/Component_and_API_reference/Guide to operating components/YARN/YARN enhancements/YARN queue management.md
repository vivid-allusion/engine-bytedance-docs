---
title: "YARN queue management"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/YARN_queue_management"
---

The Volcano Engine E\-MapReduce (EMR) console supports visual management of YARN cluster queue resources, including common scenarios such as adding queues, renaming queues, deleting queues, changing hierarchy, adjusting capacity, and starting or stopping queues.

<span id="_1-前提条件"></span>
## 1 Prerequisites


1. A cluster type that includes the YARN service has been created, and the EMR version is higher than 3.4.1 / 2.3.1. See [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. The YARN scheduler must use Capacity Scheduler.


<span id="_2-具体功能"></span>
## 2 Features

<span id="_2-1-进入-yarn-队列管理"></span>
### 2.1 Access YARN queue management


1. Log in to [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. Click **Cluster management \> Cluster list \> Cluster name** in the right navigation bar to enter the cluster details page.

3. On the cluster details page, click the **Service list** tab to access the YARN service management page.

4. On the YARN service management page, click the **Queue management** tab to access queue management.

5. Queue list:

   Tree\-structured queue objects are generated based on the current queue configuration. The queue hierarchy is displayed using indentation and collapsing, making it easy to quickly locate queues at specific levels.

   For each queue node, key information such as **status, queue capacity, and maximum capacity** is displayed. Convenient operation shortcuts are also provided, allowing you to quickly **edit** and **manage subqueues** based on this node.


<span id="_2-2-添加队列"></span>
### 2.2 Add queue


1. On the queue management page, click the **Add queue** button on the right to add a new queue.

2. In the add queue pop\-up window, perform the following configuration steps:

   * Select parent queue: You can select any node at any hierarchy level here, then add or adjust subqueues based on that node.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">When adding a sub\-queue to a leaf node, you must ensure that there are no running tasks on the original leaf node, and that it will not be used as a target queue for submissions in the future; otherwise, tasks will fail.      </div>
      

   * Add queue: Click the **Add queue** button. In the new empty row that appears below, you can configure queue information and also enable, disable, or delete the queue:

      * Queue name: Enter the queue name. Only letters and numbers are allowed for queue names.

      * Capacity percentage: Enter the capacity percentage for the new queue. YARN requires that the total capacity of queues at the same hierarchy level adds up to 100.

      * Maximum capacity ratio: When the queue is sufficiently idle, the maximum capacity ratio allows YARN to schedule resources exceeding the preset capacity ratio to this queue. This value must be at least the "capacity ratio."

      * Status: Can control whether this sub\-queue is enabled.

      * Action: Click the **Delete** button to delete the sub\-queue.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">When deleting a sub\-queue, you must ensure that <code>at least one sub-queue is retained under the root queue</code>; after the deletion operation, you need to restart the ResourceManager for the deletion to take effect.      </div>
      

3. After completing queue operations, click the **Confirm** button to submit the changes. You must restart ResourceManager for the current modifications or newly added queues to take effect.


<span id="_2-3-编辑队列"></span>
### 2.3 Edit queue

For non\-root queues, in the **Action** column of the queue list, click the **Edit** button in the pop\-up window to edit the queue.

In the edit queue pop\-up window, you can modify the **queue name, maximum capacity ratio, and queue status**.

However, for the queue capacity ratio, since the total capacity of queues at the same level must be considered, you can click the **Go to Modify** button on the right to quickly navigate to the **Add Queue** window for overall capacity editing.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After editing and modifying the queue:</div>



* <div data-tips="true" data-tips-type="tip">If the changes involve adding a new queue, changing the queue name, or deleting a queue, you must restart the ResourceManager for the changes to take effect.</div>


* <div data-tips="true" data-tips-type="tip">If the changes involve capacity or queue status, you need to perform a Refresh Queue operation for the changes to take effect.</div>



<span id="_2-4-子队列管理"></span>
### 2.4 Sub\-queue management

In the queue management list, in the **Action** column, click the **Sub\-queue Management** button to quickly locate this node as the parent queue and perform sub\-queue addition and modification operations under it.

<span id="_2-5-refresh-queue"></span>
### 2.5 Refresh Queue

Except for scenarios where renaming, adding, or deleting queues requires restarting ResourceManager, if only the queue capacity or queue status is changed, you can simply use `Refresh Queue` to apply the changes.


1. Click the **Refresh Queue** button.

2. In the pop\-up window, select the range of machines for execution; all are selected by default.

3. After adding operation notes, click the **Confirm** button to submit the operation. You can view the specific execution results in the operation history.


<span id="_2-6-队列监控"></span>
### 2.6 Queue monitoring

In addition to queue configuration management, we also provide comprehensive monitoring charts for the queues themselves, making it easy to monitor the operation of YARN cluster queues.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To learn more about cluster monitoring features, refer to the documentation: <a href="https://docs.byteplus.com/docs/E-MapReduce/105449">Overview</a></div>



1. Click the **Service Monitoring** icon at the top of the queue management interface.

2. In the YARN metric categories shown in the dropdown list, select the YARN\-QUEUE category to access the cluster monitoring interface.


The following table lists the currently supported queue metrics.


|**Group** |**metric name** |**Unit** |
|---|---|---|
|Application count |Number of submitted apps in YARN queue |Count |
||Number of suspended apps in YARN queue |Count |
||Number of running apps in YARN queue |Count |
||Number of completed apps in YARN queue |Count |
||Number of killed apps in YARN queue |Count |
||Number of failed apps in YARN queue |Count |
||Number of active apps in YARN queue |Count |
||Number of running jobs in YARN queue with runtime less than 60 minutes |Count |
||Number of running jobs in YARN queue with runtime between 60 and 300 minutes |Count |
||Number of running jobs in YARN queue with runtime between 300 and 1,440 minutes |Count |
||Number of running jobs in YARN queue with runtime greater than 1,440 minutes |Count |
|Memory size |Allocated memory size in YARN queue |Bytes(IEC) |
||Available memory size in YARN queue |Bytes(IEC) |
||Pending memory size in YARN queue |Bytes(IEC) |
||Reserved memory size in YARN queue |Bytes(IEC) |
|VCore count |Number of allocated VCores in YARN queue |Count |
||Number of reserved VCores in YARN queue |Count |
||Number of available VCores in YARN queue |Count |
||Number of pending VCores requested in YARN queue |Count |
|Number of containers |Number of allocated containers in YARN queue |Count |
||Number of pending containers in YARN queue |Count |
||Number of reserved containers in YARN queue |Count |
||Total number of allocated containers in YARN queue |Count |
||Total number of released containers in YARN queue |Count |
||Total number of preempted containers in YARN queue |Count |
|User count |Number of active users in YARN queue |Count |
