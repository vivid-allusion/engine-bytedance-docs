---
title: "Java compilation and build"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Java_compilation_and_build"
---

CP built\-in **compilation and build** task supports compilation and build for Java Maven, Java Gradle, Python, Go, and NodeJS languages. This document uses **Java compilation and build** as an example to introduce the usage instructions for this built\-in task.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Code source has been created. For specific operations, see [Create code source](https://docs.byteplus.com/en/docs/cp/Integrate_code_source).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits

For Maven compilation and build, it is recommended to use image proxies in China. Native proxies may fail to pull due to network issues.

<span id=".5re75Yqg5Lu75Yqh"></span>
## Add task

When creating or editing a pipeline, go to the **Process Orchestration** tab, click **Add Job**, and the **Add Job** drawer will pop up. For task templates, select **build \> Java compilation and build**.

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description

The following introduces the parameters of this built\-in task.


* **Job name**

   The default is Java compilation and build, and custom task names are supported.

* **Upstream task**

   Shows the name of the upstream serial task for the current task. If there is no upstream task, `-` is displayed.

* **Code source download policy**

   According to whether the current task needs to use the code source, select the code source download policy.

   * **Download code**: The current task needs to download the code source.

   * **Do not download code**: The current task does not need to use the code source.

* **Step**

   The current task includes a default built\-in step (Java compilation and build). Supports adding other serial steps to the current task as needed. The following introduces the parameters of this default built\-in step.

   
   |Parameter |Description |
   |---|---|
   |Step name |The default is Java compilation and build, and custom step names are supported. |
   |Version |Select the tool version used for Java compilation and build. The supported versions for different languages are subject to what is shown in the console. |
   |Compilation command |Enter the compilation command. The command box contains the default compilation command. Please adjust it according to actual business requirements. |
   |Skip on fail |Optional configuration.<br><br><br>* Turn on: If the current step fails to execute, it will be skipped directly. The remaining steps of the current task can continue to execute, and the pipeline can continue to run.<br><br>* Turn off: After the current step fails, the remaining steps of the current task will not execute, and the pipeline will fail. |
   

* **Task output**

   Display all outputs of the current task, including outputs from all steps under this task. If there are no outputs, display as `-`. Outputs can be used as input for subsequent tasks.

   There are no outputs for the current default predefined steps.

* **Advanced settings**

   * **LimitRange**: Supports setting upper limits for CPU and memory.

   * **Disk capacity limit**: Supports setting an upper limit for disk capacity, up to 100 GiB.

   * **Timeout time**: Sets the timeout for the entire task. The task will automatically fail if it times out. A task can include multiple serial steps; the total runtime of all steps must be less than the task's timeout.

   * [Webhook notification](https://docs.byteplus.com/en/docs/cp/Webhook_notification): Supports pushing task\-level messages via Webhook and Feishu bot, helping you stay informed about task status.

   * **Fail automatic retry**: Once enabled, enter the maximum number of retries supported. When task execution fails, it will retry up to the specified number of times according to the configured maximum retries.


<span id=".5pel5b-X6K-05piO"></span>
## Log description

The following introduces the detailed information displayed in the pipeline after this built\-in task is completed.

On the current pipeline's run details page, click the title of the Java build card to view the run log and task configuration information.


* Run log: Displays the run log of this task in real time.

* Task configuration: Shows the configuration parameters of this task. For details, refer to the parameter description above.
