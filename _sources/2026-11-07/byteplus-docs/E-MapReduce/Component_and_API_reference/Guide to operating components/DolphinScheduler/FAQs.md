---
title: "FAQs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ds_faqs"
---

<span id="任务卡在“正在执行”，看不到报错；任务执行停止，始终显示停止中"></span>
## Task stuck at "In progress", no error visible; task execution stops, but the status remains "Stopping"


* Description of the phenomenon: The task is stuck; checking the master\-server logs shows the following error:


[ERROR] 2023\-03\-16 18:01:29.170 +0800 org.apache.dolphinscheduler.server.master.runner.WorkflowExecuteRunnable:[697] \- [WorkflowInstance\-0][TaskInstance\-0] \- Start workflow error

java.lang.NullPointerException: null


* Root cause analysis: The resources bound to the workflow were deleted, but resource_ids were not updated.

   * Open source [bug-13583](https://github.com/apache/dolphinscheduler/issues/13583)

   * Open source[bug-13635](https://github.com/apache/dolphinscheduler/issues/13635)

* Solution: Connect to the Dolphin metadata database and set the resource_ids of the corresponding workflow in the t_ds_task_definition table to NULL.


Furthermore, it is not recommended to delete resources during subsequent use.
