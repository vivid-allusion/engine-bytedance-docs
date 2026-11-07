---
title: "Image source Webhook trigger"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Trigger_mirror_source_webhook"
---

CP can monitor Container Registry (CR) actions through the Webhook plugin. When an event that meets the Condition occurs, the pipeline is triggered automatically. This article describes how to configure the image source Webhook trigger rule.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

For users who use the Container Registry service, configuring the image source Webhook trigger rule enables automatic pipeline triggering after an image update. For example: After an image update, the pipeline's deployment task is triggered automatically.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The CP image source Webhook trigger feature can be linked with Container Registry event notification. In image acceleration scenarios, it automatically completes Nydus image conversion, reducing the image pull time during the container cold start stage. For specific operations, see <a href="https://docs.byteplus.com/en/docs/cp/Automatically_convert_Nydus_accelerated_images_via_pipeline?lang=en">Automatic conversion of Nydus acceleration image via pipeline</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The pipeline has been created. For specific operations, see [Create pipeline](https://docs.byteplus.com/en/docs/cp/Create_pipelines).

* The Container Registry instance, namespace, and OCI artifact repository have been created. For specific operations, see [Container Registry getting started](https://docs.byteplus.com/en/docs/cr/getting-started).

* The local environment has prepared images, which can be pushed to the Container Registry to trigger the source image Webhook. For specific operations on pushing images to the Container Registry, see [Push and pull image](https://docs.byteplus.com/en/docs/cr/push-and-pull-images?lang=en).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u5Yqo5oCB5Y-Y6YeP"></span>
### Step 1: Create dynamic custom variables

Custom pipeline dynamic variables are used to obtain the complete address of the image in the image source message.


1. Log in to the pipeline's process orchestration tab.

   1. Log in to the [CP Console ](https://console.byteplus.com/cp).

   2. In the left navigation bar, select **workspace**.

   3. Click the target workspace name to enter the current workspace.

   4. In the left navigation bar, select **pipeline** to enter the pipeline page.

   5. In the pipeline list, select the target pipeline and click  **`...`**   **\> edit** to enter the process orchestration tab of the current pipeline.

2. Click **Variable Management** to open the variable settings panel.

3. Switch to the **Custom variable** tab and click **add** to add a new custom variable.

4. Configure custom variables as required below. After configuration is complete, click **confirm**.

   
   |Parameter |Description |
   |---|---|
   |Parameter |Enter the name of the custom variable. The name must be unique within the same pipeline. It is recommended to avoid naming conflicts with built\-in variables. In this example, set as `image`. |
   |Type |Select the variable type. In this scenario, select **string**, and the user enters the default value. |
   |Default value |Enter the full image address to be used by default. |
   |Description |Enter the notes for the current variable. This field can be left blank. |
   |Privacy |Disable the privacy settings switch. |
   |Dynamic |Turn on the dynamic settings switch. |
   |Environment variable |After turning on environment variables, reference them as ${variable name} or $variable name. |
   


<span id=".5q2l6aqk5LqM77ya6YWN572u6ZWc5YOP5rqQLXdlYmhvb2st6Kem5Y-R6KeE5YiZ"></span>
### Step 2: Create image source Webhook trigger


1. In the pipeline process orchestration tab, in the **code source & trigger** panel, click **Add \> Trigger through image source Webhook**.

2. Configure the trigger rule as required. After configuration is complete, click **confirm**.

   
   |Parameter |Description |
   |---|---|
   |Trigger name |Name of the custom image source Webhook trigger. The image source Webhook trigger name must not be duplicated within the same pipeline. |
   |URL |Show the current pipeline's Webhook URL. The pipeline receives Container Registry Webhook Event notifications via this URL. |
   |Filters |Configure the trigger action and trigger condition for running the pipeline.<br><br><br>* **Trigger action**: Select the event that triggers the pipeline run. Currently, only **image push** is supported.<br><br>* **Trigger condition**: Optional configuration used for secondary filtering of image push events that meet the condition. If not configured, the effective scope of the event notification rules configured on the Container Registry side will be used.<br><br>   The trigger condition can include region, image type, instance name, namespace, OCI artifact repository, or tag. Currently, only one trigger condition is supported. Regular expressions are supported when entering the condition. For specific examples, see the console.<br><br>   For example: The trigger action is Image Push, and the trigger condition is `"data":{.*?"repository":"nginx"`. This means that when an Image Push Event occurs in the nginx Repository, the pipeline will be triggered to run. |
   |Runtime variable |Runtime variable is used to configure the actual value of the dynamic variable when the pipeline is triggered by the CR webhook. Support adding multiple dynamic variables, each bound to a different placeholder. For details on placeholders, see [built-in placeholders](https://docs.byteplus.com/en/docs/cp/Trigger_mirror_source_webhook?TagIDs=2,305&lang=en#Gc0x2Nlf) below.<br><br><br>* **Dynamic variable**: In the dropdown, select the dynamic custom variable set in [Step 1](https://docs.byteplus.com/en/docs/cp/Trigger_mirror_source_webhook?TagIDs=2,305&lang=en#.5q2l6aqk5LiA77ya6YWN572u5Yqo5oCB5Y-Y6YeP).<br><br>* **Runtime value**: Enter the placeholder, for example, `CR_PUSH_IMAGE_URL` which represents the full image address. |
   |Notes |Enter notes for the current trigger. This field can be left blank. |
   |Runtime branch |When the pipeline has a code source, it supports configuring the code branch used at runtime.<br><br><br>* Turn on: You can select the code branch to use when the pipeline is triggered by the image source. To use a non\-default branch when triggered by the image source, configure this parameter. For example: In the same pipeline, the code source's default branch is the main branch, but to have the image source trigger a specific branch, you can achieve this by configuring this parameter.<br><br>* Turn off: The pipeline will use the default branch configured in the code source when triggered by the image source. |
   

3. Click **Save** to save the pipeline configuration.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can reference the complete image address obtained from the CR Webhook message in subsequent pipeline deployment tasks by using $(parameters.variable_name) to upgrade the App image. For example: In this scenario, the variable name is set to <code>image</code>, so the reference method is <code>$(parameters.image)</code>.   </div>
   

<span id=".5q2l6aqk5LiJ77ya5ZyoLWNyLeS-p-WIm-W7uumVnOWDj-aOqOmAgemAmuefpeinhOWImQ=="></span>
### Step 3: Create image push notification rules

In the Container Registry Console, create and enable image push notification rules. For specific operations, see [Create image push notification rules](https://docs.byteplus.com/en/docs/cr/Create_notification_rules).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Fill the pipeline Webhook URL obtained in <a href="https://docs.byteplus.com/en/docs/cp/Trigger_mirror_source_webhook?TagIDs=2,305&lang=en#.5q2l6aqk5LqM77ya6YWN572u6ZWc5YOP5rqQLXdlYmhvb2st6Kem5Y-R6KeE5YiZ">Step 2</a> into the <strong>notification rules</strong>'s <strong>Target URL</strong>.</div>


<span id="Gc0x2Nlf"></span>
## Built\-in placeholders

When the image source Webhook trigger is triggered, the following content from the Container Registry push message can be assigned to dynamic variables using placeholders. Dynamic variables support adding multiple variables. Select variables from dynamic custom variables. The runtime value can be any of the following placeholders.


|**Image Source Message** |**Placeholder** |
|---|---|
|Full image address |CR_PUSH_IMAGE_URL |
|Repository Domain Name |CR_REGISTRY_HOST |
|Namespace |CR_NAMESPACE |
|OCI artifact repository |CR_REPOSITORY_NAME |
|Image tag |CR_IMAGE_TAG |
