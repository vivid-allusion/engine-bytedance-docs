---
title: "priority scheduling strategy"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/priority_scheduling_strategy"
---

The Machine Learning Platform allows users to prioritize custom tasks (and inference services) and schedule the load according to the priority. The specific configuration method is detailed in [Initiate stand-alone/distributed training tasks](https://docs.byteplus.com/docs/mlp/Initiate_stand-alone_distributed_training_tasks)[ ](https://www.volcengine.com/docs/6459/72350). The higher the priority, the more important the task is, and the more you want to obtain resources to complete the task as soon as possible. On the contrary, the chances of obtaining resources for tasks with low priority are relatively low, but this is not absolute. The following will introduce the scheduling strategy implemented by the platform based on priority in detail.

<span id="优先级和创建时间"></span>
# Priority and creation time

The higher the priority number, the more likely it is to be scheduled as early as possible, and the earlier the task is created when the priority is the same, the more likely it is to be called as early as possible.

Scenario example:


* 10:00: Different users in the same queue create custom tasks with the same default priority, excluding all the distractions mentioned below, and these tasks will receive resources from morning to night according to the creation time.

* 11:00: At this time, the creator of a task thinks that queuing for too long will delay the progress, so he contacts the queue administrator to apply to increase the priority of his task, and the administrator approves and increases the priority of the task (even the highest).

* 11:05: The task that was raised in priority receives resources, and other low\-priority tasks or tasks (or other types of payloads) created later in the same priority continue to queue up.


<span id="负载的资源量"></span>
# amount of load resources

When the conditions of high priority and early creation time are met, the load can enjoy the right to be dispatched as soon as possible, but this is not absolute. The default scheduling strategy of the platform is to maximize resource utilization, that is, to exhaust idle resources as much as possible, so tasks with small resource requirements have an inherent advantage in the order of being scheduled.

Scenario example:


* 10:00: There are two tasks A and B with the same configuration (including priority) except for creation time and resource amount. A was created earlier than B. B is a task with a small amount of resources (4c8g), and A has a large resource requirement (8c16g). At this time, the idle resources in the queue are 1c2g, so tasks A and B are queuing up and so on.

* 11:00: The queue's free resources gradually increase to 4c8g as a series of loads run out. From the perspective of priority and creation time, although task A should be scheduled before B, the free resources at this time are only enough for task B to run. In order to maximize resource utilization, task B will run before task A.

   * This scheduling strategy avoids small\-resource tasks from being "starved to death" by high\-quality large\-resource tasks, ensuring resource utilization, but if there are many such small\-resource tasks, it will lead to long\-term queuing of large\-resource tasks (the resource reservation strategy below will solve this problem).


<span id="资源预留"></span>
# resource reservation

As mentioned above, in order to avoid small resource tasks being "starved" by high\-quality large resource tasks, when there are fewer free resources in the queue, lower priority small resource tasks may be scheduled before large tasks. Another extreme may occur when the number of small tasks is large \- small tasks "starve to death" large tasks. In order to solve this problem, the platform supports reserving resources for a certain task. After opening this function, **those with a priority lower than the task will continue to queue up until the task runs, and those with a priority higher than/equal to the task will not be affected.**  **At the same time, the load using idle resources is not affected by resource reservation tasks when scheduling.**  Scenario example:


* 10:00: The queue idle resources are 0, tasks A (4c8g, priority 6), B (1c2g, priority 4), C (2c4g, priority 4), D (1c2g, priority 2) are all in a queued state, and there are no other queued tasks.

* 11:00: A task in the queue ends, and the free resource becomes 1c2g. Since the resource request of task A cannot be met, the lower\-priority task B is scheduled. The queue of idle resources becomes 0 again, and tasks A, C, and D continue to queue up.

* 11:05: The queue administrator starts resource reservation for task A, while tasks A, C, and D continue to queue up.

* 11:10: The queue of free resources becomes 2c4g, which cannot be used for scheduling task C due to resource reservation initiated by task A.

* 11:15: The queue's free resources become 4c8g, and Task A finally has enough resources to be successfully scheduled. The queue of idle resources becomes 0 again, and tasks C and D continue to queue up.

* 11:20: The queue of idle resources becomes 1c2g, and at this time, the scheduling is continued with the strategy of maximizing resource utilization, so the task C with priority 4 continues to queue up, and the priority D with priority 2 is scheduled in advance.


<span id="闲时任务"></span>
# idle task

Custom tasks support using the idle resources of other queues to submit idle tasks in the same resource group dimension to deal with the problem of uneven busy and idle of each queue resulting in low overall resource utilization (support resource sharing between heterogeneous queues, such as the idle tasks of the ml.gni3 queue can call the idle resources of the ml.pni2 queue).

When a non\-idle task queue appears in the queue, the platform will find the appropriate idle task within the scope of the entire resource group and stop it, and use the freed resources to schedule non\-idle tasks. It can be seen that, regardless of the priority of the task itself and the creation time, non\-idle tasks always receive higher priority than idle tasks (although the priority number of non\-idle tasks may be smaller than that of idle tasks).

Assuming that there are both non\-idle and idle tasks with different priority and creation time in the queue, the scheduling order is as follows (from top to bottom):


|Task name |idle time/non\-idle time |priority |creation time |
|---|---|---|---|
|Task A |non\-idle tasks |9 |10 o'clock |
|Task B |non\-idle tasks |9 |11 o'clock |
|Task C |non\-idle tasks |2 |10 o'clock |
|Task D |idle task |4 |10 o'clock |
|Task E |idle task |4 |11 o'clock |
|Task F |idle task |2 |10 o'clock |


<span id="重试高优入队"></span>
# Retry high\-quality entry

Custom tasks with auto\-retry enabled automatically generate an identical task when interrupted. In order to avoid the need for interrupted tasks to take a long time to re\-queue, the platform has opened a high\-quality queue for retried tasks. When the queue's free resources are only available for one of the retry tasks (created successfully) and the normal task, regardless of the priority of the normal task, the successfully created retry task will have priority over the normal task to obtain resources.

In addition, it should be emphasized that after the idle task triggers the retry, it is in the position of high\-quality entry in the idle tasks within the scope of the entire resource group, while the non\-idle task triggers the retry and only does high\-quality entry in the non\-idle tasks in this queue.

Scenario example:


* 10:00: There are task A (with 2c4g of resources and automatic retry enabled) and task B (with 2c4g of resources), both of which have the same priority. At this time, task A is running normally, task B is queued, and the queue of idle resources is 0.

* 11:00: The queue has 0 free resources, task B is still queued, task A is interrupted (2c4g of resources are released) and a new task A1 is automatically generated. At this time, because task A1 enjoys the right to join the team with high excellence, task A1 runs normally, and task B continues to queue up.
