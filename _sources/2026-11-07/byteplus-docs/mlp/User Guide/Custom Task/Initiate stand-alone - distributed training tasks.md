---
title: "Initiate stand-alone/distributed training tasks"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Initiate_stand-alone_distributed_training_tasks"
---

[Custom Training] In addition to supporting stand\-alone training tasks, it also presets configuration templates for various distributed training paradigms such as TensorFlowPS, PyTorchDDP, BytePS, etc. Users can initiate large\-scale distributed training tasks after simply configuring the number of training roles and instance specifications.

<span id="使用前提"></span>
# premise of use


1. When using a prepaid (proprietary) queue, you have access to \> = 1 prepaid queue.


<span id="操作步骤"></span>
# Procedure

The platform supports the initiation of training tasks through the console (Web page) and command\-line tools. The steps for each approach are described below.

<span id="控制台"></span>
## console


1. Log in to the Machine Learning Platform and click [Model Training] \- [Custom Training] in the left navigation bar to enter the list page.

2. Click [+ Create Custom Training] at the top left of the list page to enter the creation page.

3. Fill in the relevant parameters on the creation page, the specific parameters are as follows:



|Parameter |Parameter Description |
|---|---|
|Task name |* Fill in the name of the training task. **Required** .<br><br>* Supports 1 to 200 visible characters, and only includes uppercase and lowercase letters, Chinese, numbers, dashes, and underscores.<br><br>* By default, the name of compliance is generated, and the user can modify it according to the specification. The name can be repeated. |
|Description |* Fill in the appropriate description of the training task. **Optional** .<br><br>* Supports 1 to 500 visible characters. |
|label |* Fill in the task label. **Optional** .<br><br>* Supports 1 to 100 bits of visible characters, including only uppercase and lowercase letters, Chinese, numbers, dashes, underscores, and no symbols are allowed to start. |
|visible range |* Configure which account ranges this task can be visible in. **Optional** .<br><br>* Visible in the main account: All users under the main account can view the task and details.<br><br>* Members of the queue are visible: Users with privileges on the queue to which the task belongs can view the task and its details.<br><br>* The specified sub account is visible: the user in the specified account list has permission to view the task and details.<br><br>* Only the creator is visible: Only the task creator has permission to view the task and its details. |
|mirror image |* Select the mirror image for the training task. **Required** .<br><br>* Supports `preset images`, `custom images`, `BytePlus images`and `public images`(private Container Registry requires a username and key). |
|source code |* Upload the training code. **Optional** .<br><br>* Supports uploading a single file or directory to a specified directory in a container (default is `/root/code`).<br><br>   * Only 10,000 files are supported, a single file is within 100MB and the total file is within 2GB, otherwise use the [command line tool ](https://docs.byteplus.com/en/docs/mlp/Use_documents)to initiate training.<br><br>   * When the code contains a .gitignore file, it will be filtered against that file.<br><br>* **Since the code will be uploaded to the Torch Object Storage TOS, please refer to** [Open related services](https://docs.byteplus.com/docs/undefined/67e2926dbafc26050d8f9fe0#%E5%BC%80%E9%80%9A%E7%9B%B8%E5%85%B3%E6%9C%8D%E5%8A%A1)[ ](https://www.volcengine.com/docs/6459/76345#%E5%BC%80%E9%80%9A%E7%9B%B8%E5%85%B3%E6%9C%8D%E5%8A%A1)**to grant Machine Learning Platform access to the user's TOS with one click before uploading the code.**  |
|Entry command |* Fill in the start command for the task. **Required** .<br><br>* Distributed training tasks usually have special environment variables and entry commands, see [Initiate TensorFlowPS distributed training](https://docs.byteplus.com/docs/mlp/Initiate_TensorFlowPS_distributed_training), [Initiate PyTorchDDP distributed training](https://docs.byteplus.com/docs/mlp/Initiate_PyTorchDDP_distributed_training)[ ](https://www.volcengine.com/docs/6459/75222), [Initiate MPI distributed training](https://docs.byteplus.com/docs/mlp/Initiate_MPI_distributed_training)[ ](https://www.volcengine.com/docs/6459/75224). |
|Parameter |* Fill in the additional parameters of the entry command. **Optional** .<br><br>* This parameter will be spliced after the entry command. |
|environment variables |* The environment variables that will be injected into the training container. **Optional** .<br><br>* The key values of environment variables only support uppercase and lowercase letters, numbers, underscores, and cannot begin with a number.<br><br>* Configuration of up to 20 environment variables is supported.<br><br>* Supports specifying that an environment variable is visible only to the creator. |
|TensorBoard |* Select whether to collect TensorBoard logs. **Optional** .<br><br>* After opening, the user needs to write code to write the log to the corresponding address of the environment variables `TENSORBOARD_LOG_PATH`, and then start TensorBoard on the list page/details page of the task to view the corresponding log. |
|queue |Select the queue on which to run the task. You can refer to the "Resource Groups" section in the related concepts for configuration. **Required** . |
|priority |* Configure the priority of the task. **Optional** .<br><br>* The full range of priority is 1 to 9, and the **larger the value, the higher the priority** . Submit tasks only support part of the gear, the queue administrator can freely adjust the priority of the queued custom tasks in the task list (including the task list on the queue details page), in addition to making resource reservations for the task to avoid the problem of frequent queuing of high\-quality and large\-resource tasks with small amounts of resources. See the [priority scheduling strategy](https://docs.byteplus.com/docs/mlp/priority_scheduling_strategy)[ ](https://www.volcengine.com/docs/6459/1175114)for details.<br><br>* For all queued loads (including Dev boxes, custom tasks, and inference services) in the same queue, the platform will attempt to schedule according to the order of priority from high to low and creation time from early to late, and determine the final scheduling order according to the actual resource situation. **The basic guarantee is that under sufficient resources and the same priority, the tasks submitted first are scheduled first** .<br><br>* Supports queue administrators to configure default priorities for various types of payloads at the queue level.<br><br>   * For example, configure the default priority of Dev boxes to 5 and custom tasks to 4. Without adjusting the priority, Dev boxes created by default will always obtain resources before custom tasks created by default. |
|Utilize leisure resources |* Whether to allow tasks to use the idle resources of each queue (preemptible switch). **Optional** .<br><br>* Idle tasks can use the idle resources lent by each queue, reduce the queuing time to a certain extent, and improve the overall resource utilization. See [Idle-time tasks in prepaid scenarios](https://docs.byteplus.com/docs/mlp/Idle-time_tasks_in_prepaid_scenarios)[ ](https://www.volcengine.com/docs/6459/147996). |
|instance configuration |* Configure training templates and instance specifications. **Required** .<br><br>* Support `TensorFlowPS`, `PyTorchDDP`, `MPI`, `BytePS`several distributed training paradigms, specific configuration details see [Initiate TensorFlowPS distributed training](https://docs.byteplus.com/docs/mlp/Initiate_TensorFlowPS_distributed_training), [Initiate PyTorchDDP distributed training](https://docs.byteplus.com/docs/mlp/Initiate_PyTorchDDP_distributed_training)[ ](https://www.volcengine.com/docs/6459/75222), [Initiate MPI distributed training](https://docs.byteplus.com/docs/mlp/Initiate_MPI_distributed_training) ,<br><br>* Each instance specification includes specific CPU, memory, GPU quantities, and unit price.<br><br>* One type of GPU corresponds to a layer of rich CPU and memory specifications to choose from, providing users with the highest possible flexibility while improving resource utilization. |
|Maximum running time |* The longest run of the task. **Optional** .<br><br>* When the configuration is different from the long\-duration task configuration in the resource group, take the smaller of the two. When filled in `0`, the function is turned off, that is, the program always runs without error.<br><br>   * For example, if the task is configured to run for a maximum of `1`hour when creating the task, and the resource group is configured to run for `2`hours, the task will be stopped after `1`hour of operation. |
|instance retention time |* The retention duration of the instance container. **Optional** .<br><br>* When an instance fails or succeeds, the corresponding container can be retained for a period of time, so that the container can be located through WebShell.<br><br>   * For example, when creating a task, configure the retention time to be `5`minutes. When the instance fails to run, it will enter the state of `failure (reservation)`. In the next `5`minutes, it is allowed to enter the container through WebShell. After `5`minutes, the instance turns to the `failed`state. At this time, the WebShell entrance will be closed. |
|environmental diagnosis |* After this configuration is turned on, when the environment fails to run, the current task environment health status diagnosis will be automatically triggered. **Optional** .<br><br>* Diagnostics are expected to take some time to verify the availability and stability of the environment. Single machine testing is expected to take 5\-10 minutes, and multi\-machine testing is expected to take 15\-20 minutes.<br><br>* The results of environmental diagnostics can be viewed through the diagnostic flag in the list or through diagnostic events. The result of the diagnostic failure will not affect the running status of the task. |
|process inspection |* It supports continuously checking the number of `Python`processes during the stable operation of the task to determine whether the task is abnormal. It is recommended that you use it in the training task of the larger model. **Optional** .<br><br>* You can set the `inspection time`according to the operation of the task, and the platform will trigger the inspection according to the diagnostic time you set. The default diagnostic time is `60`minutes. However, please ensure that during this period of time, the task has completed initialization, data processing, and other operations and entered the stable training phase, otherwise there will be false positives.<br><br>* The results of environmental diagnostics can be viewed through the diagnostic flag in the list or through diagnostic events. The result of the diagnostic failure will not affect the running status of the task. |
|Task Hanging Detection |* Support to detect whether the task is hung. **Optional** .<br><br>* Support to configure the pause duration, the default is `30`minutes. After the set duration threshold is exceeded, the platform will determine that the task is hung.<br><br>* The results of environmental diagnostics can be viewed through the diagnostic flag in the list or through diagnostic events. The result of the diagnostic failure will not affect the running status of the task. |
|auto retry |* Support for automatic retry of configuration tasks. **Optional** .<br><br>* Support for configuring the maximum number of retries and the retry interval (the time between the termination of the previous task and the submission of the new task).<br><br>* Supports configuring conditions for triggering retries: task failure, idle resource recovery (for tasks that use idle resources), node failure, process inspection failed, task Hang. After triggering a retry, if the original state of the current task is running, it will be changed to stopped. |



4. After completing the configuration of the above form, tick Agree to the agreement, and click [Confirm Order] to submit and start the training task. Subsequent users can manage training tasks in the list page/details page of [Custom Training].


<span id="命令行"></span>
## command line


1. Install and configure the Machine Learning Platform command line tools, see [Command Line Tools ](https://docs.byteplus.com/en/docs/mlp/Use_documents).

2. Write the configuration file (.yaml) of the training task. See the [volc ml_task submit ](https://docs.byteplus.com/en/docs/mlp/Use_documents)for the preparation specification of the configuration file. You can also export the yaml of the existing task through the `volc ml_task list`instruction and operation prompts for reference.

3. Submit the training task locally using the following command:


```Plain
volc ml_task submit --conf <Path to the configuration file>
# Example:
volc ml_task submit --conf ./tf_custom_mnist_random_1worker-2c4g.yaml
100% |████████████████| (1/1, 826 it/s)
Task created successfully, task_id=t-20211011193917-vzjm4
```


<span id="任务通知"></span>
# task notification

When the task is completed, fails or abnormal, etc., the platform can send a message to notify the user in time. For the specific configuration process, please refer to the [Message notifications for configuration tasks](https://docs.byteplus.com/docs/mlp/Message_notifications_for_configuration_tasks).
