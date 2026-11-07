---
title: "Trigger from code source"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Trigger_from_code_source"
---

Code Pipeline can monitor repository activity in the form of Webhook plugins, and will automatically trigger pipeline execution when qualifying code changes occur. This article describes how to configure code source trigger rules.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The pipeline has been created and the code source has been configured for the pipeline. For specific operations, refer to [Create a pipeline](https://docs.byteplus.com/en/docs/cp/Create_pipelines).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit

General Git does not support triggering a feature directly from the code source. To enable code source event triggering, configure the [standard Webhook trigger](https://docs.byteplus.com/en/docs/cp/General_webhook_trigger), and further configure the events to be pushed in your own code repository.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Go to the process orchestration tab of the pipeline.

   1. Log in to [Code Pipeline console](https://console.byteplus.com/cp).

   2. Select **workspace** in the left navigation bar.

   3. Click the target workspace name. Enter the current workspace.

   4. Select **pipeline** in the left navigation bar to enter the pipeline page.

   5. In the pipeline list, select the target pipeline, and click  **`...`**   **\> edit**, go to the process orchestration tab of the current pipeline.

2. Click the code source configuration box. In the pop\-up configuration input source panel, check the enable box for **Event Trigger**.

3. Configure event trigger rules.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Webhook URL |Display the Webhook URL for the current pipeline. The pipeline uses this URL to receive changes from the code repository. |
   |Trigger event |Select the specific trigger event, and set the corresponding trigger condition as needed. In Code Pipeline, different code source types support different trigger events. For a detailed introduction, please refer to [Trigger event and trigger condition](https://docs.byteplus.com/en/docs/cp/Trigger_events_and_trigger_conditions). |
   |Filter |For **code push** and **merge request create/update** events, you can configure filter conditions for event triggers to prevent the pipeline from being triggered frequently.<br><br><br>* **All events trigger execution:**  Each eligible Commit event will trigger pipeline execution.<br><br>* **Trigger execution only for the latest event:**  For commit events on the same branch, execute the pipeline for the latest event and cancel pipeline runs triggered by earlier commit events. This is mainly suitable for scenarios involving multiple commits, such as debugging code and fixing defects, which helps users reduce resource consumption. |
   |Auto comment |**Merge request creation/update** or **patch set creation** events trigger pipeline execution, and the pipeline's running status supports automatic synchronization as a comment under the corresponding merge request event in the code repository. Allows users to determine whether to merge code based on the execution results.<br><br><br>* **Pipeline running status and task status**: Synchronize the pipeline running status and task status in the comments of merge request events.<br><br>* **Pipeline running status**: Synchronize the pipeline running status in the comments of merge request events.<br><br>* **Do not comment**: Do not turn on this Auto comment feature.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The Auto comment feature requires that the code source Token have PullRequest permission.</div><br> |
   |Dynamic Parameter |Dynamic Parameter is used to configure the actual value of dynamic variables when the pipeline is triggered by the code source at runtime. If no configuration is provided, dynamic variables will use their default value. For example, as shown in the figure below, configure in advance the dynamic variables that you want the pipeline to pass. Set parameter a with a default value of 1, and turn on dynamic settings.<br><br><br>* Configure the Dynamic Parameter, select parameter "a", and set the runtime value to 10. When the pipeline is triggered by the code source, the value of a is 10.<br><br>* If the Dynamic Parameter is not configured, when the code source triggers the pipeline, the value of a will be the default value 1. |
   

4. Click **confirm** to complete the code source trigger settings.

5. Click **Save** in the lower right corner to save the pipeline configuration.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

Configure the pipeline's URL in your code repository; otherwise, the pipeline will not be able to properly receive event trigger messages from the code repository. For specific operations, refer to the following chapters.


* [Gitee webhook push configuration](https://docs.byteplus.com/en/docs/cp/Configure_Gitee_Webhook_push)

* [Configure GitLab webhook push](https://docs.byteplus.com/en/docs/cp/Configure_a_GitLab_webhook)

* [GitHub webhook push event configuration](https://docs.byteplus.com/en/docs/cp/Configure_GitHub_webhook_push)

* [Configure BitbucketCloud webhook push](https://docs.byteplus.com/en/docs/cp/Bitbucket_Cloud_webhook_configuration)

* [Configure webhook push in Codeup](https://docs.byteplus.com/en/docs/cp/Codeup_webhook_delivery_configuration)

* [Gerrit Webhook push configuration](https://docs.byteplus.com/en/docs/cp/Gerrit_webhook_push_configuration)
