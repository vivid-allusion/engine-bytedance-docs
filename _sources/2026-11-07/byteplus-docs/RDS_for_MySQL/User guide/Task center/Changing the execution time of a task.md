---
title: "Changing the execution time of a task"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_the_execution_time_of_a_task"
---

For tasks planned in the maintainable time period, you can postpone their execution time. This article introduces the steps to modify the task execution time.

<span id="prerequisites"></span>
## Prerequisites

The task is in the **waiting for execution** state.

<span id="steps"></span>
## Steps


1. Log in to [Cloud Database MySQL version console](https://console.volcengine.com/db/rds-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project to which the instance belongs is not set, the project should be selected for this operation as <strong>Account All Resources</strong>.</div>



3. In the left navigation bar, click **Task Center** to enter the **Task** list.

4. In the **Task** list, click the **Modify execution time** button in the **Operation** column of the target task.

5. In the pop\-up **Modify Execution Time** window, select **Execution Mode**.

* Immediate execution: Advance tasks in the maintainable time period to the current immediate execution.

* Specify a time point: You can select a time within 7 days after the current time point.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can view the maintenance period currently set for the instance on the <strong>Instance Information</strong> page. If you need to adjust, please see <a href="https://www.volcengine.com/docs/6313/171477">Setting the maintainable time period</a>.</div>
