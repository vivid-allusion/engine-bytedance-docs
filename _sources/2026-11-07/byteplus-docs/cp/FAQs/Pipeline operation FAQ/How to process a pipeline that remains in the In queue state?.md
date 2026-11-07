---
title: "How to process a pipeline that remains in the In queue state?"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/How_to_handle_a_pipeline_that_remains_in_the_In_queue_state"
---

<span id="jeJyy7LE"></span>
## Issue description

When viewing pipeline execution records in the CP Continuous Delivery Console, you may find that the pipeline remains in the **In queue** state for an extended period and does not proceed to the next stage.

<span id="c3Kuzasv"></span>
## Cause

A pipeline in the **In queue** (Enqueued) state means the execution request has been submitted but has not yet been allocated execution resources by the Scheduling System. Possible reasons include:


|**Reason** |**Description** |
|---|---|
|**Insufficient public resource pool concurrency quota** |The number of pipelines running concurrently in the current workspace has reached the limit. Newly triggered pipelines will need to wait. |


<span id="wq1cSYYH"></span>
## Solution

<span id="jQP5EYHz"></span>
### Check the concurrency quota usage of the public resource pool.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For the maximum number of concurrent pipelines, see <a href="https://docs.byteplus.com/en/docs/cp/Limit">limit</a>.</div>



1. Log in to the [CP Continuous Delivery Console](https://console.byteplus.com/cp).

2. Go to the target workspace and view the **Resource overview** at the top of the page.

3. Confirm whether the number of currently running pipelines has reached the quota limit.

4. If the limit is reached, promptly clean up or terminate idle or redundant pipeline tasks to restore the running quantity within the quota limit and ensure normal pipeline execution.
