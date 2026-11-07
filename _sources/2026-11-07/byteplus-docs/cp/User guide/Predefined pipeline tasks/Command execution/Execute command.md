---
title: "Execute command"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Command_execution_2"
---

CP provides a built\-in **Execute command** task, making it convenient for users to write scripts and perform other general execution tasks. For example: complete configuration modification and update actions through Execute command, or pull required files using commands.

<span id=".5re75Yqg5Lu75Yqh"></span>
## Add task

When creating or editing a pipeline, go to the **Process Orchestration** tab, click **Add Job**, and the **Add Job** drawer will pop up. Select the task template **Execute command \> Execute command**.

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description

The following introduces the parameters for this built\-in task.


* **Job name**

   The default is Execute command, and it supports custom task names.

* **Upstream task**

   Displays the name of the upstream sequential task for the current task. If there is no upstream task, it displays as `-`.

* **Code source download policy**

   Depending on whether the current task needs to use the code source, select the code source download policy.

   * **Download code**: The current task needs to download the code source.

   * **Do not download code**: The current task does not need to use the code source.

* **Step**

   The current task includes one default built\-in step (Execute command). Supports adding other sequential steps to the current task as needed. The following introduces the parameters for this default built\-in step.

   
   |Parameter |Description |
   |---|---|
   |Step name |The default is Execute command, and it supports custom step names. |
   |Shell language |Select the Shell language to use. Currently, only bash commands are supported. |
   |Execute command |Custom command script to be executed. |
   |Skip on fail |Optional configuration.<br><br><br>* Enable: If the current step fails, it will be skipped directly. The remaining steps of the current task can continue to execute, and the pipeline can also continue to run.<br><br>* Disable: If the current step fails, the remaining steps of the current task will not be executed, and the pipeline will fail. |
   

* **Task output**

   Displays all artifacts output by the current task, including artifacts from all steps within the current task. If there are no artifacts, it displays as `-`. Artifacts can be used as input for subsequent tasks.

   For the current default built\-in step, there is no artifact output.

* **Advanced settings**

   * **LimitRange**: Supports setting upper limits for CPU and memory.

   * **Disk capacity limit**: Supports setting an upper limit for disk capacity, with a maximum of 100 GiB.

   * **Timeout**: Sets the timeout for the entire task. The task will automatically fail after the timeout is reached. A task can include multiple sequential steps, and the total execution time of all steps must be less than the task's timeout.

   * [Webhook notification](https://docs.byteplus.com/en/docs/cp/Webhook_notification): Supports pushing task\-level messages via Webhook, helping you stay informed about task updates in a timely manner.

   * **Automatic fail retry**: After enabling, enter the maximum number of retries supported. When a task fails to execute, it will retry up to the specified number of times according to the configured maximum number of retries.


<span id=".5pel5b-X6K-05piO"></span>
## Log description

The following describes the details displayed in the pipeline after this built\-in task is completed.

On the run details page of the current pipeline, click the title of the command execution card to view the run log and task configuration information.


* Run log: Shows the run log of this task in real time.

* Task configuration: Shows the configuration parameters of this task. For details, refer to the parameter description above.
