---
title: "Create a pipeline via console"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Create_pipelines"
---

The pipeline is the carrier for continuous delivery, enabling the entire process from development to production through build automation, integration automation, validation automation, and deployment automation. This article introduces how to create a pipeline.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A workspace has been created. For detailed instructions, see [Create workspace](https://docs.byteplus.com/en/docs/cp/Create_a_workspace).

* If you need to configure the code source, please create the code source in advance. For detailed instructions, see [Integrate code source](https://docs.byteplus.com/en/docs/cp/Integrate_code_source).

* If you need to associate a concurrency lock, make sure to create one in advance. For detailed actions, see [Configure concurrency lock](https://docs.byteplus.com/en/docs/cp/Configure_the_concurrency_lock).

* To set a group for a pipeline, please create the target group in advance. For detailed instructions, see [Pipeline group](https://docs.byteplus.com/en/docs/cp/Pipeline_group).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


* The number of stages supported by a single pipeline is less than or equal to 10.

* It is recommended to limit each pipeline to no more than 5 stages and each stage to no more than 30 serial tasks, to avoid system lag caused by excessive pipeline tasks.

* It is recommended to set the number of concurrent tasks in a single stage to no more than 9; exceeding this limit may cause the pipeline to fail.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

2. In the left navigation bar, select **workspace**. On the workspace page, click the name of the desired workspace to enter it.

3. Click **Create Pipeline** to open the **Pipeline Template Selection** dialog box.

   Select the appropriate pipeline template based on actual needs. You can choose either a predefined pipeline template or an enabled custom pipeline template. For detailed instructions on creating custom pipeline templates, see [Create pipeline templates](https://docs.byteplus.com/en/docs/cp/Create_pipeline_templates).

4. Click **OK** to enter the configuration page for the current pipeline.

   Configure the **Basic information**, **Process orchestration**, **Cache directory**, and **Notification** tabs as needed.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">During the configuration process, you can click <strong>Save to Drafts</strong> to temporarily save the current pipeline configuration as a draft, making it easier to continue editing next time.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Pipelines in Drafts do not check whether all required fields are complete and cannot be executed. After completing all required configuration items, you can save it as a standard pipeline.   </div>
   

5. After completing the configuration, click **Save** in the lower right corner to save the pipeline configuration.


The following sections provide a detailed introduction to the content and functions of the configuration items for the **Basic information**, **Process orchestration**, **Cache directory**, and **Notification** tabs.

<span id=".5Z-65pys5L-h5oGv"></span>
### Basic Information


* **Basic Information**

   
   |Configuration Item |Descriptions |
   |---|---|
   |Name |Display the default pipeline name. Custom pipeline names |
   |Workspace |Displays the workspace to which the current pipeline belongs. |
   |Pipeline group |Supports selecting the group for each pipeline to facilitate categorized management. By default, items are added to **Ungrouped**, which can be changed. |
   |concurrency lock |Optional configurations. After a concurrency lock is associated, the current pipeline run will be subject to the maximum concurrency constraint of that lock. |
   


<span id=".5rWB56iL57yW5o6S"></span>
### Process orchestration


* **Optional code source**

   Configure the code repository used by the pipeline. Currently, each pipeline only supports adding one code source.

   1. On the Process orchestration tab, click **Add \> Code source**.

   2. In the input source configuration panel, select the code repository type, code repository name, and select or enter the default branch for pipeline runs.

   3. After you finish selecting, click **OK**.

*  **(Optional) triggers**

   Configure triggers to automatically run the pipeline based on code source events, timers, or webhooks. For details, see [trigger](https://docs.byteplus.com/en/docs/cp/Trigger).

* **Optional variables**

   Pipeline global variable configuration Pipeline stages, tasks, and steps support using variables as dynamic parameters, enhancing the versatility of the pipeline. For a detailed introduction, see [Variable](https://docs.byteplus.com/en/docs/cp/Overview_of_variables).

* **Process orchestration**

   Define the execution order and specific content for each stage, task, and step in the pipeline. Process orchestration enables you to organically link components such as testing, building, deployment, and process control, allowing you to define your automated delivery process. For a detailed introduction, see [Process orchestration](https://docs.byteplus.com/en/docs/cp/Process_orchestration).


<span id=".57yT5a2Y55uu5b2V"></span>
### Cache directory

(Optional) Configure the cache directory for the build task. Enabling the cache prevents repeated downloads of dependencies during each build, greatly improving build speed. For more information, see [Cache directory](https://docs.byteplus.com/en/docs/cp/Cache_directory).


* The system provides default cache directories for build tools such as Maven, Gradle, and Node.js/npm. It is recommended that you enable the required cache directory according to your build tool.

* Allows you to add a cache directory and customize your project's cache path.


<span id=".6YCa55-l5o-Q6YaS"></span>
### Notification

Optional: Turn on pipeline notifications. Code Pipeline supports sending pipeline notifications via site messages, SMS, email, Webhook to help you quickly understand build and deployment results. For more information, see [Notification](https://docs.byteplus.com/en/docs/cp/Notification).
