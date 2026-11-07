---
title: "Getting started with BytePlus VOD"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
section: "Document"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-started"
---

To quickly get your first video online using BytePlus VOD, follow this end\-to\-end guide. You will learn the complete console\-based workflow: uploading a video file, processing it with a pre\-configured template, and generating a playback address to watch it in your browser.

<span id="de1084cd"></span>
## Prerequisites


* Prepare a video file.

* Prepare a valid domain name.

* [Create a BytePlus account](https://console.byteplus.com/auth/signup/) and sign in to the BytePlus console. If this is your first time accessing the BytePlus console, complete the authentication process and set up billing for your BytePlus account. For more information, see [Sign up and verify your BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).


<span id="002e95a8"></span>
## Procedure

<span id="b4e9d150"></span>
### Step 1: Enable the BytePlus VOD service

To enable the BytePlus VOD service, follow these steps:


1. Sign in to the [BytePlus](https://console.byteplus.com/auth/login/) console.

2. In the **Products** section, click **BytePlus VOD**.

3. Click **Request for access**.

4. Follow the instructions on the screen to activate the BytePlus VOD service.

5. After your service is enabled, sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas).


<span id="3f640366"></span>
### Step 2: Create a space

BytePlus VOD uses spaces as the basic unit for resource isolation. Each space can be configured with its own dedicated resources, templates, processes, and policies. To create a space, follow these steps:


1. Click **Spaces** on the left navigation bar.

2. Click **Create space**.

3. In the **Create space** dialog box, enter the required information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e148aab5ee9149f1b8b5567fc7b564e5~tplv-goo7wpa0wc-image.image) </span>

4. Click **OK**. The new space appears on the **Space management** page.


<span id="afc28097"></span>
### Step 3: Upload a video to the space

To upload a video to the space you created, follow these steps:


1. On the **Spaces** page, click **Enter the space** for the space you just created.

2. Click **Media assets** \> **Video** on the left navigation bar.

3. Click **Upload video** and add the file(s) you want to upload. You can:

   * Upload files from your local PC. This method is ideal for small uploads.

   * Upload files from URLs. This method is more suitable for large\-scale file migrations.

      The maximum size for a single audio or video file is 20 GB, regardless of the upload method.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d22ad27b2de459fa8ebbd361f9109ab~tplv-goo7wpa0wc-image.image) </span>

4. (Optional) Select a workflow. The console provides four [built-in workflows](https://docs.byteplus.com/byteplus-vod/docs/media-processing). You can use these workflows directly to process your file. If you do not select a workflow, files are uploaded directly without transcoding.

5. Click **Upload**. The console automatically navigates to the **Uploading** tab, which displays the upload status.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/956fe2a410684af8be287695237c0283~tplv-goo7wpa0wc-image.image) </span>


<span id="8c8734c8"></span>
### Step 4: Configure the media processing and workflow template

To enhance your audio and video files, process them in the BytePlus VOD console. You can use the pre\-built media processing and workflow templates available on the console or create custom ones tailored to your specific business requirements. For details, see [Media Processing](https://docs.byteplus.com/byteplus-vod/docs/media-processing).

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7a7b822f392473099199593adab36d6~tplv-goo7wpa0wc-image.image" width="864px" /></div>


<span id="30d1cd5a"></span>
### Step 5: Process the uploaded video

In this tutorial, we use the pre\-built workflow template, the single\-bitrate template for short video feeds, to process the uploaded video. Follow these steps:


1. In the **Uploaded** tab, select the video that you uploaded in Step 3.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7aa7e00112b04652b90cd7992287ecf6~tplv-goo7wpa0wc-image.image) </span>

2. Click the **Process video** button.

3. In the dialog box that appears, select a workflow template and click **OK** to start processing the video.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e7f745643014c61bf1f203b86ea2c0c~tplv-goo7wpa0wc-image.image) </span>

4. Check the progress of the task on the **Tasks \> Workflow management** page.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd48f3244120416dbca43377e96b5b2f~tplv-goo7wpa0wc-image.image" width="842px" />   </div>
   


<span id="ac04a496"></span>
### Step 6: Add the domain name

To accelerate content delivery for a particular website, you need to add the domain name to the BytePlus VOD console. Follow these steps:


1. Click **Accelerated distribution \> Domain names** on the left navigation bar.

2. Under the **Play domain name** tab, click **Add domain name**. The console uses the play domain name to generate playback addresses for your audio and video files.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24b9333b16814f5ab3df71d81b8e4505~tplv-goo7wpa0wc-image.image" width="842px" />   </div>
   

3. In the dialog box that appears, configure the following parameters for the domain name:

   1. Enter the domain name. Follow these rules:

      1. The domain name must be exact, such as `example.byte-test.com`. Wildcard domain names, such as `*.vod.com`, are not supported.

      2. Capital letters are not supported.

      3. Duplicate domain names are not supported. A domain name is considered a duplicate if it is already in use by another BytePlus CDN\-related service.

   2. Select whether to redirect to BytePlus VOD origin servers or third\-party origin servers.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a684683d66614fe2abb9d121f1c70db3~tplv-goo7wpa0wc-image.image) </span>

4. Click **OK**. After you add a domain name, it appears in the domain name list with a **Configuring** status. Once the configuration is complete, the status changes to **Configuration complete**. BytePlus VOD will automatically assign a CNAME record for your domain, which you can find in the **CNAME** column of the domain name list.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8da574f1eebe48ed88375d6aa5091ad3~tplv-goo7wpa0wc-image.image) </span>

5. Click **Enable** to enable the domain name.


<span id="bf087908"></span>
### Step 7: Get the playback address

To get the playback addresses of the original and processed videos, follow these steps:


1. Click **Media assets** \> **Video** on the left navigation bar.

2. Find the target video and click **View details**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc25737c37ca4d45a93611286e1143b7~tplv-goo7wpa0wc-image.image) </span>

3. In the dialog box that appears, click the **Video address** tab.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd504cf2afeb4f899fd7183c30bea83e~tplv-goo7wpa0wc-image.image" width="842px" />   </div>
   

4. Click **Publish**. You can then either copy the playback addresses of the original and processed videos or preview them directly in your browser.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7822ef0482ed4b8793ea91bd8e67f78a~tplv-goo7wpa0wc-image.image" width="842px" />   </div>
