---
title: "Intelligent video understanding"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-ai-media-understanding"
---

BytePlus VOD uses ModelArk models to analyze video content and generate summaries, viral moment analysis, plot breakdowns, and smart tags. You can run understanding tasks for existing videos or trigger them when uploading local videos. This guide explains how to configure preprocessing, authorize model services, choose prompts, and retrieve results.

## Use cases

* **Batch video preprocessing:**  Suitable for large\-scale batch preprocessing and understanding of video datasets to generate training data for large models. Can be used in conjunction with VOD's core services and large model video understanding capabilities.

* **Content summarization:**  Suitable for scenarios that require a quick grasp of a video's core content — such as users browsing video summaries or video editors performing initial content screening.

* **Viral moment analysis:**  Suitable for analyzing the virality mechanics of popular videos, helping content creators, marketing teams, or platform operators understand why a video went viral in order to optimize content strategy.

* **Plot breakdown:**  Suitable for detailed analysis of video content, such as deconstructing educational and training videos or analyzing the storyline of short dramas.

* **Tag extraction:**  Suitable for video classification, tagging, and retrieval scenarios — such as managing video libraries, optimizing content recommendation systems, or enabling users to quickly find relevant videos by tag.

## Pricing

Using the intelligent video understanding feature may incur the following costs:

* **ModelArk large model fee:**  ModelArk converts all input content into tokens for billing purposes. For pricing details, refer to [ModelArk Pricing](https://docs.byteplus.com/en/docs/modelark/model-pricing).

* **ASR fee:**  When ASR is enabled, audio will be transcribed into text during processing, which incurs a streaming speech recognition service fee. For pricing details, refer to [ASR Pricing](https://docs.byteplus.com/en/docs/byteplusvoice/asrbilling).

* **Snapshot fee:**  Snapshots generated during video understanding are billed by the number of images under the VOD snapshot billing item. See [Pay-as-you-go pricing](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing).

* **VikingDB fee:**  Semantic search may incur VikingDB compute, storage, and embedding fees. VikingDB uses pay\-as\-you\-go billing with hourly settlement. For billing details and current rates, see [VikingDB pricing](https://docs.byteplus.com/en/docs/VikingDB/Billing_of_a_vector_database).

## How it works

VOD prepares the selected video or time range, runs the configured preprocessing tasks, and passes the resulting video and text context to the model together with your prompt. The task runs asynchronously. After it completes, you can inspect the output in the task details and view supported structured results in the media asset details.

![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261022095449-1319827700003.png)

## Prerequisites

* Create a [BytePlus account](https://console.byteplus.com/auth/signup/) and sign in to the BytePlus console.

* Enable the [BytePlus VOD service](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started) and create a space.

* To process existing videos, [upload video files](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview) to the target space and obtain the Vid or FileName. You can also configure understanding during a local upload as described below.

## Use intelligent video understanding via the console

This section provides step\-by\-step instructions for using the intelligent video understanding feature.

### Step 1: Initiate intelligent video understanding

1. [Sign in to the VOD console](https://console.byteplus.com/vodpaas) and enter the specific space.

2. On the **Uploaded** tab, select one or more videos, then choose **AI processing** \> **Intelligent video understanding**.

   ![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261022071537-1329248291968.png)

3. In the **Intelligent video understanding processing** panel, complete **Pre\-processing configuration**, **Model service authorization**, **Parameter configuration**, and **Prompt editing**. Expand a section to review or change its configuration.

### Step 2: Pre\-processing configuration

Choose the preprocessing tasks for the video.

|Option |Description |
|---|---|
|Snapshot |Extract frames at regular intervals for visual analysis. Set **Resolution** to 240p, 360p, 480p, 720p, or 1080p, and configure **FPS**. |
|ASR transcription |Convert speech to text for the model. Requires an activated Seed Speech application. |
|Vocal/background sound separation |Separate the voice track before transcription. Takes effect only when ASR is enabled. |
|OCR |Extract text from video frames. Videos longer than 10 minutes are not supported. |
|Scene segmentation |Supply scene time ranges as context for understanding. This does not generate separate scene video files. |
|Processing time |Select **Full film** or **Specified duration**. For a specified duration, enter **Start time (seconds)**  and **End time (seconds)** . |

Click **Continue** after configuring preprocessing.

### Step 3: Model service authorization

Before the pipeline can invoke any AI inference, the required model services must be enabled and authorized under your account.

#### Enable large models and create inference nodes

Enable a vision\-language model and provision an inference node. Select a model from the Dola\-Seed\-2.0 series, as these models are optimized for video understanding tasks.

1. Click **Enable** to navigate to the [ModelArk Console](https://console.byteplus.com/ark/region:ark+ap-southeast-1/endpoint).

2. Under the **Model inference access point** tab, click **Create inference endpoint**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d80575fd310541cd84a7517c96519df2~tplv-goo7wpa0wc-image.image)

3. Complete the following configuration as prompted:

   1. Enter a name for the endpoint.

   2. Select a model. The `Dola-Seed-2.0-pro` model is recommended for best results.

   3. Once configured, click the **Create** button on the right side of the page.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f18189cada4e42bd8dab5b7fd7406f7a~tplv-goo7wpa0wc-image.image)

4. After the inference endpoint is created, return to the Online inference page and save the **Endpoint ID**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/362ae4ab2c2245feb79384a0cfa01463~tplv-goo7wpa0wc-image.image)

#### Enable VikingDB service

1. Click **Enable** to navigate to the [VikingDB Vector Database Console](https://console.byteplus.com/vikingdb).

2. Activate the vector database as prompted.

![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261022090819-495572770968.png)

#### Enable ASR service and obtain APP ID

This configuration is required only when **ASR transcription** is enabled in [Pre-processing configuration](https://docs.byteplus.com/en/docs/25/123493#preprocessing). Enabling ASR displays the ASR service setup entry and the **ASR AppID** field in **Parameter configuration**. When ASR is disabled, these controls are hidden and you can skip this section.

1. Go to the [Application Management page](https://console.byteplus.com/voice/app) in the Seed Speech console.

2. Click **Create an application**.

3. Enter the application name and description, and select ASR streaming service.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f26f99381e046049a8be574e57bb8c6~tplv-goo7wpa0wc-image.image)

4. After the application is created, return to the Application Management page and save the **APP ID**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ea26657ce2d48e68929b07081f4d954~tplv-goo7wpa0wc-image.image)

#### Complete cross\-service authorization

Grant VOD access to the Seed models on ModelArk by clicking **Authorize**. If the status already shows **Authorized**, no further action is required.

![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261022091036-706112762800.png)

### Step 4: Parameter configuration

Enter the credentials obtained in the previous step to connect the pipeline to the required model services.

|Field |Required |Description |
|---|---|---|
|Large model EndPointID |Yes |The Endpoint ID of the inference node created in ModelArk. |
|ASR AppID |When ASR transcription is enabled |The APP ID of an activated ASR application created in Seed Speech. This field is displayed only when **ASR transcription** is enabled. |

Use valid IDs from activated services. A task can be submitted with an invalid endpoint ID or ASR AppID and then fail during execution.

### Step 5: Configure prompts

Expand **Prompt editing**. Use **Click to view** next to **Files** to review the selected videos, then choose **System capability assembly** or **Custom prompt**.

> **Note**

> To save the output as structured media asset information, preserve the output field names, hierarchy, and data types required by the corresponding VOD prompt template. Output that does not follow the required schema can still be viewed in the task details, but cannot be saved as structured understanding results on the media asset.

#### Built\-in prompts

1. Select **System capability assembly**.

2. Select one or more capabilities from the following table.

3. Click **Prompt generation** to generate the combined prompt. Review **Prompt Template**; the generated template can be viewed and copied but cannot be edited directly.

|Capability |Result |
|---|---|
|Content summary |A summary of the main subjects and events. |
|Smart Tags |Tags that describe the video content. |
|Burst point analysis |Highlights and an explanation of their appeal. |
|Plot analysis |An analysis of the video's storyline. |

#### Custom prompts

1. Click **Custom prompt** to open **Custom Prompt Management** panel.

2. Select an existing prompt, or click **New Prompt**.

3. For a new prompt, select **Prompt type**, enter **Prompt name** and **Prompt content**, then click **Save**. The content field allows up to 2,000 characters.

You can view, edit, and delete custom prompts in the prompt list. System presets cannot be modified or deleted.

### Step 6: Submit an intelligent video understanding task

Once all steps are configured, click **Start processing** to submit the video understanding task.

### Step 7: Check task status and retrieve results

1. After submitting the task, the system processes it asynchronously. Navigate to **Media processing** \> **Tasks** in the left navigation bar to check the target task status.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e528fb6e0b2f4e9aa2317e9255e2318f~tplv-goo7wpa0wc-image.image)

2. Click **View details** to inspect the task output. To view media asset results, return to **Media assets** \> **Videos**. The **AI Label** and **AI summary** columns display the generated tags and summary directly in the video list. For more details, click **Details** for the video and open the **Video understanding** tab.

   ![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261022092623-1734918442818.png)

   ![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261022104449-355469677815.png)

## Trigger understanding when uploading

1. On the **Videos** page, click **Upload video** and choose **Local upload**. Add the files to upload.

2. Under **Upload process**, select **Upload and trigger the AI understanding task**.

   ![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261022092806-550251036171.png)

3. Click **Configure**. Configure preprocessing, the processing time range, model services, parameters, and the prompt.

4. Click **Complete configuration**, then click **Upload** on the upload page. The understanding task starts after the upload.

If the AI understanding configuration is incomplete, the page warns that uploading will not trigger the understanding task. For other upload options, see [Uploading an audio or video file](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload#261ef51f).

## Search by video content

After videos have structured understanding results, you can use the semantic search entry on the **Videos** page or query through the API.

> **Note**

* > Semantic search is available only for newly uploaded videos that have completed intelligent video understanding. Previously uploaded videos are not eligible for semantic search.

* > Semantic search uses VikingDB retrieval. Results depend on the understanding content and the query; review the returned videos to confirm relevance.

### Search in the console

1. Choose **Media assets** \> **Videos** and open the **Uploaded** tab.

2. Enter a natural\-language query in **Search in one sentence**, such as `female`.

3. Click **Search**.

![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261022093251-230216934029.png)

### Search through the API

After videos have structured understanding results, pass a natural\-language query in `SemanticText` to [GetMediaList](https://docs.byteplus.com/docs/byteplus-vod/reference-getmedialist).

## Use intelligent video understanding via the API

### Step 1: Enable and authorize model services

Complete the [model service authorization](https://docs.byteplus.com/en/docs/25/123493#service-authorization) described above. Keep the ModelArk endpoint ID and, if ASR is enabled, the Seed Speech application ID available for the request.

### Step 2: Submit a task

Call [MediaUnderstand](https://docs.byteplus.com/docs/byteplus-vod/reference-mediaunderstand) with API version `2026-08-01`:

* Use `Input.Type=Vid` with the video ID, or `Input.Type=DirectUrl` with the space name and file path.

* Set `Operation.Prompt` and `Operation.Model`. Choose `ModelType=VLM` for visual analysis or `ModelType=LLM` for analysis of text context from ASR or OCR.

* When enabling `AsrParam`, provide `Model.SpeechAppId` and `Model.SpeechAppType`. BytePlus supports the duration\-based ASR 1.0 and ASR 2.0 types listed in the API reference; speaker identification is not supported.

* Configure the optional time range and preprocessing parameters as needed.

The `StartExecution` task type `Vision` and its associated parameters are deprecated. Migrate existing integrations to [MediaUnderstand](https://docs.byteplus.com/docs/byteplus-vod/reference-mediaunderstand) using the request structure described above. The [legacy Vision reference](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-video-understanding) is retained for reference.

### Step 3: Retrieve the results

Save the `RunId` returned by `MediaUnderstand`, then call [GetExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-getexecution) with version `2025-07-01` to query the task status and output. Task submission and task completion are separate: wait for processing to complete before consuming the result.

For these tasks, read the generated text from `Result.Output.Task.VideoUnderstand.Content`. Check both `Result.Status` and `Content`: a task can return `Success` with empty content.
