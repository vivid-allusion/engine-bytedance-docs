---
title: "Creating a SenseFlow workflow"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Creating-a-SenseFlow-workflow"
---

A workflow enables you to visually orchestrate one or more operators to automatically process data in TOS buckets. These processes are carried out according to predefined procedures, resulting in automated, streamlined content processing. This topic uses the video transcoding operator to show how to create and debug a SenseFlow workflow.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">SenseFlow is currently in closed beta and is only available in China (Beijing). Please contact your account manager for access.</div>


<span id="AwdnmcNI"></span>
## Prerequisites


|Category |Description |
|---|---|
|Account registration and real name verification |Make sure that you have created a BytePlus account and completed real name verification. For more information, see [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/Account/sign-up-and-verify-byteplus-account?redirect=1). |
|Activating TOS |Make sure that you have [activated TOS](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1) for your account or Identity and Access Management users. |
|Creating a bucket |Make sure that you have [created a bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket) for storing the debug input and output. |


<span id="jkNs7mph"></span>
## Creating a workflow


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. Navigate to the **Workflow Management** page by doing one of the following:

   * In the left navigation pane, select **Content perception and processing \> Workflow Management**.

   * In the left navigation pane, click **Buckets**. Then, select the bucket you want to manage. In the left navigation pane, select **Data processing \> Workflow Management**.

3. On the **Workflow Management** page, click **Create workflow**. On the **Create workflow** page, complete the following steps:

   1. Click the edit icon in the upper\-left corner to modify the workflow name. For example, you could name it "VideoTranscoding". The name must be unique.

   2. Click  **+**  to add the **Video transcoding** operator, or drag it from the left panel into the workflow.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_838afd9b0f2e69c9deaa078264e6c566.png) </span>

4. Click the operator name and then configure the following parameters in the panel that appears.

   
   |Parameter |Description |
   |---|---|
   |Relative output path |Specify the relative path where you want the operator's debug output stored. For example:<br><br><br>* If the relative output path is **video/${RunID}/${InputName}.${Ext}** ,<br><br>* The absolute path in the bucket is tos://custom_output_path/**video/${RunID}/${InputName}.${Ext}**  |
   |Operator template |The system will automatically display a list of templates based on the selected operator. Select the template that corresponds to your desired output specifications.<br><br>For input and output specification details, see [Preset operators](https://docs.byteplus.com/en/docs/tos/Preset-operators). |
   

5. On the workflow creation page, click **Save and debug** in the upper\-right corner and configure the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Bucket |Select the bucket that contains the file you want to debug. |
   |Debug file path |Click **Select file** to specify the location of the file to be debugged.<br><br>The selected file must be smaller than 5 GB. Currently, only MP4 files are supported for the video transcoding operator. WAV files are supported for other operators. |
   |Artifact output path |Click **Select folder** to specify where you want the debug output to be stored. |
   

6. Click **Immediately debug** to submit the debugging task.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This process may take a while, so we recommend minimizing the window and continuing with other tasks.   </div>
   

7. View the results in the **View processing results** section, and locate the transcoded video file in **Artifact output path**.

   To restart debugging, click **Re\-debug** at the bottom.


<span id="1zsbQkcj"></span>
## Next steps


|Operation |Description |
|---|---|
|Create a SenseFlow template |You can use the workflow you just created to create a custom SenseFlow template. For more information, see [Creating a SenseFlow template](https://docs.byteplus.com/en/docs/tos/Creating-a-SenseFlow-template). |
|Create a SenseFlow rule |You can use a custom template to create a SenseFlow rule. For more information, see [Creating a SenseFlow rule](https://docs.byteplus.com/en/docs/tos/Creating-a-SenseFlow-rule). |
