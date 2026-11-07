---
title: "Unit test"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Unit_tests"
---

CP provides a built\-in **unit test** task that supports unit testing for Java Maven, Java Gradle, Python, and Go languages. This document uses **Go unit test** as an example to introduce usage instructions for this built\-in task.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Unit test cases have been added to the code repository.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* Go unit test

   * The test command must include `-json`.

   * In the test command, the intermediate file must be `cover.out`.

   * In the test command, you need to use the `mkdir` command to create the test report directory.

* Performance testing and example test cases are not supported.

* Java Gradle unit tests currently do not support parsing test reports, so the quality gate feature cannot be used.


<span id=".5re75Yqg5Lu75Yqh"></span>
## Add task

When creating or editing a pipeline, go to the **Process Orchestration** tab, click **Add Job**, and the **Add Job** drawer will pop up. Select the task template **Test \> Go unit test**.

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description

The following introduces the parameters of this built\-in task.


* **Task name**

   The default is Go unit test; custom task names are supported.

* **Upstream task**

   Shows the name of the upstream serial task for the current task. If there is no upstream task, `-` is shown.

* **Code source download policy**

   Select the code source download policy based on whether the current task needs to use the code source.

   * **Download code**: The current task needs to download the code source.

   * **Do not download code**: The current task does not need to use the code source.

* **Step**

   The current task includes one default built\-in step (Go unit test). You can add other serial steps to the current task as needed. The following introduces the parameters of this default built\-in step.

   
   |Parameter |Description |
   |---|---|
   |Step name |The default is Go unit test, and custom step names are supported. |
   |Version |Select the tool version used for Go unit testing. The supported versions for different languages are as shown in the Console. |
   |Test command |Enter the Go unit test command. The command box contains the default test command. Please adjust it according to your actual business needs. |
   |Directory |Displays the directory where the test report is generated after executing the test command. The pipeline will automatically upload all files in this directory. You can modify the default directory. When making changes, you must also update the directory parameter in the test command. |
   |File |Displays the test report file generated after executing the unit test command. The pipeline will automatically parse and display the file content. You can modify the default file. When making changes, you must also update the file parameter in the test command. |
   |File entry |Displays the file name of the test report in HTML format. You can modify the default file entry. When making changes, you must also update the file entry parameter in the test command. |
   |Quality gate |Supports using quality threshold values as criteria for determining whether the unit test passes. You can use the number of failures, success rate, and coverage rate as metrics.<br><br><br>* Supports setting multiple metric criteria.<br><br>* When multiple criteria are set, you can require that all conditions be met to pass the quality threshold, or allow passing if any one condition is met. |
   |Skip on fail |Optional configuration.<br><br><br>* Enabled: If the current step fails, it will be skipped, and the remaining steps of the current task and the pipeline will continue to run.<br><br>* Disabled: If the current step fails, the remaining steps of the current task will not be executed, and the pipeline will fail. |
   

* **Task output**

   Shows all artifacts output by the current task, including artifacts from all steps under the current task. If there are no artifacts, `-` is shown. Artifacts can be used as input for subsequent tasks.

   For the current default built\-in step, the total number of test cases, number of failures, number of skips, success rate, coverage rate, test report file, and test report HTML will be output.

* **Advanced settings**

   * **LimitRange**: Supports setting the upper limit for CPU and memory.

   * **Disk capacity limit**: Supports setting the upper limit for disk capacity, up to 100 GiB.

   * **Timeout time**: Sets the timeout for the entire task; the task will automatically fail if it exceeds the timeout. A task can include multiple serial steps, and the total execution time of all steps must be less than the task's timeout time.

   * [Webhook notification](https://docs.byteplus.com/en/docs/cp/Webhook_notification): Supports sending task\-level messages via both Webhook and Feishu bot, helping you stay informed about task updates in a timely manner.

   * **Automatic fail retry**: After enabling, enter the maximum number of retries supported. When a task execution fails, it will retry up to the configured maximum number of times.


<span id=".5pel5b-X5Y-K5Lqn54mp"></span>
## Logs and artifacts

The following describes the details displayed in the pipeline after this built\-in task completes.

On the run details page of the current pipeline, click the title of the Go unit test card to view the run log, artifacts, and task configuration information.


* Run log: Shows the real\-time run log of this task.

* Task configuration: Shows the configuration parameters of this task. For details, refer to the parameter description above.

* Artifacts: After a successful run, the unit test task will output the following artifacts.

   * Total number of test cases, number of failures, number skipped, coverage, and success rate.

   * Unit test file: For Go unit tests, a test report file will be generated, which can be downloaded locally by clicking.

   * Unit test report: Click to view the report content online.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <strong>coverage</strong> statistics value for Java unit tests is affected by the external mirror source, which may cause inconsistency in the final coverage calculation. It is recommended to use it for reference only. Other unit test metrics are all accurate and reliable.   </div>
