---
title: "Idle-time tasks in prepaid scenarios"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Idle-time_tasks_in_prepaid_scenarios"
---

For the prepaid (annual subscription) scenario, the user purchases the resources in the resource group in the **form of quotas (quotas)**  and divides them into several queues for different services, but different services may be due to uneven busy and idle **As a result, some queues have more quotas for the same time period, while some queues have tight quotas, and a large number of tasks are queued, resulting in resource waste on the entire resource group dimension** .

In order to address the above pain points and improve the overall utilization of resource groups, the Machine Learning Platform provides the following solutions:


* Allows users to lend the idle quota of the queue to other queues in the same resource group for performing idle custom tasks and improving the overall utilization of the resource group.

* When all queues in a resource group are willing to lend quotas, the maximum amount of resources that an idle task can use is the total resources of the resource group.

* In order to avoid the phenomenon of "borrowing and not returning" quotas, when the queue of "lending quotas" has non\-idle tasks queued, the borrowed quotas will be immediately recycled, and the idle tasks using this part of the quotas will be interrupted.


<span id="使用前提"></span>
# premise of use


1. The current user has access to \> = 1 prepaid queue (formerly a proprietary queue).

2. There are \> = 1 prepaid queues in the resource group with **free resource lending** open.

   * When this queue has enough free quotas, idle tasks can be created without the need for other queues to start lending.


<span id="使用步骤"></span>
# Procedure


1. The user logs into the Machine Learning Platform and refers to the steps for [Initiate stand-alone/distributed training tasks](https://docs.byteplus.com/docs/mlp/Initiate_stand-alone_distributed_training_tasks) to complete the configuration of the relevant fields in the task creation form.

2. Select the prepaid queue for which the current user has permissions.

3. Configure the **switch to use idle resources** to `turn on`, and submit the form to complete the task creation.

   * Since idle tasks may be interrupted due to quota collection, it is strongly recommended that users include a checkpoint mechanism in the code, so that after the task is killed, they can resume the previous training through checkpoint when the next scheduling is successful.

   * In order to detect the timing of the task being killed in time, please complete the configuration of the mailbox in [Account Management], and the system will automatically send an email to notify the user when the task is killed.

4. Configure computing resources for the task.

   * Since idle tasks can use quotas for other queues, the user's selection of instance specifications will not be limited by the **total amount of resources in this queue** and the **upper limit of personal usage** , as long as the resource limit of the resource group is not exceeded.

      * **Restriction I** : If the GPU model in this queue is V100, only V100 resources in the resource group can be selected when creating idle tasks.

      * **Limit II** : If no GPU resources are allocated in this queue, the GPU resources in the resource group cannot be selected when creating an idle task.

5. After the idle task is created, **when the quota queue has enough free quotas, the idle task can be successfully scheduled** , and the usage of this part of the temporary quota is displayed in the details page of this queue.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d82c2a8c4b14d5a9ac9e1c88b3524e9~tplv-goo7wpa0wc-image.image) </span>


6. When a non\-idle task submitted in the queue that borrows quotas is queued, the platform will collect quotas for the queue to ensure the scheduling of this part of the task.

   * When an idle task is recycled, the task creator receives the corresponding notification email.

   * The [Timeline] page in the recycled task details page can be found that the task is marked as "Preempted".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69748c1b94884a3fb8e84d8ff350473e~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54d2cb5113f04a3ab55e338a89027705~tplv-goo7wpa0wc-image.image) </span>
