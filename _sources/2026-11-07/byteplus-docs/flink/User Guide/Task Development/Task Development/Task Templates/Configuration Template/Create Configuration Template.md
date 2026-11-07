---
title: "Create Configuration Template"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Create_Configuration_Template"
---

During the task development configuration process, developers often need to fill in Flink configuration parameters multiple times. The console now offers a configuration module feature, allowing you to create configuration modules in advance and directly refer to the configuration template during task development.

<span id="837ee2ff"></span>
## Notice


* There are differences in creating configuration templates for streaming and batch tasks, primarily because Flink Batch tasks do not support Checkpointing and do not support automatic tuning. When you select a task type as either streaming or batch task, the parameters will automatically switch to match the selected task type.

* Different engine versions support different Flink parameter configurations; please review in detail to confirm specific functionalities.


<span id="8a76e41b"></span>
## Create Configuration Module


1. Log in to the [BytePlus Flink console](https://console.byteplus.com/flink).

2. Select the target region in the top menu bar.

3. Select **Project Management** from the left navigation bar, then click the project block to enter the project.

4. In the project's left navigation bar, select **Task Development \> Template Management**.

5. On the **Configure Template** page, click the plus button and select **Create Template**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58e088683c174b059dc95893924c33fb~tplv-goo7wpa0wc-image.image) </span>


6. In the **Create Configuration Template** dialog, set the template name, task type, engine version, and description, then click **OK**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db6db36dafcb4f0eac68b0610f407397~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Description** |
|---|---|
|Template Name |Customize the configuration template name. |
|Task Type |Select **streaming task configuration** or **batch task configuration** based on business needs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">There are differences when creating configuration templates for streaming tasks and batch tasks, mainly because Flink Batch tasks do not support Checkpoint.</div><br> |
|Engine Version |Configure the engine version applicable to the template according to business needs. A configuration template can only be applied to one engine version. |
|Description |A brief text describing the purpose of the template. |



7. Click the modify button, on the Configure Template details page, configure BytePlus Flink related parameters, including resource configuration for Task Manager and Job Manager, as well as settings for Checkpoint, Task Failure Restart Policy, Task Failure Retry Startup, Custom Parameters, and Custom Dependency Files.

   For how to configure Flink parameters, please refer to [Configure Flink Parameters](https://docs.byteplus.com/docs/flink/Configure_Flink_Parameters).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/352beff1e29b482282a3e1f1716b52e7~tplv-goo7wpa0wc-image.image) </span>


8. After setting the template parameters, click **Save** at the bottom right corner.


<span id="434351a9"></span>
## Other Operations


* Edit Template: On the Configure Template page, support direct modification of the configurations, then click **Save** to save them.

* Delete Template: Click **Delete** and confirm the action. Deleting a template will not affect existing tasks, but it may cause the template to be irrecoverable. Please proceed with caution.
