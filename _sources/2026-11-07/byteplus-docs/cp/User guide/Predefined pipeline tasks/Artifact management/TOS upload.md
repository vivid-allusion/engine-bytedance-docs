---
title: "TOS upload"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/TOS_upload"
---

CP provides a built\-in **TOS upload** step, supporting the upload of a single file or folder from the workspace to BytePlus's [TOS](https://docs.byteplus.com/en/docs/tos/docs-what-is-tos) object storage.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Content uploaded to TOS can come from:


* Code repository

* Pipeline build artifacts. Mainly used for front\-end static resource release scenarios: Through **Node.js build \> TOS upload**, Node.js projects are compiled and built, and the build artifacts are uploaded to TOS. Subsequently, the TOS address of the static resources can be referenced.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The BytePlus object storage service has been activated.

* A storage bucket has been created. For specific operations, see [Create bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

* For first\-time TOS uploads, cross\-service authorization must be completed. For specific operations, see [Cross-service authorization](https://docs.byteplus.com/en/docs/cp/Cross-service_authorization).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* Only uploads to the TOS service under the same BytePlus account are supported.

* The combined size of uploaded files or folders must not exceed 10 GB.


<span id=".5re75Yqg5q2l6aqk"></span>
## Add step

This article uses **Node.js build \> TOS upload** as an example to explain how to add a TOS upload step.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Each task in the pipeline shares a workspace. For build upload scenarios, <strong>build</strong> and <strong>TOS upload</strong> must be in the same task; otherwise, the build artifact cannot be obtained.</div>



1. When creating or editing a pipeline, go to the **Process Orchestration** tab, click **Add Job**, and the **Add Job** drawer will pop up. For the task template, select **Build \> NodeJS build**.

2. Click **Add step**, select **Predefined steps \> Artifact \> TOS upload**, and **under the NodeJS build** step, add the serial step **TOS upload.** 


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description

The following section introduces the parameters for the TOS upload step.


|Parameter |Description |
|---|---|
|Step name |The default step name is TOS upload; custom step names are supported. |
|Source file path |Path of the file/folder to upload. The path should be relative to the project folder; wildcards are not supported.<br><br>Example:<br><br><br>* `demo.txt`: Upload the demo.txt file.<br><br>* `build`: Upload the build folder.<br><br>* `.`: Upload all files in the current directory.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To pass artifacts between steps, place the files in the workspace directory. For example: In the <strong>build \> TOS upload</strong> scenario, build artifacts need to be placed in the workspace directory.</div><br> |
|TOS file path |Directory to upload to in the TOS bucket. If the target directory does not exist, a new directory will be created.<br><br><br>* `/`: Upload to the root directory of the bucket.<br><br>* `demo/`: Upload to the demo directory in the bucket.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If uploading a single file, such as <code>a.txt</code>.</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If you enter <code>b</code>, the file will be renamed to b and uploaded to the root directory of the bucket.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you enter <code>b/</code>, the file will be uploaded to the b directory in the bucket.</div><br> |
|Bucket region |Select the region where the bucket to be uploaded is located. |
|Bucket name |Select the target bucket to upload to. |
|Include relative parent directory during upload |Whether to upload together with the relative parent directory.<br><br><br>* Yes: The uploaded content will include the parent directory and all items within it.<br><br>* No: The uploaded content will exclude the parent directory and only include all items within it. |
|Skip on fail |Optional configuration.<br><br><br>* Turn on: If the current step fails, it will be skipped directly, the remaining steps of the current task can continue executing, and the pipeline can also continue to run.<br><br>* Turn off: After the current step fails, the remaining steps of the current task will no longer be executed, and the pipeline will fail. |


<span id=".6auY57qn6K6-572u"></span>
## Advanced settings


* **LimitRange**: Supports setting upper limits for CPU and memory.

* **Disk capacity limit**: Supports setting the upper limit for disk capacity, up to 100 GiB.

* **Timeout time**: Sets the timeout time for the entire task. If the task times out, it will automatically fail. A task can include multiple serial steps, and the total execution time of all steps must be less than the task's timeout time.

* [Webhook notification](https://docs.byteplus.com/en/docs/cp/Webhook_notification): Supports pushing task\-level messages via Webhook and Feishu bot, helping you stay informed about task status in a timely manner.

* **Retry**: After turning on, enter the maximum number of retries supported. When a task execution fails, it will retry up to the specified number of times according to the configured maximum number of retries.

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">  .   </div>
   

<span id=".5pel5b-X5Y-K5Lqn54mp"></span>
## Logs and artifacts

The following section introduces the details shown in the pipeline after this step is completed.


* Execution logs: Shows the real\-time execution logs for TOS upload.

* Task configuration: Shows the configuration parameters for this task, including the configuration parameters for all steps.

* Artifact: After the task runs successfully, the upload path of TOS will be provided.
