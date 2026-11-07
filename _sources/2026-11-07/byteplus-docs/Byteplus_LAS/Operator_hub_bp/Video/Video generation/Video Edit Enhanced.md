---
title: "Video Edit Enhanced"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Enhanced_video_editing"
---

The enhanced version of the video editing online service combines input videos and reference images to perform targeted video replacement. It is suitable for scenarios such as advertising material remastering, product replacement, background redrawing, and creative video editing.

<span id="dbf3ec4d"></span>
# Operator introduction

> Operator ID: las_video_seedance_replace


<span id="2690ee76"></span>
## Core capabilities


* The current version supports several types of intelligent video editing tasks, including scene replacement (`scene_replace`), object replacement (`object_replace`), and person replacement (`person_replace`).

   * Scene replacement (`scene_replace`): Retains the people, products, actions, and shot structure in the original video, while replacing the background or environmental style.

   * Object replacement (`object_replace`): Replaces the target object in the video with a specified style or product based on a reference image.

   * Person replacement (`person_replace`): Replace the target person in the video with a specified person based on a reference image.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">To use the person replacement feature, you must apply to enable the LAS asset managementfunction (allowlist feature, disabled by default) and set <code>seedance_use_asset_api = true</code> when submitting a person replacement task.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Required audio, video, or image assets for person replacement:      </div>
      

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">You can manually upload assets to the LAS asset library first, and then provide the asset to the operator by specifying the LAS asset ID when submitting the task.      </div>
      

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">You can also provide assets directly to the operator via HTTPS or TOS paths. In this scenario, LAS will automatically upload the asset to LAS asset management and use the asset ID as input. After the operator task is completed, the automatically uploaded asset will be cleaned up.      </div>
      

* Ensures the quality and stability of video editing results.

   * Supports supplementing natural language editing constraints via `user_prompt`, such as retaining actions, removing watermarks, avoiding subtitles, or controlling details of the style.

   * Supports automatic evaluation and retry for a limited number of times, helping to achieve more stable replacement results with complex materials.

   * Supports returning the final video result and diagnostic file (`result.json`), making it convenient for the user to retain generated results and process information.


<span id="615f271a"></span>
## Effect showcase


---



<div style="text-align: center">
<strong>[Person replacement]</strong></div>



* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41c2d4a2580d4ce7925efabf7404cb84~tplv-goo7wpa0wc-image.image" controls></video>


* Reference image

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/196389bf048a4e15be758e9c10e2910d~tplv-goo7wpa0wc-image.image) </span>

* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2885b45f0cc468bbc25b62e96ce09aa~tplv-goo7wpa0wc-image.image" controls></video>


* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7c67d7aa2db4da8937448322967d33a~tplv-goo7wpa0wc-image.image" controls></video>


* Reference image

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/883ee6a291cf44fc85448e3f6169c953~tplv-goo7wpa0wc-image.image) </span>

* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff99068f313441f8b92a51909a363e5d~tplv-goo7wpa0wc-image.image" controls></video>




---



<div style="text-align: center">
<strong>[Environment and object replacement]</strong></div>



* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38db7b1698f44ed4826a3d35e1d79f99~tplv-goo7wpa0wc-image.image" controls></video>



Scenario 1: Background replacement


* Reference image

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a612d5528b2445f8f49d8134b53a268~tplv-goo7wpa0wc-image.image) </span>

* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3870a70940944ab7a9fa927c1a05f301~tplv-goo7wpa0wc-image.image" controls></video>



Scenario 2: Object replacement


* Reference image

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/031c00f59b79461d8ddf56940c314a3e~tplv-goo7wpa0wc-image.image) </span>

* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d55ee23f381d4a709c01eed23ea06aa7~tplv-goo7wpa0wc-image.image" controls></video>




---



<span id="5654dc69"></span>
## Supported regions


* Asia Pacific(Johor)：ap\-southeast\-1


<span id="a8cce5db"></span>
## Operator performance


|Sub\-items |Performance impact description |
|---|---|
|Maximum RPM |600 |
|Maximum concurrency |10 |
|Processing time |Total processing time depends on the video duration, the number of reference images, the complexity of the replacement, whether retry is enabled, and the network environment.<br><br><br>* Enabling retry (`enable_retry`) increases the success rate and stability of generation, but significantly increases overall processing time and cost. |
|Processing result quality |The quality of video content replacement processing results depends on whether a reference image is provided and the content of the reference image.<br><br><br>* It is recommended to provide reference images as three\-view diagrams plus detail close\-ups. Especially for scene replacement, keeping the reference image's perspective and distance consistent with the original video can significantly increase the probability of successful replacement. |


<span id="3fb4d549"></span>
# Input and output requirements

<span id="14f5b42c"></span>
## Input requirements


|Subdivision |Details |
|---|---|
|Supported input data modalities |* Video<br><br>* Image<br><br>* Audio |
|Input format: Video |* Format: mp4, mov<br><br>* Size: `2-15` seconds. The input size for a single video must not exceed 200 MB.<br><br>* Resolution: 480p, 720p, 1080p<br><br>* Dimensions:<br><br>   * Aspect ratio (width/height): [0.4, 2.5]<br><br>   * Width and height (px): [300, 6000]<br><br>   * Total pixel count: [640x640=409600, 2206×946=2086876], meaning the product of width and height must fall within the range [409600, 2086876].<br><br>* Other: It is recommended to use video material with a clear subject and a relatively stable camera. |
|Input format: Image |* Format: jpeg, png, webp, bmp, tiff, gif, heic, and heif.<br><br>* Quantity: Supports input of `1-9` reference images.<br><br>* Size: Each image must be less than 30 MB.<br><br>* Resolution: Width and height (px): (300, 6000); aspect ratio (width/height): (0.4, 2.5)<br><br>* Other: It is recommended that the reference images provided include three\-view diagrams and detailed close\-ups. |
|Input format: Audio |* Format: wav, mp3<br><br>* Size: Audio duration [2,15] seconds. Each audio file must not exceed 15 MB. |
|Input path requirements |Provide input data to the operator via request parameters `video_url`, `image_urls`, and `audio_url`. Currently, the following methods are supported: public URL, TOS path, and Base64 encoding (only supported for images and audio).<br><br><br>* **Public URL**: A video URL accessible via the public network, with the format `http/https`.<br><br>* **TOS path**: After uploading the data to be processed to a TOS Bucket under the same primary account and region as the current LAS service, you can provide the TOS path, with the format `tos://bucket_name/demo`.<br><br>* **Base64 encoding** (only supported for images and audio): Convert the local file to a Base64 encoded string, then submit it to the model. Do not use Base64 encoding for large files.<br><br>   * Image input must follow the format: `data:image/<image format>;base64,<Base64 encoding>`. Note that `<image format>` must be in lowercase, for example, `data:image/png;base64,{base64_image}`.<br><br>   * Audio input must follow the format: `data:audio/<audio format>;base64,<Base64 encoding>`. Note that `<audio format>` must be in lowercase, for example, `data:audio/wav;base64,{base64_audio}`.<br><br>* **LAS asset ID**: The ID used for generating real and virtual portraits in videos, following the format: `asset://<asset-id>`.<br><br>   * When using the LAS asset ID method, you must first apply to enable the LAS asset management function (allowlist feature, disabled by default), and set `seedance_use_asset_api = true` when submitting the task.<br><br>   * When submitting various types of tasks, if the input material involves real\-person audio, video, or images, you must first upload the material to the LAS asset library and provide the corresponding material to the model using the LAS asset ID. Otherwise, the task may be blocked.<br><br>   * After enabling the feature and uploading materials, you can view the list of asset groups in the under asset management \> Virtual Portrait Asset. On the asset group details page, you can obtain the specific asset's asset ID (`asset-id`), which can then be concatenated in the above format to be used as input for the operator. |


<span id="df0c4c27"></span>
## Output requirements


|Subdivision |Details |
|---|---|
|Output data modality |* Video<br><br>* Text (JSON file) |
|Output format: Video |* Size: The output video duration is within the range of `4-15` seconds.<br><br>* Aspect ratio: Original video ratio (default), 16:9, 9:16, 1:1, 4:3, 3:4, 21:9, 9:21.<br><br>* Resolution: Supports setting to 480p, 720p, 1080p. If not set, the output will be processed automatically according to the input video.<br><br>   * If a unified output resolution is required, it is recommended to set the output resolution value via the `seedance_resolution` parameter.<br><br>   * If the output video resolution is not explicitly specified, it will match the input video resolution. |
|Output path: TOS |Specify the storage path for the operator's output results via the request parameter `output_tos_path`. Currently, setting to a TOS path is supported.<br><br><br>* TOS path: A TOS Bucket directory with write permissions under the same primary account and region as the LAS service. |


<span id="14a99ab6"></span>
# Billing instructions


* Billing standards

   
   |Breakdown |Billing standards description |
   |---|---|
   |Billing item |Duration of input/output video. |
   |Billing type |Usage\-based billing, unit: USD/second, billed hourly based on actual billing quantity. |
   |Unit price |Depends on the algorithm service version you select (basic version, enhanced version). |
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Total cost per task: In addition to the unit price, it also depends on the duration of the input/output video and the resolution of the input/output video.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you enable retry based on evaluation results (<code>"enable_retry"= "true"</code>), each retry will submit a new task and will be billed separately.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For example, after your task runs, if the evaluation result does not meet the standard and you retry twice, there will be costs for three video editing tasks in total.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only tasks that successfully generate videos will incur costs. Scenarios where video generation fails due to review or other operational reasons will not be charged.   </div>
   

* Billing details

   Billing estimate: `Total cost ≈ unit price * billing quantity = unit price * (video duration * duration conversion coefficient)`

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The above formula is for cost estimation only. Actual billing is based on the bill.   </div>
   

   
   |Version breakdown |Unit price |Billing item: Video duration |Duration conversion coefficient: Related to video resolution |
   |---|---|---|---|
   |Basic version |0.242 USD/second |Input video duration + output video duration |`seedance_model` set to seedance 2.0\-fast:<br><br><br>* 480P：0.2770<br><br>* 720P：0.5988 |
   ||||`seedance_model` set to seedance 2.0\-mini:<br><br><br>* 480P：0.1769<br><br>* 720P：0.3812 |
   |Enhanced version |0.303 USD/second |Input video duration + output video duration |`seedance_model` set to seedance 2.0:<br><br><br>* 480P：0.2830<br><br>* 720P：0.6098<br><br>* 1080P：1.5251<br><br>* 4k：3.1348 |
   ||||`seedance_model` set to seedance 2.5:<br><br><br>* 480P：0.406<br><br>* 720P：0.9125 |
   

* Billing example

   * Example scenario: Using video generation \- enhanced version (Seedance 2.0 model) for video generation, retry option not enabled, input includes a reference video (duration 10 seconds), output video duration is 10 seconds, resolution is 1080p.

   * Cost details:

      `Total cost ≈ unit price * billing quantity = 0.303 USD/second * (10 seconds + 10 seconds) * 1.5215 = 9.2421 USD`


<span id="27567e1f"></span>
# Caution and prerequisites


|Details |Caution and prerequisites |
|---|---|
|Costs |Before calling an operator, you need to understand the model invocation costs associated with using the operator. For details, see [Large model billing](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |


<span id="c2fa484f"></span>
# Rest API call

<span id="57883dd8"></span>
## API usage instructions

The operator's API is an asynchronous task interface. You need to submit a task through the submit interface, then use the Poll interface to obtain the task status and retrieve the operator's processing results. Additionally, the operator supports asynchronous callback capability (Callback). You can set the callback parameter `callback.url` when initiating the operator task. LAS will send an HTTP POST notification to this URL. For guidance on using asynchronous callbacks, see [Asynchronous callback API](https://docs.byteplus.com/docs/Byteplus_LAS/Asynchronous_callback_API).

<span id="c332688b"></span>
## Submit

<span id="231f8e27"></span>
### Interface description

You can submit asynchronous tasks by invoking the video editing enhanced version operator. This supports scene replacement, object replacement, and other video replacement editing operations based on input video and reference images or audio, and uploads the results to the specified TOS directory.

<span id="032a885a"></span>
### Request parameters

```mixin-react
const properties = ({
  "columns": [
{ "title": "Parameters", "dataIndex": "column_0", "key": "column_0", "width": 300 },
{ "title": "Type", "dataIndex": "column_1", "key": "column_1", "width": 150 },
{ "title": "Required", "dataIndex": "column_2", "key": "column_2", "width": 80 },
{ "title": "Example", "dataIndex": "column_3", "key": "column_3", "width": 150 },
{ "title": "Description", "dataIndex": "column_4", "key": "column_4" }
  ],
  "data": [
    {
      "key": "1",
      "column_0": "operator_id",
      "column_1": "string",
"column_2": "Yes",
      "column_3": "las_video_seedance_replace",
"column_4": "Operator ID"
    },
    {
      "key": "2",
      "column_0": "operator_version",
      "column_1": "string",
"column_2": "Yes",
      "column_3": "v1",
"column_4": "Operator version"
    },
    {
      "key": "3",
      "column_0": "data",
      "column_1": "VideoSeedanceReplaceReqParams",
"column_2": "Yes",
      "column_3": "",
"column_4": "Video replacement request parameters",
      "children": [
        {
          "key": "3-1",
          "column_0": "video_url",
          "column_1": "string",
"column_2": "Yes",
          "column_3": "tos://example.com/sample.mp4",
"column_4": < div> Enter the video URL. The video duration must be within &#91; 2,15&#93; seconds, and the short-side resolution must be within &#91; 480,1080&#93; pixels. It is recommended to use videos with a clear subject and relatively stable camera movement. Supports < code> http/https</ code>, < code> tos://bucket/key</ code>. If the LAS asset management feature is enabled and materials are uploaded to the asset library, you can also submit inputs using the LAS asset ID. </div>
        },
        {
          "key": "3-2",
          "column_0": "image_urls",
          "column_1": "array",
"column_2": "Yes",
          "column_3": "[\"tos://example.com/ref1.jpg\"]",
"column_4": < div> Reference image list. Currently, you must provide < code> 1-9</ code> images. It is recommended that the reference images include three-view diagrams and detail close-ups. The perspectives and distances of the reference images should match the original video as closely as possible to improve the success rate of replacement. Supports < code> http/https</ code>, < code> tos://bucket/key</ code>. If the LAS asset management feature is enabled and materials are uploaded to the asset library, you can also submit inputs using the LAS asset ID. </div>
        },
        {
          "key": "3-3",
          "column_0": "output_tos_path",
          "column_1": "string",
"column_2": "Yes",
          "column_3": "tos://bucket/output/",
"column_4": < div> Output directory. The operator will upload the result video and < code> result.json</ code> to this directory. </div>
        },
        {
          "key": "3-4",
          "column_0": "task_type",
          "column_1": "string",
"column_2": "Yes",
          "column_3": "scene_replace",
"column_4": < div> Replacement task type. Currently supports < ul>< li>< code> scene_replace</ code>: Scene replacement. </ li>< li>< code> object_replace</ code>: Object replacement. </ li>< li> < code> person_replace</ code>: Person replacement. Before submitting a person replacement task, you must apply to enable the LAS  feature (allowlist feature, disabled by default), and also set< code> seedance_use_asset_api = true</ code>. </li></ul></div>
        },
        {
          "key": "3-41",
          "column_0": "seedance_model",
          "column_1": "string",
"column_2": "No",
          "column_3": "dreamina-seedance-2-0-260128",
"column_4": < div> Video generation models currently supported < ul>< li>
dreamina-seedance-2-5-260628 and dreamina-seedance-2-0-260128: Billed using Video Editing Enhanced Edition. </li><li>
dreamina-seedance-2-0-fast-260128 and dreamina-seedance-2-0-mini-260615: Billed using Video Editing Basic Edition. </li></ul></div>
        },
        {
          "key": "3-5",
          "column_0": "user_prompt",
          "column_1": "string",
"column_2": "No",
"column_3": "Please help me replace the video background with the style of image 1, keep the person's actions and the product unchanged, and remove the subtitles.",
"column_4": "User natural language editing instruction, used to supplement replacement targets and retention constraints."
        },
        {
          "key": "3-6",
          "column_0": "prompt_rewrite_mode",
          "column_1": "string",
"column_2": "No",
          "column_3": "strict",
"column_4": < div> Prompt rewrite mode. LAS provides you with system prompts for video replacement editing under different task_type values. If you also configure user_prompt, the final video editing will rewrite the prompt according to the rules of prompt_rewrite_mode. < br/> Supports < code> light</ code> and < code> strict</ code> (default) as two possible values. < ul>< li>< code> strict</ code> means the system prompt takes precedence, and the prompt is completely rewritten internally.</ li>< li> < code> light</ code> means the input prompt takes precedence, and the operator only applies minimal constraints internally. </li></ul></div>
        },
        {
          "key": "3-7",
          "column_0": "evaluation_standard",
          "column_1": "string",
"column_2": "No",
          "column_3": "loose",
"column_4": < div> Evaluation standard. Supports < code> strict</ code>, < code> loose</ code>, default < code> loose</ code>. < code> loose</ code> means the evaluation standard is relaxed; logical consistency throughout the video and successful replacement are sufficient. < code> strict</ code> means full compliance with instructions. </div>
        },
        {
          "key": "3-8",
          "column_0": "enable_retry",
          "column_1": "boolean",
"column_2": "No",
          "column_3": "true",
"column_4": < div> Whether to trigger limited retries based on evaluation results. Enabling this may increase time and cost. Default is false. < br/> When a task retry is triggered, each retry submits a new task and is billed separately. < br/> For example, after your task runs, if the evaluation result does not meet the standard and you retry twice, the final cost will be for three video editing tasks. </div>
        },
        {
          "key": "3-9",
          "column_0": "max_retry_times",
          "column_1": "integer",
"column_2": "No",
          "column_3": "2",
"column_4": "Maximum number of retries. Valid range is 0-3, default is 1."
        },
        {
          "key": "3-10",
          "column_0": "audio_url",
          "column_1": "string",
"column_2": "No",
          "column_3": "tos://example.com/audio.mp3",
"column_4": < div> Reference audio URL, supports < code> http/https</ code>, < code> tos://bucket/key</ code>. If the LAS asset management feature is enabled and assets are uploaded to the asset library, you can also submit input using the LAS asset ID. </div>
        },
        {
          "key": "3-11",
          "column_0": "seedance_generate_audio",
          "column_1": "boolean",
"column_2": "No",
          "column_3": "false",
"column_4": "Whether the generated result is required to include audio. Default is false; if audio_url is provided, it is recommended to enable this option."
        },
        {
          "key": "3-12",
          "column_0": "seedance_duration",
          "column_1": "integer",
"column_2": "No",
          "column_3": "4",
"column_4": "Target duration of the output video, in seconds. The current valid range is 4-15."
        },
        {
          "key": "3-13",
          "column_0": "seedance_ratio",
          "column_1": "string",
"column_2": "No",
          "column_3": "16:9",
"column_4": "Output video aspect ratio. Supports 16:9, 9:16, 1:1, 4:3, 3:4, 21:9. If not configured, the default is the same as the original video aspect ratio."
        },
        {
          "key": "3-14",
          "column_0": "seedance_resolution",
          "column_1": "string",
"column_2": "No",
          "column_3": "720p",
"column_4": "Set a unified resolution for the output video. Supports 480p, 720p, and 1080p. If not configured, the default is to automatically process according to the input video (same as the input video)."
        },
        {
          "key": "3-15",
          "column_0": "seedance_camera_fixed",
          "column_1": "boolean",
"column_2": "No",
          "column_3": "false",
"column_4": "Whether to keep the camera angle as fixed as possible. Default is not set."
        },
        {
          "key": "3-16",
          "column_0": "seedance_watermark",
          "column_1": "boolean",
"column_2": "No",
          "column_3": "false",
"column_4": < div> Whether to add a watermark to the generated result. Default is false. < br/> - `false` (default): The generated video does not contain a watermark. < br/> - `true`: The generated video will display an AI-generated watermark in the lower right corner. </div>
        },
        {
          "key": "3-17",
          "column_0": "seedance_seed",
          "column_1": "integer",
"column_2": "No",
          "column_3": "42",
"column_4": "Random seed. Default is 42."
        },
        {
          "key": "3-18",
          "column_0": "seedance_use_asset_api",
          "column_1": "boolean",
"column_2": "No",
          "column_3": "false",
"column_4": < div> Whether to enable the asset library capability; the default is false. < ul>< li> If the video contains real people, you must enable the asset library. If you do not enable the asset library but upload real-person assets and complete the copyright process, video editing tasks containing real people will fail and return an error. </ li>< li> The current asset library feature is an allowlist feature. To enable the asset library, submit a ticket and contact technical support to assist with enabling allowlist access. </ li>< li> After enabling the LAS asset management allowlist feature, you can upload assets to the LAS asset library. When submitting an operator task, set< code> seedance_use_asset_api = true</ code>, and use the LAS asset ID format (follow the format:< code> asset://&lt; asset-id&gt;</ code>) to input audio, video, or images to the operator. </li></ul></div>
        }
      ]
    },
    {
      "key": "4",
      "column_0": "callback",
      "column_1": "Callback",
"column_2": "No",
      "column_3": "",
"column_4": "Task status callback configuration. After configuring callback.url, a POST request will be sent to this address when the task status changes. If not configured, you can query the task status and result using Poll.",
      "children": [
        {
          "key": "4-1",
          "column_0": "url",
          "column_1": "string",
"column_2": "Yes",
          "column_3": " `https://example.com/callback` ",
"column_4": "Callback address. By default, only HTTPS addresses accessible from the public network are supported."
        }
      ]
    },
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```


<span id="af0191d4"></span>
### Response parameters

```mixin-react
const properties = ({
  "columns": [
{ "title": "Parameter", "dataIndex": "column_0", "key": "column_0", "width": 300 },
{ "title": "Type", "dataIndex": "column_1", "key": "column_1", "width": 150 },
{ "title": "Example value", "dataIndex": "column_2", "key": "column_2", "width": 150 },
{ "title": "Description", "dataIndex": "column_3", "key": "column_3" }
  ],
  "data": [
    {
      "key": "1",
      "column_0": "metadata",
      "column_1": "metadata",
      "column_2": "",
"column_3": "Request metadata",
      "children": [
        {
          "key": "1-1",
          "column_0": "task_id",
          "column_1": "string",
          "column_2": "task-xxx",
"column_3": "Task ID in asynchronous mode, used for job status queries."
        },
        {
          "key": "1-2",
          "column_0": "task_status",
          "column_1": "string",
          "column_2": "PENDING",
"column_3": < div> Task status in asynchronous mode. < br/> - PENDING, request received< br/> - RUNNING, running< br/> - COMPLETED, completed< br/> - FAILED, failed< br/> - TIMEOUT, timed out</ div>
        },
        {
          "key": "1-3",
          "column_0": "business_code",
          "column_1": "string",
          "column_2": "0",
"column_3": "Business code."
        },
        {
          "key": "1-4",
          "column_0": "error_msg",
          "column_1": "string",
          "column_2": "",
"column_3": "If there is an exception, detailed error information will be returned."
        }
      ]
    }
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```


<span id="f1b9d802"></span>
### Request example

```Bash
# Please set OUTPUT_TOS_PATH to a tos path writable by this account
export OUTPUT_TOS_PATH="tos://path/to/seedance_replace_results"

curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_video_seedance_replace",
    "operator_version": "v1",
    "data": {
        "video_url": "https://${LAS_TOS_BUCKET}.${TOS_ENDPOINT}/operator_cards_serving/public/${LAS_ENVIRONMENT}/las_video_seedance_replace/v1/sample_input.mp4",
        "image_urls": [
            "https://${LAS_TOS_BUCKET}.${TOS_ENDPOINT}/operator_cards_serving/public/${LAS_ENVIRONMENT}/las_video_seedance_replace/v1/sample_reference.jpg"
        ],
        "output_tos_path": "$OUTPUT_TOS_PATH",
        "user_prompt": "请帮我把@视频1的背景替换成@图片1的风格，保持人物动作和商品一致性，除背景外不做任何更改，不要字幕。",
        "task_type": "scene_replace",
        "enable_retry": true,
        "max_retry_times": 2
    }
}'
```


<span id="379af451"></span>
### Response example

```JSON
{
  "metadata": {
    "task_id": "task-20260427143000-abc123",
    "task_status": "PENDING",
    "business_code": "0",
    "error_msg": ""
  }
}
```


<span id="4d80331d"></span>
### Error code


|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Url.Invalid |The url is invalid. |The input video, reference image, or audio link is invalid. |
|400 |Video.Invalid |The video file is invalid. |The video file is invalid or cannot be parsed. |
|400 |Video.DownloadFailed |Video download failed. |Video download failed. |
|400 |Video.FormatUnsupported |Video format not supported. |Video format not supported. |
|400 |Video.DurationTooShort |Video duration is too short. |Video duration is below the minimum limit. |
|400 |Video.DurationExceeded |Video duration exceeds maximum limit. |The video duration exceeds the maximum limit. |
|400 |Video.FileTooLarge |Video file size exceeds maximum limit. |The video file is too large. |
|400 |Parameter.Invalid |The parameter is invalid. |The parameter is invalid. |
|400 |Video.Timeout |Video processing timeout. |Video processing timed out. |
|400 |Video.UploadFailed |Video upload failed. |Failed to upload the resulting video. |
|400 |Tos.AccessFailed |TOS access failed. |TOS access failed. |
|401 |Authorization.Missing |Missing Authorization. |Authorization is missing. |
|401 |ApiKey.InValid |The api key is invalid. |The API is invalid. |
|500 |Internal.ServerError |Internal server error. |Internal server error, such as failure in generation, evaluation, or result assembly. |


<span id="d71131e0"></span>
## Poll

<span id="d9b28f95"></span>
### Interface description

Query the execution status and result of the video replacement task.

<span id="42da0494"></span>
### Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|operator_id |string |Yes |las_video_seedance_replace |Operator ID |
|operator_version |string |Yes |v1 |Operator version |
|task_id |string |Yes |task\-xxx |Task ID |


<span id="0c8f1908"></span>
### Response parameters

```mixin-react
const properties = ({
  "columns": [
{ "title": "Parameters", "dataIndex": "column_0", "key": "column_0", "width": 300 },
{ "title": "Type", "dataIndex": "column_1", "key": "column_1", "width": 150 },
{ "title": "Example", "dataIndex": "column_2", "key": "column_2", "width": 150 },
{ "title": "Description", "dataIndex": "column_3", "key": "column_3" }
  ],
  "data": [
    {
      "key": "1",
      "column_0": "metadata",
      "column_1": "metadata",
      "column_2": "",
"column_3": "Request metadata",
      "children": [
{ "key": "1-1", "column_0": "task_id", "column_1": "string", "column_2": "task-xxx", "column_3": "Task ID in asynchronous mode." },
{ "key": "1-2", "column_0": "task_status", "column_1": "string", "column_2": "COMPLETED", "column_3": <div>Task status in asynchronous mode.<br/> - PENDING, task submitted and queued<br/> - RUNNING, running<br/> - COMPLETED, completed<br/> - FAILED, failed<br/> - TIMEOUT, timed out</div> },
        {
          "key": "submit_time_1",
          "children": [],
          "column_0": "submit_time",
          "column_1": "string",
          "column_2": "2026-07-21T16:04:06+08:00",
"column_3": "Task submission time, in ISO 8601 timestamp format."
        },
        {
          "key": "end_time_1",
          "children": [],
          "column_0": "end_time",
          "column_1": "string",
          "column_2": "2026-07-21T16:04:06+08:00",
"column_3": "Task end time, in ISO 8601 timestamp format."
        },
{ "key": "1-3", "column_0": "business_code", "column_1": "string", "column_2": "0", "column_3": "Business code." },
{ "key": "1-4", "column_0": "error_msg", "column_1": "string", "column_2": "", "column_3": "If there is an exception, detailed error information will be returned." }
      ]
    },
    {
      "key": "2",
      "column_0": "data",
      "column_1": "VideoSeedanceReplaceResponse",
      "column_2": "",
"column_3": "Returned data",
      "children": [
        {
"key": "2-1",
"column_0": "output_video_tos_url",
"column_1": "string",
"column_2": "tos://bucket/output/run_id/generated/attempt_01.mp4",
"column_3": <div>TOS address of the output video; returned only if <code>output_tos_path</code> is provided at submission and written successfully. </div> },
        {
"key": "2-2",
 "column_0": "output_video_url",
"column_1": "string",
"column_2": "https://example.com/generated/attempt_01.mp4",
"column_3": "Pre-signed download URL for the output video, valid for 24 hours." },
        {
"key": "2-3",
"column_0": "selected_attempt_no",
"column_1": "integer",
"column_2": "1",
"column_3": "The attempt number of the final selected generation. The video editing task numbering starts from 0 and increases sequentially when task retries are triggered. The task number here corresponds to the pre-signed URL of the returned video." },
        {
"key": "2-4",
"column_0": "attempt_count",
"column_1": "integer",
"column_2": "1",
"column_3": "Actual number of generations." },
        {
"key": "2-5",
"column_0": "output_result_json_tos_url",
"column_1": "string",
"column_2": "tos://bucket/output/run_id/result.json",
"column_3": <div>TOS address of <code>result.json</code>; returned only if <code>output_tos_path</code> is provided at submission and written successfully. </div> },
        {
"key": "2-6",
"column_0": "output_result_json_url",
"column_1": "string",
"column_2": "https://example.com/result.json",
"column_3": <div>Pre-signed download URL for <code>result.json</code>, valid for 24 hours. </div> }
      ]
    }
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```


<span id="a9fe3908"></span>
### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_video_seedance_replace",
    "operator_version": "v1",
    "task_id": "task-20260427143000-abc123"
}'
```


<span id="2d974423"></span>
### Response example

```JSON
{
    "metadata": {
        "task_id": "task-20260427143000-abc123",
        "task_status": "COMPLETED",
        "submit_time": "2026-07-21T16:04:06+08:00",
        "end_time": "2026-07-21T16:04:06+08:00",
        "business_code": "0",
        "error_msg": ""
    },
    "data": {
        "output_video_tos_url": "tos://path/to/seedance_replace_results/run_id/generated/attempt_01.mp4",
        "output_video_url": "https://path/to/seedance_replace_results/run_id/generated/attempt_01.mp4",
        "selected_attempt_no": 1,
        "attempt_count": 1,
        "output_result_json_tos_url": "tos://path/to/seedance_replace_results/run_id/result.json",
        "output_result_json_url": "https://path/to/seedance_replace_results/run_id/result.json"
    }
}
```


<span id="f58f5e7a"></span>
### Error code


|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Url.Invalid |The url is invalid. |The input video, reference image, or audio link is invalid. |
|400 |Video.Invalid |The video file is invalid. |The video file is invalid or cannot be parsed. |
|400 |Video.DownloadFailed |Video download failed. |Video download failed. |
|400 |Video.FormatUnsupported |Video format not supported. |Video format not supported. |
|400 |Video.DurationTooShort |Video duration is too short. |Video duration is below the minimum limit. |
|400 |Video.DurationExceeded |Video duration exceeds maximum limit. |The video duration exceeds the maximum limit. |
|400 |Video.FileTooLarge |Video file size exceeds maximum limit. |The video file is too large. |
|400 |Parameter.Invalid |The parameter is invalid. |The parameter is invalid. |
|400 |Video.Timeout |Video processing timeout. |Video processing timed out. |
|400 |Video.UploadFailed |Video upload failed. |Failed to upload the resulting video. |
|400 |Tos.AccessFailed |TOS access failed. |TOS access failed. |
|401 |Authorization.Missing |Missing Authorization. |Authorization is missing. |
|401 |ApiKey.InValid |The api key is invalid. |The API is invalid. |
|500 |Internal.ServerError |Internal server error. |Internal service error. |
