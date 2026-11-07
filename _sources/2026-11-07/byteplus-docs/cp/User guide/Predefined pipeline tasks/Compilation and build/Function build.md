---
title: "Function build"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Function_building"
---

CP built\-in **build** task supports compiling and building for Java Maven, Java Gradle, Python, Go, and NodeJS languages. This document uses **function build** as an example to introduce the considerations for using this built\-in task.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Code source has been created. For specific operations, see [Create code source](https://docs.byteplus.com/en/docs/cp/Integrate_code_source).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits

It is recommended to use image proxies in China for Maven compilation and build. Native proxies may fail to fetch due to network issues.

<span id=".5re75Yqg5Lu75Yqh"></span>
## Add task

When creating or editing a pipeline, go to the **Process Orchestration** tab, click **Add Job**, and the **Add Job** drawer will pop up. Select **Build \> Function build** as the task template.

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description

The following introduces the parameters of this built\-in task.


* **Job name**

   The default job name is "Function build and compile". You can customize the job name.

* **Upstream task**

   Displays the name of the upstream task for the current job. If there is no upstream task, `-` is displayed.

* **Code source download policy**

   According to whether the current task needs to use the code source, select the code source download policy.

   * **Download code**: The current task needs to download the code source.

   * **No code download**: The current task does not require a code source.

* **Steps**

   * Function building and compilation

      The current task includes a default built\-in step (function building). You can add other serial steps to the current task as needed. The parameters for this default built\-in step are described below.

   
   |Parameter |Description |
   |---|---|
   |Step name |The default is function build; custom step names are supported. |
   |Build environment |Select the development language and version used for function building. The supported versions for different languages are as shown in the Console. |
   |Compilation command |Enter compilation command. The command box contains the default compilation command. Please adjust it according to your actual business requirements. |
   |Skip on failure |Optional configuration.<br><br><br>* Turn on: If the current step fails, it will be skipped. The remaining steps of the current task can continue to execute, and the pipeline can continue to run.<br><br>* Turn off: After the current step fails, the remaining steps of the current task will not be executed, and the pipeline will fail. |
   

   * TOS upload

   
   |Parameter |Description |
   |---|---|
   |Step name |The default is TOS upload; custom step names are supported. |
   |Source file path |Upload file/folder path. The starting position is the relative path of the project folder. Wildcards are not supported.<br><br>Example:<br><br><br>* `demo.txt`: Upload the demo.txt file.<br><br>* `build`: Upload the build folder.<br><br>* `.`: Upload all files in the current directory.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To pass artifacts between steps, please place the files in the workspace directory.</div><br> |
   |TOS file path |Directory to upload to TOS Bucket. If the target directory does not exist, a new directory will be created.<br><br><br>* `/`: Upload to the root directory of the Bucket.<br><br>* `demo/`: Upload to the demo directory of the Bucket.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If uploading a single file, such as <code>a.txt</code>.</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If you enter <code>b</code>, the file will be renamed to b and uploaded to the root directory of the Bucket.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you enter <code>b/</code>, the file will be uploaded to the b directory of the Bucket.</div><br> |
   |Bucket region |Select the Region where the Bucket to be uploaded is located. |
   |Bucket name |Select the target Bucket for upload. |
   |Include relative parent directory when uploading |Whether to upload the relative parent directory together.<br><br><br>* Yes: The uploaded content will include the parent directory and all content under the directory.<br><br>* No: The uploaded content will exclude the parent directory and only include all content under the directory. |
   |Skip on failure |Optional configuration.<br><br><br>* Turn on: If the current step fails to run, it will be skipped directly. The remaining steps of the current task can continue to execute, and the pipeline can continue to run.<br><br>* Turn off: After the current step fails, the remaining steps of the current task will not be executed, and the pipeline will fail to run. |
   

* **Task output**

   Displays all artifacts output by the current task, including artifacts from all steps within the task. If there are no artifacts, displays as `-`. Artifacts can be used as input for subsequent tasks.

   The current default built\-in step does not produce any artifact output.

* **Advanced settings**

   * **Resource limits**: You can set upper limits for CPU and memory.

   * **Disk capacity limit**: You can set an upper limit for disk capacity, up to 100 GiB.

   * **Timeout time**: Set the timeout for the entire task. The task will automatically fail if it exceeds the timeout. A task can include multiple serial steps, and the total execution time of all steps must be less than the task's timeout time.

   * [Webhook notification](https://docs.byteplus.com/en/docs/cp/Webhook_notification): Supports pushing task\-level messages via Webhook and Feishu bot, helping you stay informed about task status in a timely manner.

   * **Automatic retry on failure**: Once enabled, enter the maximum number of retries supported. If the task execution fails, it will retry up to the configured maximum number of times.
