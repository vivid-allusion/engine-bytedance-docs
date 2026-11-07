---
title: "Test protection capabilities online"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Create_online_test_tasks"
---

Online Testing allows you to submit samples directly in the console and quickly evaluate different protection capabilities. You can create test tasks for existing assets or custom models, monitor task status, review detection results, and copy previous tasks to reuse their configurations. These capabilities reduce repeated configuration work and shorten validation and troubleshooting cycles.

<span id="ba46fe52"></span>
## Supported test types

Online Testing currently supports the following test types:


|Test type |Description |Requirements |
|---|---|---|
|LLM Application Firewall test |Submit samples to evaluate the effectiveness of the security policies configured for an asset. |The asset must be integrated through the SDK and have **LLM Application Firewall** enabled. |
|Deepfake detection test |Upload images or videos to evaluate the effectiveness of deepfake detection. |The asset must be integrated through the SDK and have **Deepfake Detection** enabled. |
|Custom model test |Submit text samples to a trained custom model to evaluate its recognition performance before or after release. |The custom model must have the status **Pending release** or **Released**. |


<span id="9f7f3a3f"></span>
## Prerequisites

Before creating a test task, confirm that the following requirements are met:


* You have integrated an asset for the relevant protection scenario or completed custom model training.

* You have defined the purpose of the test, such as validating protection policies, detecting manipulated content, or evaluating a custom model.

* To test images, videos, or files, the selected asset must have the corresponding content\-type protection policy enabled.


<span id="c15c7c45"></span>
## Test the LLM Application Firewall

An LLM Application Firewall test evaluates how effectively the security policies associated with an asset handle user input or model responses. You can use this test to validate policies, verify configurations before launch, and refine protection rules.

<span id="a3141cbd"></span>
### Limits and considerations


* Limits and considerations

* **Asset requirements**: Only assets integrated through the SDK and configured for the **LLM Application Firewall** protection scenario are supported.

* **Task limits**: A test task can contain up to 100 subtasks, with each subtask representing one group of test samples. Each subtask can include up to nine images or files.

* **Multimodal detection**:

   * When a subtask contains multiple content types, such as images, videos, and files, the system processes each type according to the associated instance, asset, and policy configurations. Usage charges apply to pay\-as\-you\-go instances.

   * Uploading too many videos or files in a single task may cause the test to fail because of rate limits. Split large submissions into multiple tasks. For details, refer to [Usage restrictions](https://docs.byteplus.com/docs/LLM-Application-Firewall/Check_whether_input_or_output_content_is_compliant#82c0060f).

   * If any content in a multimodal subtask triggers a policy, the entire subtask is marked as having triggered that policy.

* **Unsupported capabilities**: Online Testing does not currently support capabilities that depend on the `history` field, including resource exhaustion mitigation, hallucination detection, and multi\-turn conversation protection.


<span id="c6257900"></span>
### Create a test


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield).

2. In the left navigation pane, select **Protection** \>  ** ** **Custom protection** \> **Online Testing**.

3. In the upper\-right corner of the list page, click **New Test**, select **LLM Application Protection Testing**, and confirm.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9408c2080f0649ddbebdc33ccf0005ce) </span>

4. Enter the test task parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2e9777f235804729bd3b73f5f48501be) </span>

   
   |Parameter |Note |
   |---|---|
   |**Task Name** |Enter a name that identifies the test task.<br><br>The name must begin with a Chinese character, letter, or digit. It can contain Chinese characters, letters, digits, periods (`.`), underscores (`_`), and hyphens (`-`). The length must be between 1 and 128 characters. |
   |**Associated Asset** |Select the asset to test. Only assets integrated through the SDK and configured for the **LLM Application Firewall ** protection scenario are available. |
   |**Test Samples** |Enter text or upload images, videos, or files for testing.<br><br>You can include multiple content types in the same subtask. Each subtask can contain up to nine images or files. Before uploading multimodal content, verify that the selected asset has protection policies enabled for the corresponding content types. |
   |**Submission Type** |Specifies whether the sample is a user prompt or a model response. |
   |**New Subtask** |Click to add another set of test content for the same asset. Up to 100 subtasks can be added. |
   

5. Review the configuration and click **Start Test**.


<span id="59679923"></span>
### Review the results

The system displays results separately for each subtask. For example, if a task contains two subtasks, the results may show that the first subtask triggered a protection policy while the second did not.

Review the triggered policies and detection details to determine whether the asset configuration produces the expected results.

<span id="6990cc37"></span>
## Test deepfake detection

A deepfake detection test evaluates the product’s ability to identify manipulated or AI\-generated content in images and videos. You can use it for multimedia verification, sample\-based inspections, and detection quality assessment.

<span id="07c93690"></span>
### Limits and considerations


* **Asset requirements**: Only assets integrated through the SDK and configured for the **Deepfake Detection** protection scenario are supported.

* **Supported images**: Images must use the `jpg`, `jpeg`, `webp`, or `png` format. Each image must be no larger than **10 MB**.

* **Supported videos**: Videos must use the `mp4` or `avi` format. Each video must be no larger than **50 MB**.

* **Sample limit**: A test task can contain up to 50 images and videos in total.

* **Result granularity**: The system displays a separate result for each image or video.

* **Repeated testing**: To test a new set of similar samples, copy a previous task, replace or update its samples, and run the test again.


<span id="6b1e8dcd"></span>
### Create a test


1. Log in to the [LLM Application Firewall console](https://console.volcengine.com/omni-shield/llm-shield).

2. In the left navigation pane, select **Protection** \> **Custom protection** \> **Online Testing**.

3. In the upper\-right corner of the list page, click **New Test**, select **Deepfake Detection**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2e0bf60f22324127bc83cbaacd9ee750) </span>

4. Enter the test task parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/b303665398644380971ee0b4649bdedc) </span>

   
   |Parameter |Description |
   |---|---|
   |**Task Name** |Enter a name that identifies the test task.<br><br>The name must begin with a Chinese character, letter, or digit. It can contain Chinese characters, letters, digits, periods (`.`), underscores (`_`), and hyphens (`-`). The length must be between 1 and 128 characters. |
   |**Associated Asset** |Select the asset to test. Only assets integrated through the SDK and configured for the **Deepfake Detection ** protection scenario are available. |
   |**Test Samples** |Upload the images or videos that you want to test. The system returns a separate result for each sample.<br><br>Images must use the `jpg`, `jpeg`, `webp`, or `png` format and must not exceed 10 MB each. Videos must use the `mp4` or `avi` format and must not exceed 50 MB each. You can upload up to 50 images and videos in total. |
   

5. Review the configuration and click **Start Test**.


<span id="3f0d5472"></span>
### Review the results

The system displays a result for each image or video. The result includes whether the sample was identified as manipulated content, the triggered manipulation labels, and a confidence score.

A sample can trigger multiple labels. Review the labels and confidence scores together with the original image or video when evaluating the result.


|Label name |API label |Description |
|---|---|---|
|Default forgery |`10900000` |Indicates that the system has classified the sample as manipulated content. This label applies only to deepfake detection assets. |
|PS forgery |`10901000` |Indicates suspected image editing, retouching, or partial manipulation. This label applies only to deepfake detection assets. |
|Forged entity |`10902000` |Indicates suspected generation, replacement, or manipulation of an entity in the content. This label applies only to deepfake detection assets. |
|Forged text |`10903000` |Indicates suspected generation, replacement, or manipulation of text in the content. This label applies only to deepfake detection assets. |
|Forged face |`10904000` |Indicates suspected face generation, face swapping, or facial manipulation. This label applies only to deepfake detection assets. |


<span id="0d167e9d"></span>
## Test a custom model

A custom model test evaluates how a trained custom model classifies text samples. You can use it to validate representative samples, compare results, and assess model performance before release.

<span id="c08e54c3"></span>
### Limits and considerations


* **Model status**: Only custom models with the status **Pending release** or **Released** are supported.

* **Content type**: Custom model tests support text samples only.

* **Sample limit**: A test task can contain up to 100 text samples.

* **Sample separation**: Each sample appears as a separate entry in the results, making it easier to compare model outputs.

* **Keyboard controls**: Press `Enter` to add a new sample. Press `Shift+Enter` to insert a line break within the current sample.


<span id="6f982c41"></span>
### Create a test


1. Log in to the [LLM Application Firewall console](https://console.volcengine.com/omni-shield/llm-shield).

2. In the left navigation pane, select **Protection** \> **Custom protection** \> **Online Testing**.

3. In the upper right corner of the list page, click **New Test** and select **Custom Model Testing**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c90654f9e7a2456999397e22cc4588e2) </span>

4. Fill in the test task parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a204ad9ef38c49b4b71bfa63f406fc2d) </span>

   
   |Parameter |Description |
   |---|---|
   |**Task Name** |Enter a name that identifies the test task.<br><br>The name must begin with a Chinese character, letter, or digit. It can contain Chinese characters, letters, digits, periods (`.`), underscores (`_`), and hyphens (`-`). The length must be between 1 and 128 characters. |
   |**Associated Model** |Select the custom model to test. Only models with the status **Pending release ** or **Released ** are available. |
   |**Test Samples** |Enter the text samples that you want to evaluate. Press `Enter` to add a new sample or `Shift+Enter` to insert a line break within the current sample. A test task can contain up to 100 samples. |
   

5. Review the configuration and click **Start Test**.


<span id="7baf10b3"></span>
### Review the results

The system displays a separate result for each text sample, allowing you to compare the model’s classifications across the submitted samples.

<span id="09ba6527"></span>
## Manage test tasks

The Online Testing page displays all test tasks, including their current status, test type, associated asset or model, execution time, and available actions.


|Column |Description |
|---|---|
|**Task Name/ID**<br><br> |Displays the test task name and task ID. After the task is completed or fails, click the task name to enter the details page. |
|**Test Status** |Displays the current status of the task, including<br><br><br>* Pending test: The task has been created and is waiting to start execution.<br><br>* Testing: The task is being executed.<br><br>* Test failed: All subtasks under the task failed, or the task as a whole failed.<br><br>* Test partially failed: Some subtasks under the task failed, while other subtasks succeeded.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If some tests fail, you can retry the failed subtasks. If repeated retries fail, contact technical support for assistance.   </div><br>   <br><br>* Completed: The task has been executed. |
|**Test Type** |Displays the task’s test type, such as an LLM Application Firewall test, deepfake detection test, or custom model test. |
|**Associated Asset/Model** |Displays the asset or custom model bound to this test. |
|**Start Time** /**End Time** |Displays the task execution time. |
|**Actions** |Provides options for copying, retrying, and deleting the task.<br><br>**Copy task**: Creates a new test based on the selected task. The new test page automatically inherits the test type, associated asset or model, samples, and other settings. Use this option when you want to adjust samples and run a similar test.<br><br>**Retry task**: Runs all subtasks in the task again. Use this option after a failure or when additional validation is required.<br><br>**Delete task**: Permanently removes the task and all of its subtask records from the list. |
