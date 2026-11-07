---
title: "Embodied Semantic Annotation"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/embodied-semantic-annotation"
---

This embodied semantic annotation operator is designed for embodied data collection scenarios covering physical robots, UMI, and human demonstrations. After users upload operation videos and select a task template, they can obtain information about interactive objects, action descriptions and corresponding timestamps for embodied data annotation.

# Operator introduction

> Operator ID: `las_embodied_caption`

## Application scenarios

* Physical robot, UMI and human operation data.

* Interactive object identification, temporal action annotation.

* Identify the objects interacted with during operations, and annotate actions such as grasping, handing over, placing as well as their start and end timestamps.

## Core capabilities

* **Interactive object identification**: Identify main interactive objects and their distinguishable instances, and annotate the corresponding interaction time segments.

* **Temporal action annotation**: Split continuous operations, and generate task descriptions, action start and end timestamps as well as skill tags.

* **Candidate\-guided task annotation**: Locate actual operations and their time intervals in videos by referring to candidate task descriptions.

## Supported tasks

* **Interactive object identification**: `embodied_active_object_detection@v2` uses horizontally stitched videos from left and right wrist cameras; `@v3` also supports single\-channel head\-mounted video input.

* **Temporal action annotation**: `embodied_action_captioning@v2` adopts the first\-person main perspective to output task descriptions and action segments attached with skill tags.

* **Candidate\-guided task annotation**: `embodied_action_captioning_prior@v2` takes candidate task descriptions as reference to output actions and corresponding time intervals.

## Effect display

* Input task template: `embodied_action_captioning@v2`

* Input main\-view video

   [video](https://dev-whhan-shanghai.tos-cn-shanghai.volces.com/public-data/las_embodied_caption/v1/main_480p.mp4)

* Output result excerpt

   ```json
   {
     "task_description": "After repositioning the trash can, pick up the plastic bottles on the table one by one and put them into the trash can.",
     "segments": [
       {
         "start": 2,
         "end": 6.4,
         "skill": "Move",
         "description": "The right hand grasps the white cylindrical trash can, adjusts its position on the table, and then releases it."
       }
     ]
   }
   ```

## Supported regions

* Asia Pacific(Johor)：ap\-southeast\-1

## Operator performance

|Breakdown item |Performance impact |
|---|---|
|Submit RPM |600 |
|Poll RPM |600 |
|Maximum concurrency |10 |

# Input and output requirements

## Input requirements

|Breakdown item |Detailed requirements |
|---|---|
|Supported input data modalities |* Video<br><br>* Text |
|Input format: Video |* Format: `mp4`, `mov`, `avi`, `mkv`, `flv`, or `webm`.<br><br>* Duration: Up to 3 hours.<br><br>* Size: Up to 10 GB.<br><br>* Analysis interval: Use `start` and `end` to limit the interval to analyze. |
|Input format: Text |Use `task_template` to select a built\-in task, or provide a custom task description through `query`. |
|Input path requirements |Provide the video through `video_url`. Accessible `http://`, `https://`, and `tos://bucket/key` addresses are supported. |

## Output requirements

|Breakdown item |Detailed requirements |
|---|---|
|Supported output data modalities |Text |
|Output format: Text |Returns structured interactive\-object annotations, task descriptions, action descriptions, timestamps, and skill tags according to the selected task. |
|Output path requirements |No output storage path is required. Retrieve the structured annotation result from the Poll response after the asynchronous task completes. |

# Billing information

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing item |ModelArk model invocation. Charges include input tokens, output tokens, and, when caching is used, cache\-hit input tokens and cache storage. |
   |Billing type |Pay\-as\-you\-go in USD per million tokens. Seed 2.0 models use tiered pricing based on prompt length. |
   |Billing formula |`Model invocation cost = input unit price × input tokens + cache-hit input unit price × cache-hit tokens + cache-storage unit price × cache-storage tokens × storage duration + output unit price × output tokens` |

* Billing details

   The following table lists the standard online\-inference prices for the models currently accepted by `model_name`. Prices are in USD per million tokens, except cache storage, which is in USD per million tokens per hour.

   |Supported model |Prompt length (K tokens) |Input (non\-audio) |Input (audio) |Cache storage |Cache\-hit input (non\-audio) |Cache\-hit input (audio) |Output |
   |---|---|---|---|---|---|---|---|
   |`seed-2-0-mini-260215` |[0, 128] |0.10 |Not supported |0.0083 |0.02 |Not supported |0.40 |
   ||(128, 256] |0.20 |Not supported |0.0083 |0.04 |Not supported |0.80 |
   |`seed-2-0-mini-260428` |[0, 128] |0.10 |1.50 |0.0083 |0.02 |0.30 |0.40 |
   ||(128, 256] |0.20 |3.00 |0.0083 |0.04 |0.60 |0.80 |
   |`seed-2-0-lite-260228` |[0, 128] |0.25 |Not supported |0.0083 |0.05 |Not supported |2.00 |
   ||(128, 256] |0.50 |Not supported |0.0083 |0.10 |Not supported |4.00 |
   |`seed-2-0-lite-260428` |[0, 128] |0.25 |3.75 |0.0083 |0.05 |0.75 |2.00 |
   ||(128, 256] |0.50 |7.50 |0.0083 |0.10 |1.50 |4.00 |
   |`seed-2-0-pro-260328` |[0, 128] |0.50 |Not supported |0.0083 |0.10 |Not supported |3.00 |
   ||(128, 256] |1.00 |Not supported |0.0083 |0.20 |Not supported |6.00 |
   |`dola-seed-2-1-turbo-260628` |[0, 256] |0.50 |Not supported |0.0083 |0.10 |Not supported |2.50 |

   On the ModelArk pricing page, the price for `dola-seed-2-1-turbo-260628` is listed under the model entry `dola-seed-2-1-turbo`. For the latest prices and billing rules, see [Model pricing](https://docs.byteplus.com/en/docs/modelark/model-pricing).

# Cautions and prerequisites

|Details |Caution and prerequisites |
|---|---|
|Costs |Before calling an operator, you need to understand the model invocation costs associated with using the operator. For details, see [Large model billing](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |

# Rest API call

## Submit

### Interface description

Invoke the las_embodied_caption operator to perform embodied semantic annotation. `video_url`, `ark_api_key`, and `model_name` are required fields; you can pass custom prompts via `query`, or select a built\-in task template via `task_template`, and configure other fields as needed based on task complexity and analysis requirements.

### Request parameters

**operator_id** string 必选 `Example value: las_embodied_caption`

Operator ID

**operator_version** string 必选 `Example value: v1`

Operator version, independent of template version

**data** las_embodied_caption_info 必选

Operator parameters

**video_url** string 必选 `Example value: https://las-ai-ap-southeast-1-online-bp.tos-ap-southeast-1.bytepluses.com/operator_cards_serving/public/online/las_embodied_caption/v1/main_480p.mp4`

Accessible address of the video to be analyzed, supporting http/https, TOS (tos://bucket/key), etc. The maximum supported duration is 3 hours and the maximum size is 10 GB; supported formats include mp4, mov, avi, mkv, flv, webm.

**ark_api_key** string 必选 `Example value: ark-xxxx`

Ark API Key.

**model_name** string 必选 `Example value: seed-2-0-pro-260328`

Specify the supported model.

Supported models:

\- Seed 2.0 Mini: `seed-2-0-mini-260215`, `seed-2-0-mini-260428`.

\- Seed 2.0 Lite: `seed-2-0-lite-260228`, `seed-2-0-lite-260428`.

\- Seed 2.0 Pro: `seed-2-0-pro-260328`.

\- Seed 2.1 Turbo: `dola-seed-2-1-turbo-260628`.

**ark_endpoint_id** string `Optional` `Example value: ep-xxxx`

Ark inference endpoint. When this field is not empty, the specified endpoint will be used, which must correspond to the same minor model version as model_name; when this field is empty, the default endpoint of the model will be used.

**query** string `Optional` `Example value: Annotate the actions of picking up and placing objects and their start and end times`

Required when task_template is not passed. An explicit query will override the template's default query, and other explicit parameters will override the corresponding template default values.

**task_template** string `Optional` `Example value: embodied_action_captioning@v2`

Task template, formatted as template_name@version_number. If the version number is omitted, v1 is used by default.

\- embodied_active_object_detection@v2: interactive object identification for dual\-wrist horizontally concatenated videos; @v3 also supports single\-channel head\-mounted videos.

\- embodied_action_captioning@v2: First\-person main perspective action annotation, including task descriptions and skill tags.

\- embodied_action_captioning_prior@v2: Temporal annotation combined with candidate task descriptions.

**task_context** task_context `Optional` `Example value: {"prompt_context":"..."}`

Task template context, see prompt_context below.

**prompt_context** string `Optional` `Example value: Main interactive objects: white cylindrical trash bin, white plastic bottle with red label`

Object information or skill vocabulary can be provided during action annotation. For prior@v2, a serialized JSON string of the candidate description string array must be provided, for example ["Adjust the position of the trash bin", "Pick up the plastic bottle"].

**start** float `Optional` `Example value: 0.0`

Analysis start time, in seconds. Default value is 0; the range is [0, video duration], and start < end.

**end** float `Optional` `Example value: 106.9`

Analysis end time, in seconds. If not passed, analysis will run until the end of the video; the range is [0, video duration], and start < end.

**fps** float `Optional` `Example value: 1.0`

Frame extraction frame rate, range [1/60, 10]. Default value is 1.0 when no template is used; templates may provide different default values, and explicit parameters override template configurations. Increasing this value will increase latency and Token consumption.

**media_resolution** string `Optional` `Example value: medium`

Video processing resolution level. Default value is medium when no template is used, supported values: low, medium, high, xhigh. Explicit parameters override template default configurations.

**reasoning_effort** string `Optional` `Example value: minimal`

Model reasoning intensity. Default value is minimal when no template is used. Common values: minimal, low, medium, high. Explicit parameters override template default configurations, and available levels are subject to the model.

**clip_context** string `Optional` `Example value: medium`

Single clip context range, default value is medium, supported values: medium, long. Explicit parameters override template default configurations.

**use_responses_api** boolean `Optional` `Example value: false`

Whether to enable the Responses API, default value is false. After enabling, video content can be cached with a default validity period of 1 hour, which is used for repeated analysis of the same video.

**previous_response_ids** list of string `Optional` `Example value: ["cache_resp_test"]`

Pass the previous response ID when reusing cached video content. This field only takes effect when use_responses_api=true.

### Response parameters

**metadata** metadata

Request metadata

**task_id** string `Example value: task-xxx`

Task ID in asynchronous mode, used for job status query.

**task_status** string `Example value: PENDING`

Task status in asynchronous mode.

\- PENDING: Task submitted and queued

\- RUNNING: Running

\- COMPLETED: Completed

\- FAILED: Failed

\- TIMEOUT: Timed out

**business_code** string `Example value: 0`

Business code. Usually returns `0` when submission is successful.

**error_msg** string

If there is an exception, detailed exception information will be returned.

### Examples

#### Request example

```bash
curl --location "${LAS_ENDPOINT}/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
  "operator_id": "las_embodied_caption",
  "operator_version": "v1",
  "data": {
    "video_url": "https://las-ai-ap-southeast-1-online-bp.tos-ap-southeast-1.bytepluses.com/operator_cards_serving/public/online/las_embodied_caption/v1/main_480p.mp4",
    "ark_api_key": "ark-xxxx",
    "model_name": "seed-2-0-pro-260328",
    "task_template": "embodied_action_captioning@v2"
  }
}'
```

#### Response example

```json
{
  "metadata": {
    "task_id": "task-xxx",
    "task_status": "PENDING",
    "business_code": "0",
    "error_msg": ""
  }
}
```

### Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Model.InvalidName |The model name is invalid. |The model name is invalid |
|401 |Authorization.Missing |Missing Authorization. |Missing authentication |
|401 |ApiKey.InValid |The api key is invalid. |The API key is invalid |

## Poll

### Interface description

Query the status and results of embodied semantic annotation tasks. After the task is completed successfully, `data.final_summary` returns a JSON\-formatted result string, which can be parsed to read the annotation fields of the corresponding template.

### Request parameters

**operator_id** string 必选 `Example value: las_embodied_caption`

Operator ID: las_embodied_caption

**operator_version** string 必选 `Example value: v1`

Operator version

**task_id** string 必选 `Example value: task-xxx`

Task ID

### Response parameters

**metadata** metadata

Request metadata

**task_id** string `Example value: task-xxx`

Task ID in asynchronous mode.

**task_status** string `Example value: COMPLETED`

Task status in asynchronous mode.

\- PENDING: Task submitted and queued

\- RUNNING: Task in progress

\- COMPLETED: Task finished

\- FAILED: Task failed

\- TIMEOUT: Task timed out

Asynchronous tasks usually require combining `task_status=COMPLETED` and `business_code=0` to determine that the task is truly completed.

**submit_time** string `Example value: 2026-07-21T16:04:06+08:00`

Task submission time, in ISO 8601 timestamp format.

**end_time** string `Example value: 2026-07-21T16:04:06+08:00`

Task end time, in ISO 8601 timestamp format.

**business_code** string `Example value: 0`

Business code. Usually returns `0` when business processing is successful.

**error_msg** string

If an exception occurs, detailed exception information will be returned.

**data** las_embodied_caption_result

Returned data

**token_usages** list of token_usage_info `Example value: [{"model_name":"seed-2-0-pro-260328","token_usage":{"prompt_tokens":4453444,"completion_tokens":10929}}]`

Token usage information

**model_name** string `Example value: "seed-2-0-pro-260328"`

Model name

**token_usage** token_usage `Example value: {"prompt_tokens": 4453444, "completion_tokens": 10929, "audio_tokens": 0, "cached_tokens": 10032, "cached_audio_tokens": 0, "cached_store_tokens": 10032, "total_tokens": 4464373}`

Token usage

**prompt_tokens** integer `Example value: 4453444`

Number of input prompt tokens, including all types such as text, audio, etc.

**completion_tokens** integer `Example value: 10929`

Number of tokens generated by the model

**audio_tokens** integer `Example value: 0`

Number of audio tokens in the input

**cached_tokens** integer `Example value: 10032`

Number of cache\-hit tokens, including all types such as text, audio, etc.

**cached_store_tokens** integer `Example value: 10032`

Number of tokens written to cache

**cached_audio_tokens** integer `Example value: 0`

Number of cache\-hit audio tokens

**total_tokens** integer `Example value: 4464373`

Total number of tokens, the value is equal to prompt_tokens + completion_tokens

**video_duration** float `Example value: 106.9`

Video duration, in seconds

**resolution** string `Example value: 854x480`

Original video resolution, not the media_resolution level

**final_summary** string `Example value: JSON string`

Annotation result. Interactive object identification returns objects; action@v2 returns task_description and segments (start, end, skill, description); prior@v2 returns segments (start, end, description). Times are in seconds.

**response_ids** list of string `Example value: ["cache_resp_test"]`

List of response identifiers returned after the Responses API is enabled, which can be passed in via `previous_response_ids` in subsequent Submit requests to reuse cached video content

### Examples

#### Request example

```bash
curl --location "${LAS_ENDPOINT}/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
    "operator_id": "las_embodied_caption",
    "operator_version": "v1",
    "task_id": "task-xxx"
}'
```

#### Response example

The following annotation content is an excerpt of the reference result. The task times and token counts are illustrative. This example retains the original Chinese annotations in `final_summary`.

```json
{
  "metadata": {
    "task_id": "task-xxx",
    "task_status": "COMPLETED",
    "submit_time": "2026-10-09T16:00:00+08:00",
    "end_time": "2026-10-09T16:01:00+08:00",
    "business_code": "0",
    "error_msg": ""
  },
  "data": {
    "token_usages": [
      {
        "model_name": "seed-2-0-pro-260328",
        "token_usage": {
          "prompt_tokens": 10000,
          "audio_tokens": 0,
          "completion_tokens": 1000,
          "cached_audio_tokens": 0,
          "cached_tokens": 0,
          "cached_store_tokens": 0,
          "total_tokens": 11000
        }
      }
    ],
    "video_duration": 106.9,
    "resolution": "854x480",
    "final_summary": "{\"task_description\":\"调整桌面白色圆柱垃圾桶的摆放位置后，逐个拾取桌面上的塑料瓶与透明长方塑料盒，部分物品经双手递交后丢入垃圾桶内；投放透明无标签塑料瓶时瓶子掉落至垃圾桶外侧桌面，最终清空桌面待丢弃物品后双手返回初始位置。\",\"segments\":[{\"start\":0,\"end\":2,\"skill\":\"None\",\"description\":\"双手未与任务物品交互，从初始位置抬起向桌面方向移动。\"},{\"start\":2,\"end\":6.4,\"skill\":\"Move\",\"description\":\"右手握持白色圆柱垃圾桶，拖动调整其在桌面的摆放位置后松开。\"},{\"start\":6.4,\"end\":8.2,\"skill\":\"None\",\"description\":\"双手在桌面上方移动，定位待拾取的塑料瓶。\"},{\"start\":8.2,\"end\":12.8,\"skill\":\"Pick\",\"description\":\"左手抓取桌面上的白色带红标签塑料瓶，右手扶住瓶身协同将瓶子从桌面拿起。\"},{\"start\":12.8,\"end\":14.4,\"skill\":\"Drop\",\"description\":\"右手将白色带红标签塑料瓶移动至垃圾桶上方，松开手将瓶丢入垃圾桶内。\"}]}",
    "response_ids": []
  }
}
```

### Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Task.NotFound |The task is not found. |Task does not exist |
|401 |Authorization.Missing |Missing Authorization. |Missing authentication |
|401 |ApiKey.InValid |The api key is invalid. |Invalid API key |
