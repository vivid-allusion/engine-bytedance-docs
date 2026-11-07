---
title: "Fine-grained video understanding"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Fine-grained_video_understanding"
---

The video fine\-grained understanding operator is designed for general video content and supports direct understanding and analysis of videos. Whether it is a short video, film clip, course recording, or surveillance footage, after the user uploads a video and provides a query or task_template, the video content can be described, queried, and information can be extracted, with relevant segments located using timestamps. Supports video input up to several hours (maximum 3 hours, 10 GB), and also supports joint audio\-video understanding by combining visual, speech, and sound effect information, making it suitable for retrieval, question answering, and content analysis scenarios.

<span id="operator-introduction"></span>
# Operator introduction

> Operator ID: las_video_understanding


<span id="applicable-scenarios"></span>
## Applicable scenarios

Supports several video content understanding tasks:


* **Cross\-segment Q&A**: Integrates information from multiple clips to answer complex questions;

* **Highlight generation**: Extracts key segments (emotional climaxes, plot twists, and more);

* **Role tracking**: Continuously tracks target entities and analyzes their behavior;

* **Chapter breakdown**: Logically splits long videos into chapters;

* **Comprehensive audio\-video analysis**: Outputs integrated understanding results by combining visual changes, speech content, and sound effect cues;

* **Key quote extraction**: Extracts core viewpoints or memorable lines from the video.


Typical application scenarios are as follows.

&nbsp;


|Scenario types |Capabilities assessed |Sample questions |
|---|---|---|
|Sports competitions |Role tracking, tactic recognition, cross\-segment summarization, highlight generation |"Summarize all scoring moments and methods for the player in this match" |
|TV series |Highlight generation, temporal reasoning, emotion trajectory analysis, character relationship mapping |"Identify three key segments of relationship changes between the male and female leads in this episode" |
|Educational open course |Chapter breakdown, key point summary, cross\-segment Q&A, Slide OCR |"Split the speech into chapters according to the agenda and generate key points" |
|Evaluation type |Parameter extraction, screen OCR, emotion analysis |"Summarize three advantages and two disadvantages of the mobile phone review" |
|Tutorial type |Operation step breakdown, risk alert identification, retrieval index |"Break down the PS tutorial into an operation guide and associate timestamps" |
|Traffic monitoring type |Event detection, violation identification, license plate OCR, target tracking |"Detect illegally parked vehicles and license plates in the video" |


<span id="core-capabilities"></span>
## Core capabilities


* **General video input processing**: Supports hour\-level video input (up to 3h and 10G), and can understand and analyze video content based on the user's query.

* **Audio\-visual understanding**: Combines video frames, speech, background audio, and sound effects for comprehensive analysis, suitable for scenarios that require both visual and auditory cues.

* **Video content description**: Generates content descriptions based on video frames, subtitles, and context, suitable for video overviews, clip descriptions, and similar scenarios.

* **Video Q&A**: Supports natural language Q&A around video content and returns analysis results related to the question.

* **Information extraction**: Extracts people, actions, scenes, subtitles, and other information from videos. The specific extraction dimensions are determined by the query.

* **Timestamp association**: Locates related segments with time information, making it easier to reference and trace key video content.

* **Cache reuse**: Supports Responses API frame caching, suitable for asking multiple questions about the same video.


<span id="effect-demonstration"></span>
## Effect demonstration


---



[Example 1]


<columns>
<columnsItem zoneid="YOdcKtQR89">

* Input video

   <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e472c17b08f4eb999cedc9ebdf331f3~tplv-goo7wpa0wc-image.image" controls></video>
   

</columnsItem>
<columnsItem zoneid="XALGFgTslD">

* Result example 1:

   * API output result

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f3a1cc58aa94813bcafa5c9ce84380f~tplv-goo7wpa0wc-topic.webp) </span>

   * Key parameters: split by time, generate summaries of actions and scene content

      ```JSON
      {
      "video_url": "tos://las-doctest-bp/las-ai/input/video/short_drama/english/EP01.mp4",
      "task_template": "dense_video_captioning"  ,
      "model_name": "seed-2-0-lite-260228215"
          }
      ```
      

</columnsItem>
<columnsItem zoneid="RQ1JloD1oL">

* Result example 2:

   * API output result

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5207ece5478d4559bb6b133fd974b67d~tplv-goo7wpa0wc-topic.webp) </span>

   * Key parameters: custom requirements for content summary output

      ```JSON
      {
      "video_url": "tos://las-doctest-bp/las-ai/input/video/short_drama/english/EP01.mp4",
      "query": "Identify three key segments showing changes in the relationship between the male and female leads in this episode. For each segment, provide the timestamp, a concise description of what happens, the characters involved, and the dialogue or subtitle evidence when available. Return every field and all text in English. Do not output Chinese.",
      "model_name": "seed-2-0-lite-260228"
          }
      ```
      

</columnsItem>
</columns>



---



[Example 2]


<columns>
<columnsItem zoneid="G3POMpLzTu">

* Input Video

   <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f35ce742d45142559d12e89109ba48eb~tplv-goo7wpa0wc-raw.image" controls></video>
   

</columnsItem>
<columnsItem zoneid="uZEVa31aqT">

* Key parameters

   ```Bash
   {
   "query": "Analyze the entire sports match from beginning to end and identify every scoring event without omission. Return only a valid JSON array and no Markdown or explanatory text. Each array item must contain exactly these fields: time, team, event, current_score. Use this structure: [{\"time\":\"74s\",\"team\":\"Blue Team\",\"event\":\"Made layup\",\"current_score\":\"41:39\"}]. List all scoring events in chronological order. The video has no audio, so use visual evidence, scoreboard changes, player or team actions, and on-screen text. All field values and all text must be in English. Do not output Chinese.",
   "model_name": "seed-2-0-lite-260228",
   "fps": 5
   }
   ```
   

</columnsItem>
<columnsItem zoneid="f5gXaWU1qH">

* Output


```Plain
"time": "15s", "team": "Blue Team", "event": "Made mid-range shot", "current_score": "59:37" ,
"time": "29s", "team": "Red Team", "event": "Made layup", "current_score": "59:39" , 
"time": "44s", "team": "Blue Team", "event": "Made layup", "current_score": "61:39" ,
"time": "60s", "team": "Red Team", "event": "Made three-point shot", "current_score": "61:42" , 
"time": "75s", "team": "Blue Team", "event": "Made layup", "current_score": "63:42" 
```


</columnsItem>
</columns>



---



<span id="supported-regions"></span>
## Supported regions


* Asia Pacific(Johor)：ap\-southeast\-1


<span id="operator-performance"></span>
## Operator performance

&nbsp;


|Sub\-item |Performance impact description |
|---|---|
|Maximum RPM |600 |
|Maximum concurrency |10 |
|Latency |Total latency depends on video duration, content complexity, and network environment. |


<span id="input-and-output-requirements"></span>
# Input and output requirements

<span id="input-requirements"></span>
## Input requirements

&nbsp;


|Subdivision |Detailed description |
|---|---|
|Supported input data modalities |* Video<br><br>* Text (supplementary task text) |
|Input format: Video |* Format: Common video formats such as mp4, mov, avi, mkv are supported<br><br>* Size: Supports input videos up to 3 hours and 10 GB |
|Input path requirements |Provide input data to the operator via the request parameter `video_url`. Currently, two methods are supported: public URL and TOS path.<br><br><br>* Public URL: A video URL accessible over the public internet, in the format `http/https`.<br><br>* TOS path: After uploading the data to be processed to a TOS Bucket under the same primary account and region as the current LAS service, you can provide the TOS path in the format `tos://bucket_name/demo`. |


<span id="output-requirements"></span>
## Output requirements

&nbsp;


|Subdivision |Detailed description |
|---|---|
|Output data modalities |Text |
|Output path: Returned by API |After the operator has finished processing, the result is returned directly through the return parameters of the operator Poll interface. |


<span id="billing-information"></span>
# Billing information


* Billing standards

&nbsp;

   
   |Breakdown |Description of billing standards |
   |---|---|
   |Billing items |There are four billing items: **model input, model output, cache storage, cache hits**. The total payable cost is the sum of all billing items. |
   |Billing type |Usage\-based billing, unit: `USD/million tokens`, billed hourly based on actual usage. |
   |Unit price |The unit price for each billing item is tiered based on the model input length at the time of model invocation. The unit price varies depending on the input length tier. |
   

* Billing details

   Billing formula: `Total cost = Model input cost + Model output cost + Cache storage cost + Cache hit cost`

&nbsp;

   
   |Model type |Input length range (thousand tokens) |Input (non\-audio)<br><br>USD/million tokens |Input (audio)<br><br>USD/million tokens |Cache storage<br><br>USD/million tokens/hour |Cache hit (non\-audio)<br><br>USD/million tokens |Cache hit (audio)<br><br>USD/million tokens |Output<br><br>USD/million tokens |
   |---|---|---|---|---|---|---|---|
   |dola\-seed\-2.1\-turbo |Input length [0, 256] |1 |Not applicable |0.0166 |0.2 |Not applicable |5 |
   |seed\-2.0\-pro |Input length [0, 128] |1 |Not applicable |0.0166 |0.2 |Not applicable |6 |
   ||Input length (128, 256] |2 |Not applicable |0.0166 |0.4 |Not applicable |12 |
   |seed\-2.0\-lite |Input length [0, 128] |0.5 |7.5 |0.0166 |0.1 |1.5 |4 |
   ||Input length (128, 256] |1 |15 |0.0166 |0.2 |3 |8 |
   |seed\-2.0\-mini |Input length [0, 128] |0.2 |Not applicable |0.0166 |0.04 |Not applicable |0.8 |
   ||Input length (128, 256] |0.4 |Not applicable |0.0166 |0.08 |Not applicable |1.6 |
   |seed\-1.8 |Input length [0, 128] |0.5 |Not applicable |0.0166 |0.1 |Not applicable |4 |
   ||Input length (128, 256] |1 |Not applicable |0.0166 |0.1 |Not applicable |8 |
   

* Billing estimation

   * Based on the above billing details table, you can estimate the approximate number of tokens in the input video. Combined with the operator request code, this provides an estimate of the overall model input length.

   * Caution: This estimation result is for reference only and cannot be used as the exact input length data. When processing tasks, there will also be system prompts and other inputs, but the length of these other inputs is generally short.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">说明   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, when using the seed\-2.1 model, the billing statement still displays impact factors related to seed\-2.0. You can determine the actual model type used in the current bill based on details such as the unit price in the billing statement.   </div>
   

<span id="caution-and-prerequisites"></span>
# Caution and prerequisites

&nbsp;


|Details |Caution and prerequisites |
|---|---|
|Costs |Before calling an operator, you need to understand the model invocation costs associated with using the operator. For details, see [Large model billing](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |


<span id="api-invocation"></span>
# API invocation

<span id="api-call-instructions"></span>
## API call instructions


* This operator's API is an asynchronous task interface. Submit a task through the `Submit` interface to obtain the `task_id`. Then use the `Poll` interface to check the status of the corresponding task (`task_id`) and retrieve the operator's processing result.

* Caution: After a task is submitted, the `task_id` is valid for 3 days. After 3 days, the `task_id` cannot be used to retrieve the operator's processing result.


<span id="submit"></span>
## Submit

<span id="interface-description"></span>
### Interface description

Call the las_video_understanding operator for fine\-grained video understanding. The minimum valid request can include `video_url` and `query`, or `video_url` and `task_template`; configure the other fields as needed based on task complexity and analysis requirements.

<span id="request-parameters"></span>
### Request parameters



**operator_id** <span data-label="purple">string</span> <span data-api-tag="require|BXhL8P">必选</span> `Example value: las_video_understanding`

Operator ID: las_video_understanding



**operator_version** <span data-label="purple">string</span> <span data-api-tag="require|T4DS4s">必选</span> `Example value: v1`

Operator version



**data** <span data-label="purple">long_video_understand_info</span> <span data-api-tag="require|OoUfxy">必选</span>

Operator parameters


**video_url** <span data-label="purple">string</span> <span data-api-tag="require|daKl6y">必选</span> `Example value: https://example.com/video.mp4`

Accessible URL of the video to be analyzed. Supports `http/https`, Volcengine TOS (`tos://bucket/key`), etc. Please ensure the server can fetch the resource, and it is recommended to use a stable, directly downloadable file link. Maximum supported duration: 3 hours; maximum supported size: 10 GB; supported formats: `mp4`, `mov`, `avi`, `mkv`, `flv`, `webm`.



**query** <span data-label="purple">string</span> `Example value: Summarize the key scoring moments in the video in chronological order, and note the player numbers and timestamps`

Analysis goal or question for the video. Required when task_template is not provided. If both query and task_template are provided, query overrides the parameters in the template. It is recommended to make the expected output and result organization as clear as possible. In general, the more specific the question, the more stable the result will be.



**task_template** <span data-label="purple">string</span> `Example value: general_video_captioning@v1`

Task template. After being specified, it automatically fills in the default configuration required by the task; when using a template, only `video_url` and `task_template` are required. Use `template_name@version` to specify a template version. If the version is omitted, `v1` is used by default, so `general_video_captioning` is equivalent to `general_video_captioning@v1`.

Supported values:


* `general_video_captioning`: Generates a continuous, detailed, unstructured Chinese video\-level description.

* `dense_video_captioning`: Generates fine\-grained structured JSON with event and action/scene time segmentation.

* `video_audio_understanding`: Generates audio\-visual understanding results from video frames, speech, and sound effects.

* `embodied_active_object_detection`: Identifies main interactive objects in embodied manipulation scenarios and supports `v2`.

* `embodied_action_captioning`: Generates action temporal annotations for embodied manipulation scenarios and supports `v2`.

* `object_detection`: Object detection task that detects input\-specified targets and returns bbox.



**task_context** <span data-label="purple">task_context</span> `Example value: {"prompt_context":"Main interactive objects: yellow pushpin, light-green sticky note."}`

Structured context for task templates, used to provide additional text information to the template. Currently supports prompt_context and target_object: prompt_context supplies prior task context for embodied action captioning templates, and target_object supplies target categories and descriptions for the object detection template.


**prompt_context** <span data-label="purple">string</span> `Example value: Main interactive objects: yellow pushpin, light-green sticky note.`

Prior task context information. Currently supported when task_template is embodied_action_captioning or embodied_action_captioning@v2.



**target_object** <span data-label="purple">string</span> `Example value: pink_bear (pink plush bear)`

Target detection categories and descriptions. Currently supported when task_template is object_detection. The recommended format is English category key (natural\-language description); the returned category uses the key before the parentheses.




**start** <span data-label="purple">float</span> `Example value: 30.0`

Video analysis start time, in seconds. Range: `[0, video duration]`, and `start < end`.



**end** <span data-label="purple">float</span> `Example value: 120.0`

Video analysis end time, in seconds. Range: `[0, video duration]`, and `start < end`.



**fps** <span data-label="purple">float</span> `Example value: 1.0`

Video frame extraction rate. Increasing `fps` can improve analysis accuracy, but will also increase processing latency, token consumption, and cost. The default value is `1.0`, and the value range is `[1/60, 10]`. The default value is sufficient for general scenarios; when the task requires identifying fast actions or more fine\-grained events, you can try to increase the value appropriately.



**media_resolution** <span data-label="purple">string</span> `Example value: medium`

Video processing resolution level, which affects the retention of visual details and processing latency. The default value is `medium`, supported values: `low`, `medium`, `high`, `xhigh`. The default value is sufficient for general scenarios; when the task has high requirements for identifying visual details such as subtitles, small targets, and jersey numbers, you can try to use a higher level.



**model_name** <span data-label="purple">string</span> `Example value: seed‑2‑0‑lite‑260228`

Specifies the video understanding model. The default is `seed‑2‑0‑lite‑260228`. Unless you have specific requirements, we recommend using the default value.

Supported models:


* Seed 1.8: `seed‑1‑8‑251228`.

* Seed 2.0 Mini: `seed-2-0-mini-260215`, `seed-2-0-mini-260428`.

* Seed 2.0 Lite: `seed-2-0-lite-260228`, `seed-2-0-lite-260428`.

* Seed 2.0 Pro: `seed-2-0-pro-260328`.

* Seed 2.1 Turbo: `dola-seed-2-1-turbo-260628`.



**reasoning_effort** <span data-label="purple">string</span> `Example value: minimal`

Controls the model reasoning intensity. The default value is `minimal`, which means deep thinking is disabled. Common values: `minimal`, `low`, `medium`, `high`. The default value is sufficient for general scenarios; when the task involves cross\-segment induction, complex causal relationships or multi\-role analysis, you can try to use a higher level.



**clip_context** <span data-label="purple">string</span> `Example value: medium`

Controls the context range of a single video segment. The default value is `medium`, supported values: `medium`, `long`. The default value is sufficient for general scenarios; when the task is more dependent on context continuity, you can try to use the higher level `long`.



**use_responses_api** <span data-label="purple">boolean</span> `Example value: false`

Whether to enable the Responses API capability. After enabling, the video content will be cached with a validity period of 1 hour, which is suitable for repeated analysis requests of the same video.



**previous_response_ids** <span data-label="purple">list of string</span> `Example value: ["cache_resp_test"]`

After passing in the list of response identifiers returned by the previous round of response, the cached video content can be reused. It only takes effect when use_responses_api=true.




&nbsp;

<span id="response-parameters"></span>
### Response parameters


**metadata** <span data-label="purple">metadata</span>

Request meta information


**task_id** <span data-label="purple">string</span> `Example value: task-xxx`

Task ID in asynchronous mode, used for job status query.



**task_status** <span data-label="purple">string</span> `Example value: PENDING`

Task status in asynchronous mode.


* PENDING: Submitted task is queuing

* RUNNING: In progress

* COMPLETED: Completed

* FAILED: Failed

* TIMEOUT: Timed out



**business_code** <span data-label="purple">string</span> `Example value: 0`

Business code. Usually returns `0` when the submission is successful.



**error_msg** <span data-label="purple">string</span>

If an exception occurs, detailed exception information will be returned.



&nbsp;

<span id="recommended-configuration"></span>
### Recommended configuration

&nbsp;


|Scenario |Recommended parameters |
|---|---|
|General summary, basic Q&A |The default parameters are sufficient |
|Sports competitions, action detail analysis |`fps` can be increased as appropriate; for tasks requiring high accuracy in recognizing jersey numbers, small targets, and other details, `media_resolution=high` can be considered |
|Meeting minutes, course breakdown, plot sorting |`clip_context=long` can be considered; for tasks involving complex induction, `reasoning_effort` can be further increased |
|Repeated analysis of the same video, reuse of cached video |`use_responses_api=true`, and pass in `previous_response_ids`; video cache is valid for 1 hour |


<span id="example"></span>
### Example

<span id="request-example"></span>
#### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_video_understanding",
    "operator_version": "v1",
    "data": {
      "video_url": "https://example.com/video.mp4",
      "task_template": "general_video_captioning@v1",
      "model_name": "dola-seed-2-1-turbo-260628"
    }
}'
```


<span id="response-example"></span>
#### Response example

```JSON
{
  "metadata": {
    "task_id": "task-20251125163544-abc123",
    "task_status": "PENDING",
    "business_code": "200",
    "error_msg": ""
  }
}
```


<span id="poll"></span>
## Poll

<span id="interface-description-1"></span>
### Interface description

Query the execution status and results of the video understanding task.

<span id="request-parameters-1"></span>
### Request parameters



**operator_id** <span data-label="purple">string</span> <span data-api-tag="require|h3V9UV">必选</span> `Example value: las_video_understanding`

Operator ID



**operator_version** <span data-label="purple">string</span> <span data-api-tag="require|tARGAL">必选</span> `Example value: v1`

Operator version



**task_id** <span data-label="purple">string</span> <span data-api-tag="require|DSaOOZ">必选</span> `Example value: task-xxx`

Task ID



&nbsp;

<span id="response-parameters-1"></span>
### Response parameters



**metadata** <span data-label="purple">metadata</span>

Request metadata


**task_id** <span data-label="purple">string</span> `Example value: task-xxx`

Task ID in asynchronous mode.



**task_status** <span data-label="purple">string</span> `Example value: COMPLETED`

Task status in asynchronous mode.


* PENDING: Task is queued after submission

* RUNNING: Task is running

* COMPLETED: Task is finished

* FAILED: Task failed

* TIMEOUT: Task timed outAsynchronous tasks usually need to be judged as truly completed by combining `task_status=COMPLETED` and `business_code=0`.



**submit_time** <span data-label="purple">string</span> `Example value: 2026-07-21T16:04:06+08:00`

Task submission time, in ISO 8601 timestamp format.



**end_time** <span data-label="purple">string</span> `Example value: 2026-07-21T16:04:06+08:00`

Task end time, in ISO 8601 timestamp format.



**business_code** <span data-label="purple">string</span> `Example value: 0`

Business code. It usually returns `0` when business processing is successful.



**error_msg** <span data-label="purple">string</span>

If there is an exception, detailed exception information will be returned.




**data** <span data-label="purple">long_video_understand_result</span>

Returned data


**token_usages** <span data-label="purple">list of token_usage_info</span> `Example value: [{"model_name":"seed‑2‑0‑lite‑260228","token_usage":{"prompt_tokens":4453444,"completion_tokens":10929}}]`

Token usage


**model_name** <span data-label="purple">string</span> `Example value: seed‑2‑0‑lite‑260228`

Model name



**token_usage** <span data-label="purple">token_usage</span> `Example value: {"prompt_tokens": 4453444, "completion_tokens": 10929, "audio_tokens": 0, "cached_tokens": 10032, "cached_audio_tokens": 0, "cached_store_tokens": 10032, "total_tokens": 4464373}`

Token usage


**prompt_tokens** <span data-label="purple">integer</span> `Example value: 4453444`

Number of prompt tokens in the input, including all types such as text and audio



**completion_tokens** <span data-label="purple">integer</span> `Example value: 10929`

Number of tokens generated by the model



**audio_tokens** <span data-label="purple">integer</span> `Example value: 0`

Number of audio tokens in the input



**cached_tokens** <span data-label="purple">integer</span> `Example value: 10032`

Number of cache\-hit tokens, including all types such as text and audio



**cached_store_tokens** <span data-label="purple">integer</span> `Example value: 10032`

Number of tokens written to cache



**cached_audio_tokens** <span data-label="purple">integer</span> `Example value: 0`

Number of cache\-hit audio tokens



**total_tokens** <span data-label="purple">integer</span> `Example value: 4464373`

Total number of tokens, equal to `prompt_tokens + completion_tokens`





**video_duration** <span data-label="purple">float</span> `Example value: 847.296`

Original video duration, in seconds



**resolution** <span data-label="purple">string</span> `Example value: 1920x1080`

Original video resolution



**final_summary** <span data-label="purple">string</span> `Example value: The video as a whole presents...`

Final summary



**response_ids** <span data-label="purple">list of string</span> `Example value: ["cache_resp_test"]`

List of response identifiers returned after enabling the Responses API, which can be passed in via `previous_response_ids` in subsequent Submit requests to reuse cached video content




&nbsp;

<span id="example-1"></span>
### Example

<span id="request-example-1"></span>
#### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_video_understanding",
    "operator_version": "v1",
    "task_id": "task-20251125163544-abc123"
}'
```


<span id="response-example-1"></span>
#### Response example

```JSON
{
    "metadata": {
        "task_id": "task-20251125163544-abc123",
        "task_status": "COMPLETED",
        "submit_time": "2026-07-21T16:04:06+08:00",
        "end_time": "2026-07-21T16:04:06+08:00",
        "business_code": "0",
        "error_msg": ""
    },
    "data": {
        "token_usages": [
            {
                "model_name": "doubao-seed-2-0-lite-260215",
                "token_usage": {
                    "prompt_tokens": 4453444,
                    "completion_tokens": 10929,
                    "cached_tokens": 2612,
                    "cached_store_tokens": 2612,
                    "total_tokens": 4464373
                }
            }
        ],
        "video_duration": 847.296,
        "resolution": "1920x1080",
        "final_summary": "The video as a whole describes...",
        "response_ids": [
            "cache_resp_test"
        ]
    }
}
```


<span id="error-code"></span>
## Error code

&nbsp;


|HttpCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Model.InvalidName |The model name is invalid. |Model name is invalid |
|401 |Authorization.Missing |Missing Authorization. |Authorization missing |
|401 |ApiKey.Invalid |The api key is invalid. |API key is invalid |
