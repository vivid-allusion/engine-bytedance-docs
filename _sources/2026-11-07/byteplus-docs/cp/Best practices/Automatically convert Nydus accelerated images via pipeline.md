---
title: "Automatically convert Nydus accelerated images via pipeline"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Automatically_convert_Nydus_accelerated_images_via_pipeline"
---

This article describes how to leverage the integration capabilities of BytePlus CP with Container Registry to automatically trigger a pipeline to complete the conversion and push the Nydus accelerated image back after pushing the original image, achieving a fully automated image acceleration workflow where conversion occurs upon push.

<span id="v9MT4sr8"></span>
## Background

Nydus is a container image acceleration format that supports lazy loading, which can significantly reduce the image pull time during container cold start. BytePlus Container Registry supports managed OCI standard\-compliant cloud\-native artifacts, including Nydus format accelerated image copies.

Business images are typically pushed to the Container Registry via pipelines. By connecting the event notification of the Container Registry with CP's image source Webhook trigger, each time an original image is pushed, a pipeline is automatically triggered to convert and generate an accelerated image with the \-nydus suffix, without any manual intervention throughout the process.

<span id="w5xLRlv5"></span>
## Implementation process

The overall process for automatic Nydus image conversion is shown in the following diagram.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4061de8c608bfafc07c96f4a829b9bcb.png) </span>

<span id="qlDlHW40"></span>
## Prerequisites


* An instance, a namespace, and an OCI artifact repository (`golang-demo-app`) have been created in the Container Registry [ ](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance?lang=en)[ ](https://docs.byteplus.com/en/docs/cr/create-a-namespace?lang=en)[ ](https://docs.byteplus.com/en/docs/cr/create-an-OCI-repository?lang=en).

* The image has been prepared in the local environment.


<span id="krnR7sGk"></span>
## Procedure

<span id="zk7UjQ8o"></span>
### Step 1: Create a pipeline

Create a pipeline for Nydus conversion in BytePlus CP.


1. Log in to the [CP Console](https://console.byteplus.com/cp).

2. In the left navigation bar, select **Workspace**, click the target workspace name on the workspace page to enter the current workspace.

3. On the right **Pipeline** page, click **Create Pipeline.** 

4. In the **Select Pipeline Template** dialog box, select **Blank Template**, and click **Create**.


<span id="9rtCD8xP"></span>
### Step 2: Add a dynamic custom variable named tag

Create a dynamic custom variable `tag` in the pipeline. In the subsequent **Nydus image conversion** task, use the custom variable `$(parameters.tag)` to dynamically set the version number of the converted image.


1. On the **Process Orchestration** page, click **Variable Management \> Custom Variable \> Add.** 

2. Configure the parameters of the custom variable, and click **Confirm** after completion. This document only describes the parameters relevant to this scenario. For a complete description of parameters, see [Custom variables](https://docs.byteplus.com/en/docs/cp/Custom_variables?lang=en).

   
   |Parameter |Description |
   |---|---|
   |Parameter |Enter the name of the custom variable. In this example, `tag`. |
   |Type |Select the type of variable. In this example, select **string.**  |
   |Dynamic |Whether to turn on the dynamic settings switch. In this example, the switch is enabled. |
   


<span id="MXyREuC1"></span>
### Step 3: Add **Nydus image conversion**


1. In **Process orchestration**, click  ** + \> Add task.** 

2. In **Step**, click **Add \> Image \> Nydus image conversion.** 

3. Configure task parameters. After completion, click **confirm**. This document only describes the parameters related to Nydus image task conversion. All other parameters remain at their default values.

   
   |Parameter |Description |
   |---|---|
   |Step name |The default is **Nydus image conversion**, and custom step names are supported. |
   |Source image region |Select the region of the container registry to which the image to be converted belongs. For currently supported regions, see [Container Registry Service region](https://docs.byteplus.com/en/docs/cr/Region).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Due to network impact, using the public resource pool to push to the Johor region may take a long time. It is recommended to use the private resource pool to push tasks to Johor.</div><br> |
   |Source container registry instance |Select the container registry instance of the image to be converted in [prerequisites](https://docs.byteplus.com/en/docs/cp/Automatically_convert_Nydus_accelerated_images_via_pipeline?TagIDs=2,305&lang=en#qlDlHW40). |
   |Source namespace |<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The namespace must already exist; otherwise, the push will fail with error 401 Unauthorized.</div><br><br><br>Select the repository namespace of the image to be converted in [prerequisites](https://docs.byteplus.com/en/docs/cp/Automatically_convert_Nydus_accelerated_images_via_pipeline?TagIDs=2,305&lang=en#qlDlHW40). |
   |Source OCI artifact repository |Select the OCI artifact repository of the image to be converted in [prerequisites](https://docs.byteplus.com/en/docs/cp/Automatically_convert_Nydus_accelerated_images_via_pipeline?TagIDs=2,305&lang=en#qlDlHW40). This example uses `golang-demo-app`. |
   |Source image tag |Use the custom variable `$(parameters.tag)` to dynamically set the version number. |
   


<span id="5LsmRSb8"></span>
### Step 4: Create image source webhook trigger


1. In the pipeline's **Process orchestration** tab, in the **code source and trigger** area, click **Add \> Image source webhook trigger**.

2. Configure the trigger rule. After configuration is complete, click **confirm**. This document only describes the parameters relevant to this scenario. For a complete description of parameters, see [Image source webhook trigger](https://docs.byteplus.com/en/docs/cp/Trigger_mirror_source_webhook?lang=en).

   
   |**Parameter** |**Description** |
   |---|---|
   |Trigger name |Custom name for the image source webhook trigger. |
   |URL |<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When you create <strong>Event notification</strong> in the container registry later, you need to enter this value in <strong>Target URL</strong>.</div><br><br><br>The current pipeline's webhook URL. The pipeline receives webhook event notifications from the container registry through this URL. |
   |Filters |Configure the trigger action and trigger condition for running the pipeline.<br><br><br>* **Trigger action**: Select the event that triggers the pipeline. In this example, select **Image Push**.<br><br>* **Trigger condition**: In this example, enter `"data":{.*?"repository":"golang-demo-app"`. The pipeline is triggered when an image is pushed to the `golang-demo-app` OCI artifact repository. |
   |Runtime variable |This is the actual value used for the dynamic variable when configuring a Container Registry Webhook to trigger a pipeline.<br><br><br>* Dynamic variable: In this example, add the custom dynamic variable created in [Step 2](https://docs.byteplus.com/en/docs/cp/Automatically_convert_Nydus_accelerated_images_via_pipeline?lang=en) to dynamically set the version number of the converted image. Click **Add** and select `tag`.<br><br>* Placeholder: Enter `CR_IMAGE_TAG`. |
   

3. Click **Save** to save the pipeline configuration.


<span id="eXnf9iNO"></span>
### Step 5: Configure container registry event notification

Create event notification rules in the Container Registry CR so that after the original image is pushed, a webhook can be sent to the pipeline trigger.


1. Log in to the[ CR console](https://console.byteplus.com/cr).

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Event notification**.

4. On the **Event notification** page, click **Create notification rule**.

5. Configure rule parameters. This document only describes the parameters relevant to this scenario. For a complete parameter description, see [Create image push notification rule](https://docs.byteplus.com/en/docs/cr/Create_notification_rules?lang=en).

   
   |Parameter |Description |
   |---|---|
   |**Effective scope** ||
   |Effective level |Select **OCI artifact repository**. |
   |Instance |Select the instance to which the image to be converted belongs. |
   |Namespace |Select the namespace to which the image to be converted belongs. |
   |OCI artifact repository |Select the OCI artifact repository to which the image to be converted belongs. This example uses `golang-demo-app`. |
   |Artifact repository type |Select **Image**. |
   |Tier |In this example, select **Regular expression matching**, and enter `^(.{1,5}\|.*[^s]\|.*[^u]s\|.*[^d]us\|.*[^y]dus\|.*[^n]ydus\|.*[^-]nydus)$` to exclude version numbers ending with `-nydus`. |
   |**Notification rules** ||
   |Rule state |Click **Enable** to enable the notification rule. |
   |Notification method |Select **HTTP(s)** . |
   |Target URL |The URL that is invoked when the event is triggered. The notification payload is sent to this URL. In this example, enter the Webhook address of the CP trigger in [Step 4](https://docs.byteplus.com/en/docs/cp/Automatically_convert_Nydus_accelerated_images_via_pipeline?lang=en). |
   |Custom Header |Supports defining custom Header for the request sent to the target URL based on your service. |
   


<span id="g51MpCLF"></span>
## Validate results

After completing the above configuration, pushing an original image will trigger the entire automatic conversion chain.


1. Push the original image to the Container Registry using the following command. For details on push image actions, see [Push and pull artifacts](https://docs.byteplus.com/en/docs/cr/push-and-pull-images?lang=en#f5HFyORf).

   ```Bash
   docker push ****-ap-southeast-1.cr.bytepluses.com/****/golang-demo-app:0.0.2
   ```
   

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260630090656-1619645431323.png) </span>

2. In the image list of the target OCI artifact repository in the Container Registry (in this example, golang\-demo\-app), the presence of an accelerated image replica with the `-nydus` suffix indicates that the operation was successful.
