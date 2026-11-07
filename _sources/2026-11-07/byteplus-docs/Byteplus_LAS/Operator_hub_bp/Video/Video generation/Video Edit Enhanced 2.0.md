---
title: "Video Edit Enhanced 2.0"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Enhanced_video_editing_2"
---

The Video Edit Enhance 2.0 operator (las_video_edit_enhance) is designed for video production and post\-editing scenarios. Provide a source video, a clear editing request, and the necessary reference images to enhance a video, change local content, replace a person's identity or appearance, replace an object or background, or apply a consistent style to the entire video. The source video is used to preserve existing motion, camera work, composition, and timing, while reference images describe the target result. Content outside the requested edit is preserved as much as possible.

<span id="923378c3"></span>
# Operator introduction

> Operator ID: las_video_edit_enhance


<span id="8fa3a53d"></span>
## Core capabilities


* **Template\-based routing**: The business only specifies the editing target, and the server\-side template is responsible for selecting the VLM, keyframe redraw, structural video, and Seedance prompt assembly workflow.

* **General keyframe editing**: VLM interprets the video and user intent, selects keyframes, and uses Seedream to edit based on the source frame canvas.

* **Full character replacement**: Uses the original video as the basis for actions and timeline, locking the final character appearance with the target character image and redrawn keyframes.

* **Style transfer**: By default, uses pure depth structural video to preserve spatial layout, actions, and camera movement, reducing interference from the original video's color, material, subtitles, and cinematographic style.

* **Multi\-subject mapping**: Multiple source subjects in `user_prompt` can be bound to different target images in `image_urls` respectively.

* **Controllable fallback**: When `allow_fallback=true`, preprocessing failures can fall back to direct generation equivalent to `basic`; for strong semantic editing, it is recommended to set it to `false` to avoid returning incomplete editing results.


<span id="02e14931"></span>
## Supported preset templates

The supported template types and applicable scenarios are as follows.


|`template.id` |Applicable scenarios |Reference image requirements |Unsuitable scenarios |
|---|---|---|---|
|`basic` |To skip VLM, frame extraction, and redraw, and directly request Seedance when complete prompts and reference materials are already prepared. |Optional |Editing or replacing multiple people or objects |
|`general` |General keyframe editing, such as local removal, movement, attribute modification, or hybrid editing not yet covered by dedicated templates. |At least 1 image |Editing or replacing multiple people or objects |
|`replace/person_replace` |Fully replace one or more characters, including the target character's face, hairstyle, body shape, clothing, and accessories, while retaining the original video's actions and positions. For multi\-character scenarios, it is recommended to use the seedance\-2\-5 model. |At least one target person image is required. |Scenarios for simultaneously replacing people and items |
|`replace/subject_replace` |Replace objects, props, partial backgrounds, full backgrounds, or the overall content of people and environments in the video |At least one target reference image |Replace only people; when replacing only people, use replace/person_replace |
|`style_transfer/general` |Convert the entire video to a unified visual style such as Japanese manga, Korean manga, Chinese manga, 3D animation, or photorealism, while maintaining content and sequence. |Optional; can be provided if there is a style reference image. |Replace only a specific person or object without changing the overall style of the video |


Template boundaries:


* To replace only characters, use `replace/person_replace`.

* Use `style_transfer/general` only to change global visual media and style; do not use style transfer templates when editing only local subjects.

* `general` is the general fallback template. When a dedicated template can more clearly constrain person identity, replacement scope, and video structure, the dedicated template should be preferred.


<span id="40867639"></span>
## Effect showcase


---



<div style="text-align: center">
<strong>[Film and television series scenarios]</strong></div>



* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c583b325a1d4b35afc5de29230b0598~tplv-goo7wpa0wc-image.image" controls></video>


* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d4e46096f6b4f46a0027ff9c0a3ce81~tplv-goo7wpa0wc-image.image" controls></video>


* Reference image

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1e8582566964ac6a8e9a3d63641ea1c~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cde347e487194f8c861f40f32bcfbfdb~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1046133b1f9449e29f4779eb86cc75c5~tplv-goo7wpa0wc-image.image) </span>

* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ab882b45f244897ad24c98548614785~tplv-goo7wpa0wc-image.image" controls></video>


* Reference image

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a928ead9afa9414ea0619625244194f6~tplv-goo7wpa0wc-image.image) </span>

* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef183bd524d24a37bb426e8b5e909f20~tplv-goo7wpa0wc-image.image" controls></video>


* Reference image

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61e9e146ddbf44b4b1200e0f291d6ba8~tplv-goo7wpa0wc-image.image) </span>



---



<div style="text-align: center">
<strong>[Marketing video scenarios]</strong></div>



* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa15cf687bf6419a8b0ec84437dfc0ce~tplv-goo7wpa0wc-image.image" controls></video>


* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49c6e72387134981ad1ea05e86c3ff9c~tplv-goo7wpa0wc-image.image" controls></video>


* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be32304724ec4cd386d3a2d217650073~tplv-goo7wpa0wc-image.image" controls></video>


* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b6414b4ee604517a347586d4ea39976~tplv-goo7wpa0wc-image.image" controls></video>




---



<span id="359eb6c4"></span>
## Supported regions


* Asia Pacific(Johor)：ap\-southeast\-1


<span id="3d6da631"></span>
## Operator performance


|**Item** |**Details** |
|---|---|
|Submit RPM |600 |
|Poll RPM |600 |
|Concurrency |10 |
|Processing time |Depends on video duration, reference count, selected template, model, system load, and task queue. |


<span id="2a8b450e"></span>
# Operator performance


|Subcategories |Performance impact description |
|---|---|
|Maximum RPM |600 |
|Maximum concurrency |10 |
|Processing time |* Total processing time depends on video duration, number of keyframes, number of reference images, template, and downstream model queue status. `basic` does not perform preprocessing and usually has the shortest processing time. |


<span id="c3e285d1"></span>
# Input and output requirements

<span id="fbe9eae0"></span>
## Input requirements


|Subdivision |Detailed description |
|---|---|
|Supported input data modalities |* Video<br><br>* Image<br><br>* Audio<br><br>* Text |
|Input path requirements |Provide input data to the operator via request parameters `video_url`, `image_urls`, and `audio_url`. Currently, public URLs, TOS paths, and LAS asset IDs are supported.<br><br><br>* **Public URL**: A video URL accessible via the public internet, in the format `http/https`.<br><br>* **TOS path**: After uploading the data to be processed to a TOS Bucket under the same primary account and region as the current LAS service, you can provide the TOS path in the format `tos://bucket_name/demo`.<br><br>* **LAS asset ID**: The ID used for generating real and virtual avatars in videos, following the format: `asset://<asset-id>`.<br><br>   * When using the LAS asset ID method, you must first apply to enable the LAS asset managementfeature (allowlist feature, disabled by default), and set `seedance_use_asset_api = true` when submitting the task.<br><br>   * When submitting various tasks, if the input material involves real audio/video or images, you must first upload the material to the LAS asset library and input the corresponding material to the model via the LAS asset ID method; otherwise, the task may be blocked.<br><br>   * After enabling the feature and uploading materials, you can view the list of asset groups in the [LAS console](https://console.volcengine.com/las/region:las+cn-beijing/next/home) under asset management \> Virtual Portrait Asset. On the asset group details page, you can obtain the specific asset ID (`asset-id`), which can be concatenated in the above format as the operator's input. |


<span id="85832628"></span>
## Output requirements


|Subdivision |Detailed description |
|---|---|
|Output data modality |* Video |
|Output format: Video |* Aspect ratio: Original video ratio (default), 16:9, 9:16, 1:1, 4:3, 3:4, 21:9.<br><br>* Resolution: Supports setting to 480p, 720p, 1080p, 4k (4k is supported only in seedance 2.0). |
|Output path: TOS |Specify the storage path for the operator's output results via the request parameter `output_tos_path`. Currently, only TOS paths are supported.<br><br><br>* TOS path: A directory in a TOS Bucket under the same primary account and region as the LAS service, with write permissions. |


<span id="c5910344"></span>
# Billing informationBilling information


* Billing standards

   
   |Breakdown |Billing standard description |
   |---|---|
   |Billing items |Includes two billing items: **`video preprocessing`** and **`video editing`**. Both billing items are charged based on the usage calculated from the duration of the input and output videos.<br><br><br>* **`Video preprocessing`** billing:<br><br>   * This depends on the type of video editing task template selected when submitting the task. When submitting an operator task, set the processing template for the task using the `template` request parameter. The unit price for video preprocessing billing varies depending on the task template.<br><br>* **`Video editing`** billing:<br><br>   * This depends on the type of processing model selected when submitting the task. When submitting an operator task, set the processing model for the task using the `model` request parameter. The unit price for video editing billing varies depending on the model.<br><br><br>The final total cost is the sum of the two billing items: **`video preprocessing`** and **`video editing`**. |
   |Billing type |Pay\-as\-you\-go billing, unit: USD/second. Charges are settled hourly based on actual usage. Billing precision: rounded. |
   |Unit price |* **`Video preprocessing`** unit price: 0.025 USD/second<br><br>* **`Video editing`** unit price details: This depends on the model type and video resolution you select. See the table below for details. |
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The cost for each <strong><code>video editing</code></strong> task: In addition to the unit price, it also depends on the duration of the input/output videos and the resolution of the input/output videos.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only tasks that successfully generate videos will incur charges; scenarios where video generation fails due to review or other operational reasons are not billed.   </div>
   

* Billing details

   Billing estimate: `Total cost ≈ Video preprocessing cost + Video editing cost = Video preprocessing unit price * (input video duration + output video duration) + Video editing unit price * (input video duration + output video duration) * conversion factor`

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The above formula is for cost estimation only; actual billing is based on the billed usage.   </div>
   

   * **`Video preprocessing`** unit price: 0.025 USD/second

   * **`Video editing`** unit price details: This depends on the model type and video resolution you select. Details are as follows.

      
      |Version breakdown |Unit price |Model type |Duration conversion coefficient: depends on video resolution |
      |---|---|---|---|
      |Basic version |0.242 USD/second |seedance 2.0\-fast |* 480P：0.2770<br><br>* 720P：0.5988 |
      |||seedance 2.0\-mini |* 480P：0.1769<br><br>* 720P：0.3812 |
      |Enhanced version |0.303 USD/second |seedance 2.0 |* 480P：0.2830<br><br>* 720P：0.6098<br><br>* 1080P：1.5251<br><br>* 4k：3.1348 |
      |||seedance 2.5 |* 480P：0.406<br><br>* 720P：0.9125 |
      

* Billing example

   * Example scenario: Use the `replace/person_replace` task template and the Seedance 2.0 model to perform video face replacement editing. The input video duration is 10 seconds, with a resolution of 1080p.

   * Cost details:

      `Total cost ≈ Video preprocessing cost + Video editing cost = 0.025 USD/second * (10 seconds + 10 seconds) + 0.303 USD/second * (10 seconds + 10 seconds) * 1.5251 ≈ 9.7421 USD`


<span id="4bda6137"></span>
# Caution and prerequisites


|Details |Caution and prerequisites |
|---|---|
|Costs |Before calling an operator, you need to understand the model invocation costs associated with using the operator. For details, see [Large model billing](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |


<span id="cff46ad3"></span>
# Rest API invocation

<span id="8ec1ed23"></span>
## API invocation instructions


* The API for this operator is an asynchronous task interface. You need to submit a task via the submit interface to obtain the task_id, then use the Poll interface to check the status of the corresponding task (task_id) and retrieve the operator processing result. Additionally, this operator supports asynchronous callback capability (Callback). You can set the callback parameter `callback.url` when initiating an operator task. LAS will send an HTTP POST notification to this URL. For guidance on using asynchronous callbacks, see [Asynchronous callback API](https://docs.byteplus.com/docs/Byteplus_LAS/Asynchronous_callback_API).

* After the task is submitted, the task_id is valid for 3 days. After 3 days, you will not be able to obtain the operator processing result using this task_id.


<span id="d287a11c"></span>
## Submit

<span id="c026c377"></span>
### Interface description

Submit an asynchronous task to Video Edit Enhance 2.0 (las_video_edit_enhance). Select template.id according to the business goal, and use user_prompt to describe what should change, what should remain unchanged, and what each reference image represents.

<span id="b98ebb5b"></span>
### Request parameters

```mixin-react
const properties = ({
  "columns": [
    {
      "title": "Parameter",
      "dataIndex": "column_0",
      "key": "column_0",
      "width": 300
    },
    {
      "title": "Type",
      "dataIndex": "column_1",
      "key": "column_1",
      "width": 150
    },
    {
      "title": "Required",
      "dataIndex": "column_2",
      "key": "column_2",
      "width": 100
    },
    {
      "title": "Example value",
      "dataIndex": "column_3",
      "key": "column_3",
      "width": 180
    },
    {
      "title": "Description",
      "dataIndex": "column_4",
      "key": "column_4"
    }
  ],
  "data": [
    {
      "key": "1",
      "column_0": "operator_id",
      "column_1": "string",
      "column_2": "Yes",
      "column_3": "las_video_edit_enhance",
      "column_4": "Fixed operator ID"
    },
    {
      "key": "2",
      "column_0": "operator_version",
      "column_1": "string",
      "column_2": "Yes",
      "column_3": "v1",
      "column_4": "Fixed operator version"
    },
    {
      "key": "3",
      "column_0": "data",
      "column_1": "VideoEditEnhanceReqParams",
      "column_2": "Yes",
      "column_3": "-",
      "column_4": "Video Edit Enhance request parameters",
      "children": [
        {
          "key": "3-1",
          "column_0": "video_url",
          "column_1": "string",
          "column_2": "Yes",
          "column_3": "-",
          "column_4": <div>Source video. Supports http/https, tos://bucket/key, asset://&lt;id&gt;, or a bare asset ID. A bare asset ID must first be uploaded to the LAS Asset Library.</div>
        },
        {
          "key": "3-2",
          "column_0": "template",
          "column_1": "object",
          "column_2": "No",
          "column_3": "{\"id\":\"basic\"}",
          "column_4": "Recommended workflow selector; mode is supported for backward compatibility",
          "children": [
            {
              "key": "3-2-1",
              "column_0": "`id`",
              "column_1": "string",
              "column_2": "Yes",
              "column_3": "",
              "column_4": "Template ID. Must be one of the values in the tempalte table."
            },
            {
              "key": "3-2-2",
              "column_0": "`paras`",
              "column_1": "object",
              "column_2": "No",
              "column_3": "",
              "column_4": <div>Template parameters. Defaults to <code>&#123;&#125;</code>. Parameters not declared by the selected template are not allowed.</div>
            }
          ]
        },
        {
          "key": "3-3",
          "column_0": "user_prompt",
          "column_1": "string",
          "column_2": "Yes",
          "column_3": "-",
          "column_4": "Describe the business goal in natural language, including what to replace or change, the desired result, and what must remain unchanged"
        },
        {
          "key": "3-4",
          "column_0": "image_urls",
          "column_1": "array",
          "column_2": "Template-dependent",
          "column_3": "[]",
          "column_4": <div>Target reference images for a person, object, background, or style. Supports http/https, tos://, and asset://&lt;id&gt;</div>
        },
        {
          "key": "3-5",
          "column_0": "audio_urls",
          "column_1": "array",
          "column_2": "No",
          "column_3": "[]",
          "column_4": "Audio reference list using the same formats as images"
        },
        {
          "key": "3-6",
          "column_0": "allow_fallback",
          "column_1": "boolean",
          "column_2": "No",
          "column_3": "false",
          "column_4": "Whether a failed complex edit may return a basic pass-through result; keep it false for strongly semantic person or subject replacement"
        },
        {
          "key": "3-7",
          "column_0": "model",
          "column_1": "string",
          "column_2": "No",
          "column_3": "dreamina-seedance-2-0-260128",
          "column_4": "Seedance model name. When omitted, the server-configured default model is used. Allowed values are dreamina-seedance-2-0-mini-260615, dreamina-seedance-2-0-fast-260128, dreamina-seedance-2-0-260128, and dreamina-seedance-2-5-260628."
        },
        {
          "key": "3-8",
          "column_0": "duration",
          "column_1": "integer",
          "column_2": "No",
          "column_3": "null",
          "column_4": "Must be greater than or equal to -1; Seedance 2.5 only accepts -1"
        },
        {
          "key": "3-9",
          "column_0": "resolution",
          "column_1": "string",
          "column_2": "No",
          "column_3": "null",
          "column_4": "All models supports 480p, 720p; Only Seedance 2.0 supports 1080p"
        },
        {
          "key": "3-10",
          "column_0": "ratio",
          "column_1": "string",
          "column_2": "No",
          "column_3": "adaptive",
          "column_4": "Supports 16:9, 4:3, 1:1, 3:4, 9:16, 21:9, and adaptive"
        },
        {
          "key": "3-11",
          "column_0": "generate_audio",
          "column_1": "boolean",
          "column_2": "No",
          "column_3": "true",
          "column_4": "Whether to generate synchronized audio"
        },
        {
          "key": "3-12",
          "column_0": "watermark",
          "column_1": "boolean",
          "column_2": "No",
          "column_3": "false",
          "column_4": "Whether to display an AI-generated watermark"
        },
        {
          "key": "3-13",
          "column_0": "return_last_frame",
          "column_1": "boolean",
          "column_2": "No",
          "column_3": "false",
          "column_4": "Whether to return the generated video's last frame"
        },
        {
          "key": "3-14",
          "column_0": "priority",
          "column_1": "integer",
          "column_2": "No",
          "column_3": "0",
          "column_4": "Seedance task priority"
        },
        {
          "key": "3-15",
          "column_0": "execution_expires_after",
          "column_1": "integer",
          "column_2": "No",
          "column_3": "172800",
          "column_4": "Validity period in seconds, from 3600 to 259200"
        },
        {
          "key": "3-16",
          "column_0": "callback_url",
          "column_1": "string",
          "column_2": "No",
          "column_3": "null",
          "column_4": "Public HTTPS callback URL"
        },
        {
          "key": "3-17",
          "column_0": "safety_identifier",
          "column_1": "string",
          "column_2": "No",
          "column_3": "null",
          "column_4": "End-user identifier for safety auditing"
        },
        {
          "key": "3-18",
          "column_0": "moderation_options",
          "column_1": "object",
          "column_2": "No",
          "column_3": "null",
          "column_4": "Moderation IP configuration"
        },
        {
          "key": "3-19",
          "column_0": "output_format",
          "column_1": "string",
          "column_2": "No",
          "column_3": "mp4",
          "column_4": "Effective only for Seedance 2.5"
        },
        {
          "key": "3-20",
          "column_0": "omni_reference_task_type",
          "column_1": "string",
          "column_2": "No",
          "column_3": "auto",
          "column_4": "Effective only for Seedance 2.5"
        },
        {
          "key": "3-21",
          "column_0": "use_asset_api",
          "column_1": "boolean",
          "column_2": "No",
          "column_3": "false",
          "column_4": "Whether to convert media into Seedance Asset references"
        },
        {
          "key": "3-22",
          "column_0": "asset_group_id",
          "column_1": "string",
          "column_2": "No",
          "column_3": "null",
          "column_4": "Asset group ID; the server looks up or creates one when omitted"
        }
      ]
    }
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```


<span id="852ea0d9"></span>
### Response parameters

```mixin-react
const properties = ({
  "columns": [
    {
      "title": "Parameter",
      "dataIndex": "column_0",
      "key": "column_0",
      "width": 300
    },
    {
      "title": "Type",
      "dataIndex": "column_1",
      "key": "column_1",
      "width": 150
    },
    {
      "title": "Example value",
      "dataIndex": "column_3",
      "key": "column_3",
      "width": 180
    },
    {
      "title": "Description",
      "dataIndex": "column_4",
      "key": "column_4"
    }
  ],
  "data": [
    {
      "key": "1",
      "column_0": "metadata",
      "column_1": "metadata",
      "column_3": "-",
      "column_4": "Asynchronous task metadata",
      "children": [
        {
          "key": "1-1",
          "column_0": "task_id",
          "column_1": "string",
          "column_3": "task-xxx",
          "column_4": "Task ID for Poll queries"
        },
        {
          "key": "1-2",
          "column_0": "task_status",
          "column_1": "string",
          "column_3": "PENDING",
          "column_4": "PENDING, RUNNING, COMPLETED, FAILED, or TIMEOUT"
        },
        {
          "key": "1-3",
          "column_0": "business_code",
          "column_1": "string",
          "column_3": "0",
          "column_4": "Business code"
        },
        {
          "key": "1-4",
          "column_0": "error_msg",
          "column_1": "string",
          "column_3": "-",
          "column_4": "Failure reason"
        }
      ]
    }
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```


<span id="c7000837"></span>
### Example

<span id="ee1b63ef"></span>
#### Request example

basic: Direct generation

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
  "operator_id": "las_video_edit_enhance",
  "operator_version": "v1",
  "data": {
    "video_url": "tos://bucket/videos/input.mp4",
    "template": {"id": "basic"},
    "user_prompt": "Keep the camera and motion unchanged while improving image clarity and color depth",
    "image_urls": []
  }
}'
```


general: General local editing

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
  "operator_id": "las_video_edit_enhance",
  "operator_version": "v1",
  "data": {
    "video_url": "tos://bucket/videos/input.mp4",
    "template": {"id": "general"},
    "user_prompt": "Replace the cup on the table with the product in reference image 1, while preserving all other people, objects, and the background",
    "image_urls": ["https://example.com/product.png"]
  }
}'
```


replace/person_replace: Complete person replacement

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
  "operator_id": "las_video_edit_enhance",
  "operator_version": "v1",
  "data": {
    "video_url": "tos://bucket/videos/input.mp4",
    "template": {"id": "replace/person_replace"},
    "user_prompt": "Fully replace the woman on the left with the person in reference image 1 and the man on the right with the person in reference image 2. Use the target people's faces, hairstyles, body types, clothing, and accessories while preserving the source video's motion, positions, interactions, camera work, and background",
    "image_urls": ["https://example.com/woman.png", "https://example.com/man.png"],
    "use_asset_api": true
  }
}'
```


style_transfer/general: Global style transfer

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
  "operator_id": "las_video_edit_enhance",
  "operator_version": "v1",
  "data": {
    "video_url": "tos://bucket/videos/input.mp4",
    "template": {"id": "style_transfer/general", "paras": {"style_template": "2d_japanese"}},
    "user_prompt": "Convert the entire video into polished Japanese 2D animation while preserving character identities, character count, motion, lip movements, camera work, composition, and timeline. Do not add subtitles or watermarks",
    "image_urls": ["https://example.com/man.png"],
    "use_asset_api": true
  }
}'
```


<span id="21ba768d"></span>
#### **Response example**

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


<span id="00c65a31"></span>
### Error codes


|**HttpStatusCode** |**Error code** |**Error message** |**Description** |
|---|---|---|---|
|400 |Url.Invalid |The URL is invalid. |Invalid video, image, or audio reference |
|400 |Parameter.Invalid |The parameter is invalid. |Invalid template, parameter, reference image, or generation parameter |
|400 |Model.InvalidName |The model name is invalid. |Invalid Seedance model name |
|400 |Video.DownloadFailed |Video download failed. |Video download failed |
|400 |Tos.AccessFailed |TOS access failed. |TOS access failed |
|401 |Authorization.Missing |Missing Authorization. |Missing authorization |
|401 |ApiKey.Invalid |The API key is invalid. |Invalid API key |
|500 |Internal.ServerError |Internal server error. |Video editing or result generation failed |


<span id="8b595531"></span>
## Poll

<span id="78356bfd"></span>
### Interface description

Query the execution status and result of a Video Edit Enhance task.

<span id="3e4f5bb9"></span>
### Request parameters


|**Name** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|operator_id |string |Yes |las_video_edit_enhance |Operator ID. |
|operator_version |string |Yes |v1 |Operator version. |
|task_id |string |Yes |task\-xxx |Task ID returned by Submit. |


<span id="8a709911"></span>
### Response parameters

```mixin-react
const properties = ({
  "columns": [
    {
      "title": "Parameter",
      "dataIndex": "column_0",
      "key": "column_0",
      "width": 300
    },
    {
      "title": "Type",
      "dataIndex": "column_1",
      "key": "column_1",
      "width": 150
    },
    {
      "title": "Example value",
      "dataIndex": "column_3",
      "key": "column_3",
      "width": 180
    },
    {
      "title": "Description",
      "dataIndex": "column_4",
      "key": "column_4"
    }
  ],
  "data": [
    {
      "key": "1",
      "column_0": "metadata",
      "column_1": "metadata",
      "column_3": "",
      "column_4": "Request metadata.",
      "children": [
        {
          "key": "1-1",
          "column_0": "task_id",
          "column_1": "string",
          "column_3": "task-xxx",
          "column_4": "Asynchronous task ID."
        },
        {
          "key": "1-2",
          "column_0": "task_status",
          "column_1": "string",
          "column_3": "COMPLETED",
          "column_4": <div>Asynchronous task status.<br/>- PENDING: queued after submission<br/>- RUNNING: running<br/>- COMPLETED: completed<br/>- FAILED: failed<br/>- TIMEOUT: timed out</div>
        },
        {
          "key": "1-3",
          "column_0": "business_code",
          "column_1": "string",
          "column_3": "0",
          "column_4": "Business code."
        },
        {
          "key": "1-4",
          "column_0": "operator_id",
          "column_1": "string",
          "column_3": "las_video_edit_enhance",
          "column_4": "Operator ID."
        },
        {
          "key": "1-5",
          "column_0": "operator_version",
          "column_1": "string",
          "column_3": "v1",
          "column_4": "Operator version."
        },
        {
          "key": "1-6",
          "column_0": "error_msg",
          "column_1": "string",
          "column_3": "",
          "column_4": "Detailed error information returned when the task fails."
        }
      ]
    },
    {
      "key": "2",
      "column_0": "data",
      "column_1": "VideoEditEnhanceResponse",
      "column_3": "",
      "column_4": "Video editing task result.",
      "children": [
        {
          "key": "2-1",
          "column_0": "id",
          "column_1": "string",
          "column_3": "cgt-xxxxxxxx",
          "column_4": "Video generation task ID."
        },
        {
          "key": "2-2",
          "column_0": "model",
          "column_1": "string",
          "column_3": "dreamina-seedance-2-0-260128",
          "column_4": "Model name and version used by the task."
        },
        {
          "key": "2-3",
          "column_0": "status",
          "column_1": "string",
          "column_3": "succeeded",
          "column_4": "Video generation status: queued, running, succeeded, failed, or expired."
        },
        {
          "key": "2-4",
          "column_0": "resolution",
          "column_1": "string",
          "column_3": "1080p",
          "column_4": "Generated video resolution."
        },
        {
          "key": "2-5",
          "column_0": "ratio",
          "column_1": "string",
          "column_3": "adaptive",
          "column_4": "Actual aspect ratio of the generated video. When adaptive is requested, this field contains the final ratio."
        },
        {
          "key": "2-6",
          "column_0": "duration",
          "column_1": "integer",
          "column_3": "5",
          "column_4": "Actual generated video duration in seconds. When duration=-1 is requested, this field contains the duration selected by the model."
        },
        {
          "key": "2-7",
          "column_0": "framespersecond",
          "column_1": "integer",
          "column_3": "24",
          "column_4": "Generated video frame rate."
        },
        {
          "key": "2-8",
          "column_0": "usage",
          "column_1": "object",
          "column_3": "",
          "column_4": "Token usage returned by the video generation model."
        },
        {
          "key": "2-9",
          "column_0": "content",
          "column_1": "content",
          "column_3": "",
          "column_4": "Generated result content.",
          "children": [
            {
              "key": "2-9-1",
              "column_0": "video_url",
              "column_1": "string",
              "column_3": "https://{bucket}.tos-ap-southeast-1.bytepluses.com/xxxx/output.mp4?X-Tos-...",
              "column_4": "Generated video URL, usually valid for 24 hours. Download or persist the video promptly."
            },
            {
              "key": "2-9-2",
              "column_0": "last_frame_url",
              "column_1": "string",
              "column_3": "https://{bucket}.tos-ap-southeast-1.bytepluses.com/xxxx/last_frame.png?X-Tos-...",
              "column_4": "Last-frame image URL, usually valid for 24 hours. Returned only when return_last_frame=true was specified at submission."
            }
          ]
        },
        {
          "key": "2-10",
          "column_0": "template",
          "column_1": "object",
          "column_3": "{\"id\":\"replace/person_replace\"}",
          "column_4": "Business template actually used for this task. Only the template id is returned; the submitted paras are not returned."
        }
      ]
    }
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```


<span id="db5c27b5"></span>
### Example

**Request example**

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_video_edit_enhance",
    "operator_version": "v1",
    "task_id": "task-20260427143000-abc123"
}'
```


**Response example**

```JSON
{
  "metadata": {
    "task_status": "COMPLETED",
    "business_code": "0",
    "operator_id": "las_video_edit_enhance",
    "operator_version": "v1"
  },
  "data": {
    "id": "cgt-xxxxxxxx",
    "model": "dreamina-seedance-2-0-260128",
    "status": "succeeded",
    "resolution": "1080p",
    "ratio": "adaptive",
    "duration": 5,
    "framespersecond": 24,
    "usage": { "completion_tokens": 221386, "total_tokens": 221386 },
    "content": {
      "video_url": "https://{bucket}.tos-ap-southeast-1.bytepluses.com/xxxx/output.mp4?X-Tos-...",
      "last_frame_url": "https://{bucket}.tos-ap-southeast-1.bytepluses.com/xxxx/last_frame.png?X-Tos-..."
    },
    "template": {"id": "replace/person_replace"}
  }
}
```


<span id="9567f318"></span>
### Error codes


|**HttpStatusCode** |**Error code** |**Error message** |**Description** |
|---|---|---|---|
|400 |Parameter.Invalid |The parameter is invalid. |Invalid parameter, such as a missing task_id. |
|401 |Authorization.Missing |Missing Authorization. |Missing authorization. |
|401 |ApiKey.Invalid |The api key is invalid. |Invalid API key. |
|500 |Internal.ServerError |Internal server error. |Internal service error. |
