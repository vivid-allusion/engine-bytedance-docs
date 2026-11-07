---
title: "Pipeline status"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Pipeline_status"
---

This article describes the meaning and flow logic of each Status during the execution of a BytePlus CP pipeline, helping you better monitor and manage pipeline Execution status.

<span id="oD20gpAC"></span>
## Background

The Status of a pipeline reflects its entire life cycle from trigger to completion. Understanding the meaning of each Status helps with:


* **Troubleshooting**: Quickly identify the reason why the pipeline is stuck or has failed

* **Optimize efficiency**: Identify resource bottlenecks and adjust the concurrency policy

* **Automate operations**: Set up alerts and notifications based on Status changes


<span id="wmFFjn6k"></span>
## Status description

CP pipelines use an asynchronous scheduling mechanism. After a pipeline is triggered, it goes through multiple stages such as resource scheduling, lock contention, and execution, with each stage corresponding to a different Status.


|**Status** |**API Status** |**Description** |
|---|---|---|
|**In queue** |Enqueued |The pipeline trigger request has been submitted and is waiting for the scheduling system to allocate execution resources. At this time, the pipeline has not yet begun actual execution. |
|**Environment starting** |Dequeued |The pipeline has been removed from the wait queue and is preparing the execution environment or waiting for dependencies to become available. |
|**Waiting for lock** |LockWaiting |The pipeline is waiting to obtain a resource lock to prevent conflicts caused by multiple pipelines concurrently performing actions on the same resources.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Resource lock is a concurrency control mechanism that ensures that at any given time <strong>only one pipeline instance</strong> can access or operate specific shared resources. When multiple pipelines are triggered simultaneously, only the instance that obtains the lock can continue execution, while other instances enter the <strong>waiting for lock</strong> status and wait.</div><br> |
|**Running** |InProgress |The pipeline is running and executing tasks for each stage and step. |
|**Canceled** |Canceling/Canceled |The pipeline has been manually canceled or automatically canceled by the system, execution is terminated, and not all tasks are completed. |
|**Succeeded** |Succeeded |All steps of the pipeline have been executed successfully, with no errors or exceptions occurring, and the overall execution was successful. |
|**Fail** |Failed |A step in the pipeline execution failed or a system error occurred, resulting in overall execution failure. |
|**Environment startup timeout** |Timeout |The pipeline exceeded the configured timeout threshold while waiting for the execution environment to start, and the system automatically terminated the execution. |


<span id="VF4rxLIp"></span>
## Status flow

The Status of a pipeline follows fixed flow rules, forming a complete life cycle from the initial Status to the final Status.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d37851feeb941e8f2d1e377538a10a12.png) </span>

<span id="0ArjasNp"></span>
## View pipeline status


1. Log in to the [Continuous Delivery Console](https://console.byteplus.com/cp).

2. In the left navigation bar, select **workspace** and enter the target workspace.

3. In the left navigation bar, select **pipeline** and click the target pipeline name.

4. In the **Run Records** column, view the status of each instance.


<span id="rOgsNEa9"></span>
## FAQ

For methods to handle abnormal statuses in pipelines, see [Pipeline Status FAQ](https://docs.byteplus.com/en/docs/cp/Pipeline_operation_FAQ).
