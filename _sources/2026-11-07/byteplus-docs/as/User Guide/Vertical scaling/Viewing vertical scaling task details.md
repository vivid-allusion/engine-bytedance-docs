---
title: "Viewing vertical scaling task details"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Viewing-the-details-of-a-vertical-scaling-task"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

After a vertical scaling task is executed, you can refer to this topic to view task execution details.

<span id="qb7rdyV4"></span>
## Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the region of your target resource.

3. In the top menu bar, select a region.

4. View task details.

   * In the task list, you can view the task type, trigger type, and the ID of the instance to be modified.

   * Click the task name. On the task details page, you can also view the original and target instance types.

5. View task execution results.

   * For tasks executed immediately:

      * Check the status in the "Task status" column in the task list to see whether the execution succeeded.

   * For tasks executed at a specified time:

      * Check the status in the "Task status" column in the task list to see whether the execution succeeded.

      * If the task status is "Waiting", it means the execution time of the task has not been reached. You can view the execution time in the "Trigger type" column.

   * For tasks executed periodically:

      * Click the task name. On the task details page, you can view the task schedule preview. The preview list displays all subtasks in the cycle. You can check the status in the "Task status" column in the task list to see whether the execution succeeded.
