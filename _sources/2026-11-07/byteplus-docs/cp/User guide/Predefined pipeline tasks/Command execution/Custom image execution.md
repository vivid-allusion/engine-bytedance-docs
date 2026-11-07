---
title: "Custom image execution"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Custom_image_execution"
---

CP provides the **Custom image execution** task, which supports using a custom environment to execute commands. This is suitable for scenarios where built\-in tasks cannot meet user requirements. For example: writing scripts using shell tools other than Bash, compiling and building C++ code, and more.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The image address is used as the runtime environment for custom command execution. Please prepare the container image to be used in advance.

<span id=".5re75Yqg5Lu75Yqh"></span>
## Add task

When creating or editing a pipeline, go to the **Process Orchestration** tab, click **Add Job**, and the **Add Job** drawer will pop up. Select **Custom image execution** as the task template.

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description

The following describes the parameters of this built\-in task.


* **Job name**

   The default is "Custom image execution", and custom task names are supported.

* **Upstream task**

   Displays the name of the upstream serial task for the current task. If there is no upstream task, `-` is displayed.

* **Code source download policy**

   Select the code source download policy according to whether the current task needs to use the code source.

   * **Download code**: The current task needs to download the code source.

   * **Do not download code**: The current task does not need to use the code source.

* **Step**

   The current task includes a default built\-in step (custom environment command execution). You can add other serial steps to the current task as needed. The following describes the parameters of this default built\-in step.

   
   |Parameter |Description |
   |---|---|
   |Step name |The default is to execute custom environment commands, and custom step names are supported. |
   |Image address |Enter the image address to be used. The image here is used to define the script's runtime environment.<br><br>The image address format is `host/namespace/repo:tag`. |
   |Username |Optional. For private images, you must enter the correct username. |
   |Password |Optional. For private images, you must enter the correct password. |
   |Command execution |Customize the command script to be executed. |
   |Skip on failure |Optional configuration.<br><br><br>* Turn on: If the current step fails, it will be skipped directly, and the remaining steps of the current task can continue to execute. The pipeline can also continue to run.<br><br>* Turn off: After the current step fails, the remaining steps of the current task will not be executed, and the pipeline will fail. |
   

* **Task output**

   Displays all artifacts output by the current task, including artifacts from all steps under the current task. If there are no artifacts, `-` is displayed. Artifacts can be used as input for subsequent tasks.

   For the current default predefined steps, no artifact is output.

* **Advanced settings**

   * **Resource limit**: Supports setting upper limits for CPU and memory.

   * **Disk capacity limit**: Supports setting an upper limit for disk capacity, up to a maximum of 100 GiB.

   * **Timeout**: Sets the timeout for the entire task. The task will automatically fail if it exceeds the timeout. A task can contain multiple serial steps, and the total runtime of all steps must be less than the task's timeout.

   * [Webhook notification](https://docs.byteplus.com/en/docs/cp/Webhook_notification): Supports sending task\-level messages via Webhook and Feishu bot, helping you stay informed about task status in a timely manner.

   * **Automatic retry on failure**: When enabled, enter the maximum number of retries supported. If task execution fails, it will retry up to the specified number of times according to the configured maximum number of retries.


<span id=".5pel5b-X6K-05piO"></span>
## Log description

The following introduces the detailed information displayed in the pipeline after the built\-in task is completed.

On the current pipeline's execution details page, click the title of the Custom images execution task card to view the execution log and task configuration information.


* Execution log: Displays the task's execution log in real time.

* Task configuration: Displays the configuration parameters for the task. For details, refer to the parameter description above.
