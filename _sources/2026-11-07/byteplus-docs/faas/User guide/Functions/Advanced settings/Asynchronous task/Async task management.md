---
title: "Async task management"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Async_task_management"
---

This article discusses the basic operations of managing asynchronous tasks, including viewing task status and terminating tasks.

<span id="view-task-status"></span>
## View task status

FaaS records the status change process of each task and provides real\-time query capabilities. After the task is successfully submitted, go to the **Async task** tab to view the execution status of the task. Supports querying the task status of up to the last 24 hours.

An async task currently includes the following statuses:


|**Status name** |**Description** |
|---|---|
|Pending |The task has been submitted and is pending scheduling. |
|Running |The task has been scheduled and is executing. |
|Retrying |Task retry in progress due to a system error. After rescheduling, the task status will change to Running.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, only automatic retries caused by system errors are supported. The first retry interval is 1 s, and subsequent retry intervals will be calculated using binary exponential backoff. That is, retry intervals are 1 s, 2 s, 4 s, 8 s 1 s, 2 s, 4 s, 8 s, and others, up to a maximum retry time of 3 h.</div><br> |
|Succeeded |The task was executed successfully. |
|Failed |The task execution failed. |
|Terminated |The task has been terminated. After manually terminating the call, the task status will change to Terminated. |


<span id="terminate-task"></span>
## Terminate Task

Before the execution of the task ends, supports manually terminating the task at any time. Suitable for scenarios where it's necessary to interrupt function execution prematurely due to function running errors, infinite loops, etc. After terminating the task, the task status will change to Terminated.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">For <strong>Webserver mode</strong> async tasks, after terminating the task:</div>


   * <div data-tips="true" data-tips-type="warning">If multiple concurrent requests per instance are not enabled, FaaS will terminate the request and restart the webserver (business) process.</div>


   * <div data-tips="true" data-tips-type="warning">If multiple concurrent requests per instance are enabled, FaaS will only cancel the corresponding request. Please ensure that the cancellation signals are properly handled in your business logic, such as listening for the cancel signal in Context and terminating the execution of business logic. Otherwise, your business logic may continue to operate after the request has been cancelled, leading to waste of resources or tasks not stopping as expected.</div>


* <div data-tips="true" data-tips-type="warning">For <strong>non\-Webserver mode</strong> async tasks, after terminating a task, FaaS will terminate the corresponding task process.</div>


1. In the **Async task** tab of the target function, select the task ID to be terminated from the task list, and click **Actions** in the**Terminate Call** column.

2. In the pop\-up confirmation box, click **Confirm** to terminate the current task.
