---
title: "Lifecycle"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Lifecycle01"
---

​The lifecycle of a vertical scaling task refers to all the states experienced from task creation to deletion.

During a lifecycle, a vertical scaling task has some fixed states, and state triggers are shown in the following table:


|Task status |State description |
|---|---|
|Running |Indicates that a vertical scaling task is being executed, and the target instance type is being changed. |
|Success |Indicates that a vertical scaling task was executed successfully. |
|Fail |Indicates that a vertical scaling task failed. |
|Waiting |Indicates that a vertical scaling task is waiting to be executed. For scheduled tasks and periodically executed tasks, the task status is **Waiting** before the scheduled execution time is reached. |
|Cancelled |The task status after you manually cancel the vertical scaling task. |
