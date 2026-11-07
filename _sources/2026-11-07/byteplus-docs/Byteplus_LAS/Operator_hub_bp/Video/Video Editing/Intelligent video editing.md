---
title: "Intelligent video editing"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Intelligent_video_editing"
---

The video intelligent editing operator leverages multimodal large models to provide intelligent video editing capabilities, enabling users to quickly extract valuable content segments from long videos. Supports understanding editing requirements described in natural language, reference image\-assisted recognition (such as characters, objects, scenes, and dialogues), multidimensional video content analysis (visuals, subtitles, storyline), and outputs standardized editing decision information (timestamps, descriptions, and more).

<span id="operator-introduction"></span>
# Operator introduction

> Operator ID: las_video_edit


<span id="applicable-scenarios"></span>
## Applicable scenarios


* Video editing

   * Batch production of short drama delivery materials: For live\-action short dramas and AI comic drama delivery scenarios, after inputting the original episode, the operator can intelligently identify storyline highlights with high conversion potential, combine storyline understanding to generate high\-impact mixed editing materials in batches that are ready for delivery, significantly improving the efficiency of material production and reducing the production cost per material.

   * Assist manual editing to improve ROI: Simultaneously outputs precise timestamps, storyline shot lists, and highlight segment information, helping editors quickly locate key conflicts, plot twists, and emotional highlights, reducing the cost of frame\-by\-frame searching and rough editing. Meanwhile, use AI\-generated materials for online trial delivery to quickly validate user interest points, then have manual editors perform in\-depth secondary editing based on validated highlight storylines, enhancing material production efficiency and delivery ROI.

* Audio editing

   * Intelligent cleaning of voice\-over materials: Identifies valid content, stutters, repetitions, speech errors, noise, and more, for downstream processing according to tags.


<span id="core-capabilities"></span>
## Core capabilities


* A variety of common editing task scenarios for video and audio editing are preset for you. You can quickly invoke the operator for editing by using the preset editing tasks (`task_name`).

   * Video editing:

      * Common scenarios covered include: character segment extraction, highlight segment detection, product segment detection, custom editing, and more.

      * Supports reference image\-assisted recognition (such as characters, objects, scenes), and multidimensional video content analysis (visuals, subtitles, storyline).

      * Short drama scenario: Supports rendering of the three key elements for short dramas (title, prompt, and corner mark), suitable for vertical screen short drama scenarios; supports highlight pre\-roll functionality, automatically extracting a 10–15 second attractive segment as the opening.

   * Audio editing:

      * Covers single\-person and two\-person voice\-over scenarios.

      * Supports returning semantic tags such as `spear`, `label`, and `label_reason`, facilitating in\-depth voice\-over video editing based on processing results.

* In addition to preset editing tasks, user\-defined editing requirements are also supported. By configuring custom editing requirements (`task_description`), enabling flexible interpretation of editing requirements described in natural language.

* Supports enabling ASR\-enhanced semantic understanding (`enable_asr=true`), suitable for editing scenarios with rich dialogue content and no subtitles, improving the smoothness of segment boundaries.

* Standardized editing decision output includes: timestamps, descriptions of editing outcomes, and more, facilitating further downstream editing processing.


<span id="effect-showcase"></span>
## Effect showcase


---



<div style="text-align: center">
<strong>[Video editing example: Highlight sequential editing for short dramas]</strong></div>



<columns>
<columnsItem zoneid="GVrAjohWfA">

* Input video

   <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e472c17b08f4eb999cedc9ebdf331f3~tplv-goo7wpa0wc-image.image" controls></video>
   

</columnsItem>
<columnsItem zoneid="Mes2c4bJB0">

* Key parameters

   ```JSON
   {
   "mode": "detail",
   "enable_asr":"true",
   "task_name":"SHORT_DRAMA_HIGHLIGHT_EXTRACTION",
   "extra_config":{
       "miniseries_elements":{
       "title":"THE DASHWOOD FAMILY",
       "hint":"Film and television effects",
       "template_name":"模板1"}
               },
   "preset_intro":{
        "transition":"fade",
        "transition_duration":0.5
               }
       }
   ```
   

</columnsItem>
<columnsItem zoneid="Dbsm7KuY1m">

* Output result

   <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42555ef71fb84000b87240bab8b5920f~tplv-goo7wpa0wc-image.image" controls></video>
   

</columnsItem>
</columns>



---



<div style="text-align: center">
<strong>[Video editing example: Key character segment extraction]</strong></div>



<columns>
<columnsItem zoneid="qnYZzabFWq">

* Input video

   <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e472c17b08f4eb999cedc9ebdf331f3~tplv-goo7wpa0wc-image.image" controls></video>
   

* Task description

   ```JSON
   {
   "task_description":"Extract every segment in which the character Fanny Dashwood appears, including all of her dialogue. Use the reference image to identify Fanny Dashwood. Return all descriptions, dialogue text, plot summaries, labels, metadata values, and other textual output entirely in English. Do not output Chinese."
       }
   ```
   

* Reference images

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6f48d6f5c0447248f789bb7347b5f9b~tplv-goo7wpa0wc-topic.webp) </span>

</columnsItem>
<columnsItem zoneid="GK80P7KoRC">

* Output Video 1

   <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cefd9baf27b8420b90b8363590290a8f~tplv-goo7wpa0wc-image.image" controls></video>
   

* Output Video2

   <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf80c474805c4b17becd5eb8ac0a61b9~tplv-goo7wpa0wc-image.image" controls></video>
   

</columnsItem>
<columnsItem zoneid="YV9tqoEfUO">

* Output Video 3

   <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30e764f8753e4e5a83ffb864df940232~tplv-goo7wpa0wc-image.image" controls></video>
   

* Output Video 4

   <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb265e3dfcb64700bc9acf6f3c483c8e~tplv-goo7wpa0wc-image.image" controls></video>
   

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
|Processing time |* Total processing time depends on the source file duration, processing method, and network environment.<br><br>* Performance and cost balance for different processing methods:<br><br>   * Simple mode: fast speed, low cost<br><br>   * Detailed mode: high quality, higher cost |
|Network performance |It is recommended to access TOS sources and write TOS results within the BytePlus intranet environment for more stable network performance. |


<span id="input-and-output-requirements"></span>
# Input and output requirements

<span id="input-requirements"></span>
## Input requirements

&nbsp;


|Subcategories |Detailed requirements |
|---|---|
|Supported input data modalities |* Video<br><br>* Audio<br><br>* Image (reference image)<br><br>* Text (Prompt) |
|Input format: video/audio |* Formats: mp4, mp3, wav, ogg, raw<br><br>* Size: The total duration of the video input must be between 1 second and 5 hours. Inputs shorter than 1 second will not be processed and will return an error message directly; the overall file size must not exceed 5GB. |
|Input format: image |Other: Effective only when ASR enhancement is not enabled (`enable_asr = false`). |
|Input path requirements |Provide operator input data via request parameters `video_url` and `reference_images`. Currently, two methods are supported: public URL and TOS path.<br><br><br>* Public URL: A URL accessible from the public network, format `http/https`.<br><br>   * Public URLs do not support addresses requiring login status or additional header authentication; temporary URLs must remain valid during task execution.<br><br>* TOS path: After uploading the data to be processed to a TOS Bucket under the same primary account and region as the current LAS service, you can provide the TOS path in the format `tos://bucket_name/demo`.<br><br>   * The TOS object must exist and have read permissions. |


<span id="output-requirements"></span>
## Output requirements

&nbsp;


|Subcategories |Detailed requirements |
|---|---|
|Output data modalities |* Video<br><br>* Text (`Poll` interface direct return) |
|Output path: TOS<br><br>(Video editing scenario) |In the video editing scenario, specify the storage path for the operator output result using the request parameter `output_tos_path`. Currently, TOS paths are supported.<br><br>TOS path: A TOS Bucket directory under the same primary account and region as the LAS service, with write permissions, format: `tos://bucket/output/`. |
|Output path: API<br><br>(Audio editing scenario) |In the audio editing scenario, after the operator completes processing, the edited result will be returned directly via the `Poll` interface's return parameter. |


<span id="billing-description"></span>
# Billing description


* Billing standards

&nbsp;

   
   |Component |Billing standard description |
   |---|---|
   |Billing item |Duration of the input source file. |
   |Billing type |Usage\-based billing, unit: `USD/minute`, billed hourly based on actual usage. Billing precision: rounded down to the nearest second |
   |Unit price |The unit price depends on the selected intelligent editing scenario. Different editing scenarios and modes have different unit prices. |
   

* Billing details

   Billing formula: `Total cost = unit price * usage`

&nbsp;

   
   |Scenario breakdown |Unit price |
   |---|---|
   |Video editing in `simple` mode<br><br>That is, the request parameter is set to `mode = simple` |0.21 USD/minute |
   |Video editing in `detail` mode<br><br>That is, the request parameter is set to `mode = detail` |0.29 USD/minute |
   |Audio\-only editing<br><br>That is, the request does not specify the `mode` parameter and `enable_asr = true` |0.07 USD/minute |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">说明   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the audio\-only editing scenario, after invoking the operator, the billing details will display the billing item as "video editing \- simple mode". The difference in the displayed billing item does not affect the actual cost calculation and settlement.   </div>
   

<span id="caution-and-prerequisites"></span>
# Caution and prerequisites

&nbsp;


|Details |Caution and prerequisites |
|---|---|
|Costs |Before calling an operator, you need to understand the model invocation costs associated with using the operator. For details, see [Large model invocation billing- BytePlus](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |


<span id="rest-api-call"></span>
# REST API call

<span id="api-call-instructions"></span>
## API call instructions


* This operator's API is an asynchronous task interface. Submit a task through the `Submit` interface to obtain the `task_id`. Then use the `Poll` interface to check the status of the corresponding task (`task_id`) and retrieve the operator's processing result.

* Caution: After a task is submitted, the `task_id` is valid for 3 days. After 3 days, the `task_id` cannot be used to retrieve the operator's processing result.


<span id="submit"></span>
## submit

<span id="interface-description"></span>
### Interface description

Submit processing tasks by invoking the intelligent video editing operator, supporting intelligent analysis of public network, BytePlus intranet, or TOS source files, and returning edited video segments or segment analysis results based on audio semantics.

<span id="request-parameters"></span>
### Request parameters



**operator_id** <span data-label="purple">string</span> <span data-api-tag="require|gcbzDE">必选</span> `Example value: las_video_edit`

Operator ID



**operator_version** <span data-label="purple">string</span> <span data-api-tag="require|W8v0ee">必选</span> `Example value: v1`

Operator version



**data** <span data-label="purple">VideoEditUserReqParams</span> <span data-api-tag="require|NCnZFA">必选</span>

Video editing request parameters


**video_url** <span data-label="purple">list of string</span> <span data-api-tag="require|EisPM5">必选</span> `Example value: https://example.com/video.mp4`

Downloadable address of the source file. Supports http/https and BytePlus TOS (tos://bucket/key). The source file must be accessible; the total duration of the video must be between 1 second and 5 hours, and the file size must not exceed 5GB. When only returning timeline annotations based on audio semantics, mp3, wav, ogg, and raw audio files are supported.



**task_name** <span data-label="purple">string</span> `Example value: MOVIE_HIGHLIGHT_EXTRACTION`

Built\-in common scenario names; at least one of task_description or this must be provided. When both are provided, task_description takes precedence and task_name is ignored. Optional values for task_name include:


* MOVIE_HIGHLIGHT_EXTRACTION: Extract highlights from movies and TV shows.

* HIGHLIGHT_CLIP_EXTRACTION: Extract general highlight clips.

* PRODUCT_HIGHLIGHT_DETECTION: Extract product highlight clips from promotional videos.

* SHORT_DRAMA_HIGHLIGHT_EXTRACTION: Sequential highlight extraction for short dramas, suitable for vertical short drama scenarios. It is recommended to use with `enable_asr=true`.

* SINGLE_SPEAKER_ORAL: Single\-speaker oral content, suitable for monologues, single\-person explanations to camera, single\-person product introductions, and similar oral materials. Must be used with `enable_asr=true` and without `mode`.

* DUAL_SPEAKER_ORAL: Dual\-speaker oral/interview, suitable for two\-person interviews, conversations, Q&A interactions, and similar oral materials. Must be used with `enable_asr=true` and without `mode`.



**task_description** <span data-label="purple">string</span> `Example value: Extract all segments of the Nick character, including lines.`

A clear natural language description of the editing requirements; at least one of task_name or this must be provided.

In audio editing scenarios, you can specify your own audio annotation label system in task_description. Example script:

This is a two\-person talk show. Please use the following labels:


* INSIGHT: Expression of unique insights;

* QUESTION: Asking good questions;

* STORY: Telling a story or case;

* FILLER: Transitional or filler speech with no information;

* REPEAT: Repeated expressions;Label each segment with the most appropriate tag.



**reference_images** <span data-label="purple">list of ReferenceImage</span>

Reference image list (supports URL or TOS address), used to assist in identifying specified characters, objects, and so on. The structure is `[{"target":"Reference object name","images":["image address"]}]`; Only effective when ASR enhancement is not enabled; if reference image download fails, returns `ReferenceImage.DownloadFailed`.


**target** <span data-label="purple">string</span> <span data-api-tag="require|0Nk6Zl">必选</span> `Example value: nick`

Reference object name



**images** <span data-label="purple">list of string</span> <span data-api-tag="require|yjt6LD">必选</span> `Example value: ["tos://path/to/image.jpg"]`

Reference object image address; supports http/https/tos:// protocol




**output_tos_path** <span data-label="purple">string</span>

Directory in TOS for saving video clips, format: tos://bucket/path. The TOS credentials used for the request must have write permissions for this directory; if the bucket does not exist, the path is inaccessible, region configuration is inconsistent, or permissions are insufficient, Tos.AccessFailed will be returned.

The scenario for video editing must be specified; for audio editing scenarios (when `mode` is not provided and `enable_asr=true`), configuration is not required.



**mode** <span data-label="purple">string</span> `Example value: simple`

Configuration is required for video editing scenarios to explicitly specify the video editing processing mode. Optional values include:


* **simple**: High speed, low cost



**detail**: High quality, higher cost, suitable for extracting segments from sports scenarios.

`mode` and `enable_asr` parameter configurations determine whether the current editing task is video editing or audio editing.



&nbsp;

* When the `mode` parameter is provided: indicates a video editing task, and the input source file will be processed for video editing output. Only the detail mode supports enabling ASR enhancement. If `mode=simple` and `enable_asr=true`, `Parameter.Invalid` is returned.

* If `mode` is not provided and ASR enhancement is not enabled (`enable_asr=false`): indicates it is still a video editing task, and video editing will be processed in `simple` mode;

* If `mode` is not provided and ASR enhancement is enabled (`enable_asr=true`): indicates an audio editing task, returns segment analysis results based on audio semantics, does not use video frame information, and does not generate video segments.



**enable_asr** <span data-label="purple">boolean</span> `Example value: true`

Whether to introduce ASR for semantic understanding enhancement. Applicable to videos with rich dialogue content and no subtitles, and scenarios requiring smooth boundaries for video segments. It is recommended that the video duration be within 1 hour.


* `false`: ASR is not enabled, the dialogue field is not returned



`true`: ASR is enabled.

`enable_asr` and `mode` parameter configurations determine whether the current editing task is video editing or audio editing. For details, refer to the above `mode` parameter description.




**min_clip_duration** <span data-label="purple">integer</span> `Example value: 5`

Filtering rule for editing results in video editing scenarios: video segments shorter than this duration will be filtered out.


* Unit: seconds. Valid range: 1–1800 seconds. Default is 1 second.



Setting a value that is too large may result in empty results. If no segments meet the criteria after filtering, the task returns COMPLETED with clips=[], total_segments=0.

For audio editing scenarios (when `mode` is not provided and `enable_asr=true`), configuration is not required. If configured, parameter validity will be checked, but it will not take effect in practice.




**max_clip_duration** <span data-label="purple">integer</span> `Example value: 60`

Filtering rule for editing results in video editing scenarios: video segments longer than this duration will be filtered out.


* Unit: seconds. Valid range: 1–1800 seconds. 0 means no limit. Default is 0.

* Setting a value that is too short may cause content fragmentation.

* When max_clip_duration \> 0, max_clip_duration \>= min_clip_duration must be satisfied; otherwise, the error code Parameter.Invalid is returned.



max_clip_duration cannot exceed the duration of the input video.

For audio clipping scenarios (when `mode` is not specified and `enable_asr=true`), configuration is not required. If configured, parameter validity will be checked, but the configuration will not take effect.




**max_clip_count** <span data-label="purple">integer</span> `Example value: 10`

Filtering rules for clipping results in video clipping scenarios. This specifies the maximum number of highlight segments to return. The model will attempt to return the number of video segments according to this requirement.


* Valid range: 1–50. 0 means no limit. The default is 0.



Setting this value too high may result in a large number of low\-quality segments being returned.

For audio clipping scenarios (when `mode` is not specified and `enable_asr=true`), configuration is not required. If configured, parameter validity will be checked, but the configuration will not take effect.




**extra_config** <span data-label="purple">ExtraConfig</span> `Example value: See example below`

Additional editing configuration. Currently, miniseries three\-element rendering and highlight intro features are supported. Available only when `mode=detail` and `enable_asr=true`. If these conditions are not met, `Parameter.Invalid` is returned. `miniseries_elements` and `preset_intro` can be provided at the same time. If both are provided and a highlight intro is generated, the intro segment will be concatenated before the main segment, and the miniseries three elements will be rendered.


**miniseries_elements** <span data-label="purple">MiniseriesElements</span>

Miniseries three\-element configuration, suitable for vertical miniseries scenarios. The rendering effect includes the title, hint, and badge. Only `title`, `hint`, and `template_name` fields are supported.


**title** <span data-label="purple">string</span> <span data-api-tag="require|dnX4D4">必选</span> `Example value: 《错换千金：冰山机长将我宠上天》`

Miniseries name, displayed centered at the top of the video



**hint** <span data-label="purple">string</span> <span data-api-tag="require|cwdP4g">必选</span> `Example value: 影视效果 请勿模仿`

Hint, displayed vertically on the left or right according to the template



**template_name** <span data-label="purple">string</span> <span data-api-tag="require|T73OR6">必选</span> `Example value: 模板1`

Template name, optional values:


* **模板1**: Title centered at the top + hint vertically on the left + badge "Popular Miniseries" at the top right

* **模板2**: Title centered at the top + hint vertically on the right + badge "Now Airing" at the top right

* **模板3**: Title centered at the top + hint vertically on the left + badge "Recommended Hit" at the top rightIf another value is provided, `Parameter.Invalid` is returned.




**preset_intro** <span data-label="purple">PresetIntro</span>

Highlight intro configuration. Passing a `preset_intro` object enables this feature. The system will select a 10–15 second attractive segment from those that meet the `task_description` requirements and place it at the beginning to quickly engage users. Whether a highlight intro is actually generated is determined by the `preset_start_time`, `preset_end_time`, and `preset_duration` fields in the returned result.


**transition** <span data-label="purple">string</span> `Example value: fade`

Transition type between the pre\-roll and the main video. Optional values:


* `none`: No transition, direct concatenation. transition_duration is not effective.

* `fade`: Fade in and out, used together with transition_duration.



**transition_duration** <span data-label="purple">float</span> `Example value: 0.5`

Transition duration (seconds), recommended: 0.5





**output_format** <span data-label="purple">string</span> `Example value: mp4`

The output video format in the video editing scenario. Currently, only mp4 output is supported. If not specified, mp4 is used by default.

In the audio editing scenario (when `mode` is not specified and `enable_asr=true`), video files are currently not generated, so this parameter can be ignored.




&nbsp;

<span id="response-parameters"></span>
### Response parameters


**metadata** <span data-label="purple">metadata</span>

Request metadata


**task_id** <span data-label="purple">string</span> `Example value: task-xxx`

Task ID in asynchronous mode, used for job status queries.



**task_status** <span data-label="purple">string</span> `Example value: PENDING`

Task status in asynchronous mode.


* PENDING, request received

* RUNNING, in progress

* COMPLETED, completed

* FAILED, failed

* TIMEOUT, timed out



**business_code** <span data-label="purple">string</span> `Example value: 0`

Business code.



**error_msg** <span data-label="purple">string</span>

If an exception occurs, detailed exception information will be returned.



&nbsp;

<span id="request-example"></span>
### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_video_edit",
    "operator_version": "v1",
    "data": {
        "video_url": ["https://${LAS_TOS_BUCKET}.${TOS_ENDPOINT}/operator_cards_serving/public/${LAS_ENVIRONMENT}/shared_video_dataset/A_Quiet_Place_movie_clip.mp4"],
        "task_description": "Extract all the clips of the little boy in the hat, including the lines",
        "output_tos_path": "$OUTPUT_TOS_PATH",
        "mode": "detail",
        "enable_asr": true
    }
}'
```


<span id="response-example"></span>
### Response example

```JSON
{
    "metadata": {
        "task_id": "task-20251125163544-abc123",
        "task_status": "PENDING",
        "business_code": "0",
        "error_msg": ""
    }
}
```


<span id="error-code"></span>
### Error code

&nbsp;


|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Url.Invalid |The url is invalid. |The video URL is invalid. |
|400 |Video.Invalid |The video file is invalid. |The video file is invalid. |
|400 |Video.DurationExceeded |Video duration exceeds maximum limit of 5 hours. |The duration of a single video or the total duration of multiple videos exceeds the maximum limit. |
|400 |Video.FileTooLarge |Video file size exceeds maximum limit of 5GB. |The video file size exceeds the limit. |
|400 |Parameter.Invalid |The parameter is invalid. |Parameter is invalid |
|401 |Authorization.Missing |Missing Authorization. |Missing authorization |
|401 |ApiKey.InValid |The api key is invalid. |API is invalid |
|400 |Video.DurationTooShort |Video duration is too short, minimum 1 second required. |The video duration is too short. |
|400 |Video.Timeout |Video processing timeout. |Video processing timeout |
|500 |Internal.ServerError |Internal server error. |Internal server error |


<span id="poll"></span>
## Poll

<span id="interface-description-1"></span>
### Interface description

Query the execution status and result of the video editing task.

<span id="request-parameters-1"></span>
### Request parameters



**operator_id** <span data-label="purple">string</span> <span data-api-tag="require|xxxGLy">必选</span> `Example value: las_video_edit`

Operator ID



**operator_version** <span data-label="purple">string</span> <span data-api-tag="require|ahLRDF">必选</span> `Example value: v1`

Operator version



**task_id** <span data-label="purple">string</span> <span data-api-tag="require|zKTl3o">必选</span> `Example value: task-xxx`

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


* PENDING, task submitted and queued

* RUNNING, running

* COMPLETED, completed

* FAILED, failed

* TIMEOUT, timed out



**submit_time** <span data-label="purple">string</span> `Example value: 2026-07-21T16:04:06+08:00`

Task submission time, in ISO 8601 timestamp format.



**end_time** <span data-label="purple">string</span> `Example value: 2026-07-21T16:04:06+08:00`

Task end time, in ISO 8601 timestamp format.



**business_code** <span data-label="purple">string</span> `Example value: 0`

Business code.



**error_msg** <span data-label="purple">string</span>

If an exception occurs, detailed exception information will be returned.




**data** <span data-label="purple">VideoEditResponse</span>

Task result data. Only when task_status=COMPLETED and business_code=0 is it the final VideoEditResponse; for PENDING/RUNNING/FAILED/TIMEOUT, a placeholder empty structure may be returned, such as {"video_duration":0.0,"total_segments":0,"clips":[],"resolution":""}. This structure does not indicate that there are no matching segments in the final result. In case of failure or timeout, check metadata.business_code and metadata.error_msg for the reason.


**total_segments** <span data-label="purple">integer</span> `Example value: 8`

The total number of segments that actually meet the requirements in this response.



**clips** <span data-label="purple">list of VideoClipInfo</span>

Segment list. In the video editing scenario, returns the edited video segments; when only timeline annotation based on audio semantics is performed, currently supports returning all voice timeline segments.


**clip_id** <span data-label="purple">string</span> `Example value: clip_001`

Unique identifier for the segment.



**source_id** <span data-label="purple">string</span> `Example value: source_001`

The unique identifier of the input video to which the current segment belongs.



**start_time** <span data-label="purple">string</span> `Example value: 00:02:05.000`

Segment start time (HH:MM:SS.mmm format).



**end_time** <span data-label="purple">string</span> `Example value: 00:02:14.500`

Segment end time (HH:MM:SS.mmm format).



**duration** <span data-label="purple">float</span> `Example value: 9.5`

Segment duration (seconds).



**description** <span data-label="purple">string</span> `Example value: Dialogue between Nick and Judy at the police station`

Segment description information. May be empty when only timeline annotation based on audio semantics is performed.



**dialogue** <span data-label="purple">string</span> `Example value: Do you need help?`

Segment dialogue content, from the ASR recognition result within the segment. Returned only when enable_asr is enabled and there is ASR content in the segment.



**clip_url** <span data-label="purple">string</span> `Example value: tos://bucket/path/clip_001.mp4`

TOS URI of the edited segment. When only timeline annotation based on audio semantics is performed, video segments are currently not generated and this field is not returned.



**file_size** <span data-label="purple">integer</span> `Example value: 1993083`

Segment file size (bytes). When only timeline annotation based on audio semantics is performed, video segments are currently not generated and this field is not returned.



**confidence** <span data-label="purple">float</span> `Example value: 1.0`

Confidence score (0.0\-1.0), indicating the model's confidence that the segment meets the requirements.



**meta** <span data-label="purple">object</span> `Example value: {"scene_type": "indoor"}`

Custom metadata, used to store additional information requested by the user via task_description; when only timeline annotation based on audio semantics is performed, semantic tag information such as speaker, label, and label_reason can also be returned.

The supported values for the label field returned in preset voice\-over task scenarios include:


* KEEP: Indicates that the current segment is a valid utterance.

* REPEAT: The same sentence was repeated.

* CORRECTION: Slip of the tongue or self\-correction.

* FILLER: Filler words (for example: um, uh, well, you know, and so on).

* NOISE: Environmental noise or off\-screen sound.



**preset_start_time** <span data-label="purple">string</span> `Example value: 00:02:09.000`

Preset segment start time (HH:MM:SS.mmm format). Value is only present if there is an actual preset segment.



**preset_end_time** <span data-label="purple">string</span> `Example value: 00:02:21.000`

Preset segment end time (HH:MM:SS.mmm format). Value is only present if there is an actual preset segment.



**preset_duration** <span data-label="purple">float</span> `Example value: 12`

Preset segment duration (seconds). Value is only present if there is an actual preset segment.



**preset_description** <span data-label="purple">string</span> `Example value: -`

Preset segment content description. Value is only present if there is an actual preset segment.




**videos** <span data-label="purple">list of VideoSourceInfo</span>

Input video list and processing result information. In multi\-input scenarios, this can be used to view the processing status, basic properties, and statistics of identified segments for each source video.


**episode** <span data-label="purple">integer</span> `Example value: 1`

Video sequence number.



**source_id** <span data-label="purple">string</span> `Example value: source_001`

Unique identifier for the input video.



**source_index** <span data-label="purple">integer</span> `Example value: 0`

Index position of the input video in the request list, starting from 0.



**video_url** <span data-label="purple">string</span> `Example value: https://example.com/video.mp4`

Input video URL.



**media_type** <span data-label="purple">string</span> `Example value: video`

Media type, currently always `video`.



**status** <span data-label="purple">string</span> `Example value: SUCCEEDED`

Processing status of the current video. Enumeration values:`SUCCEEDED` (processing succeeded), `FAILED` (processing failed).



**file_size** <span data-label="purple">integer</span> `Example value: 58499535`

Input video file size (bytes).



**duration** <span data-label="purple">float</span> `Example value: 482.482`

Input video duration (seconds).



**resolution** <span data-label="purple">string</span> `Example value: 1280x720`

Input video resolution.



**candidate_clip_count** <span data-label="purple">integer</span> `Example value: 2`

Number of candidate segments for the current video.



**selected_clip_count** <span data-label="purple">integer</span> `Example value: 2`

Number of final selected segments for the current video.



**business_code** <span data-label="purple">string</span> `Example value: null`

Business code corresponding to the processing of the current video; may be empty if successful.



**error_msg** <span data-label="purple">string</span> `Example value: null`

Error message when processing the current video fails; empty if successful.




**video_duration** <span data-label="purple">float</span> `Example value: 300.09`

Original source file duration (seconds).



**resolution** <span data-label="purple">string</span> `Example value: 1920x800`

Original video resolution (such as "1920x1080"). This field is not returned when only audio semantics are used.




&nbsp;

<span id="request-example-1"></span>
### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_video_edit",
    "operator_version": "v1",
    "task_id": "task-20251125163544-abc123"
}'
```


<span id="response-example-1"></span>
### Response example

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
        "total_segments": 8,
        "videos": [
            {
                "episode": 1,
                "source_id": "source_001",
                "source_index": 0,
                "video_url": "https://example.com/video.mp4",
                "media_type": "video",
                "status": "SUCCEEDED",
                "file_size": 58499535,
                "duration": 482.482,
                "resolution": "1280x720",
                "candidate_clip_count": 2,
                "selected_clip_count": 2,
                "business_code": null,
                "error_msg": null
            }
        ],
        "clips": [
            {
                "clip_id": "clip_001",
                "source_id": "source_001",
                "start_time": "00:02:05.000",
                "end_time": "00:02:14.500",
                "duration": 9.5,
                "description": "A young boy wearing a hat appears behind the counter, with subtitles displayed at the bottom of the screen. The boy wearing a hat is sitting on the floor next to the shelf.",
                "dialogue": "Tak apa",
                "clip_url": "tos://${LAS_TOS_BUCKET}/operator_cards_serving/public/${LAS_ENVIRONMENT}/las_video_edit/v1/clip_001.mp4",
                "file_size": 1993083,
                "confidence": 1.0,
                "meta": null
            },
            {
                "clip_id": "clip_002",
                "source_id": "source_001",
                "start_time": "00:02:27.000",
                "end_time": "00:02:30.500",
                "duration": 3.5,
                "description": "The boy wearing a hat is sitting on the floor next to the shelf, facing the left side of the screen.",
                "clip_url": "tos://${LAS_TOS_BUCKET}/operator_cards_serving/public/${LAS_ENVIRONMENT}/las_video_edit/v1/clip_002.mp4",
                "file_size": 419782,
                "confidence": 1.0,
                "meta": null
            },
            {
                "clip_id": "clip_003",
                "source_id": "source_001",
                "start_time": "00:02:52.000",
                "end_time": "00:03:17.500",
                "duration": 25.5,
                "description": "A woman walks toward the boy wearing a hat who is sitting on the floor, interacts with him, feeds him, and touches his hat. The boy wearing a patterned knit hat is sitting against the wall, a woman hands him a water bottle, he takes the bottle and drinks, then starts to speak.",
                "clip_url": "tos://${LAS_TOS_BUCKET}/operator_cards_serving/public/${LAS_ENVIRONMENT}/las_video_edit/v1/clip_003.mp4",
                "file_size": 4616337,
                "confidence": 1.0,
                "meta": null
            },
            {
                "clip_id": "clip_004",
                "source_id": "source_001",
                "start_time": "00:03:26.000",
                "end_time": "00:03:51.500",
                "duration": 25.5,
                "description": "The boy wearing a dark hat is on the supermarket floor, squatting and playing interactively with another girl, making a gesture similar to launching a rocket.",
                "dialogue": "Roket",
                "clip_url": "tos://${LAS_TOS_BUCKET}/operator_cards_serving/public/${LAS_ENVIRONMENT}/las_video_edit/v1/clip_004.mp4",
                "file_size": 5612855,
                "confidence": 1.0,
                "meta": null
            },
            {
                "clip_id": "clip_005",
                "source_id": "source_001",
                "start_time": "00:03:56.000",
                "end_time": "00:04:02.500",
                "duration": 6.5,
                "description": "The boy wearing a red-and-white striped knit hat speaks, expressing the idea of leaving this planet. The boy with the hat stands in front of the shelf, delivers his line, and raises one finger.",
                "dialogue": "Itulah caranya..... Kita pergi dari Planet ini",
                "clip_url": "tos://${LAS_TOS_BUCKET}/operator_cards_serving/public/${LAS_ENVIRONMENT}/las_video_edit/v1/clip_005.mp4",
                "file_size": 1037987,
                "confidence": 1.0,
                "meta": null
            },
            {
                "clip_id": "clip_006",
                "source_id": "source_001",
                "start_time": "00:04:09.000",
                "end_time": "00:04:11.500",
                "duration": 2.5,
                "description": "The boy with the hat smiles, then starts running and leaves the frame.",
                "clip_url": "tos://${LAS_TOS_BUCKET}/operator_cards_serving/public/${LAS_ENVIRONMENT}/las_video_edit/v1/clip_006.mp4",
                "file_size": 456489,
                "confidence": 1.0,
                "meta": null
            },
            {
                "clip_id": "clip_007",
                "source_id": "source_001",
                "start_time": "00:04:31.000",
                "end_time": "00:04:41.500",
                "duration": 10.5,
                "description": "The boy with the hat steps onto a box to climb next to the shelf and reaches for an item on the shelf.",
                "clip_url": "tos://${LAS_TOS_BUCKET}/operator_cards_serving/public/${LAS_ENVIRONMENT}/las_video_edit/v1/clip_007.mp4",
                "file_size": 2120459,
                "confidence": 1.0,
                "meta": null
            },
            {
                "clip_id": "clip_008",
                "source_id": "source_001",
                "start_time": "00:04:46.000",
                "end_time": "00:04:58.500",
                "duration": 12.5,
                "description": "The boy with the hat stands next to the girl, the girl looks at him, and then the boy reaches for an item on the shelf.",
                "clip_url": "tos://${LAS_TOS_BUCKET}/operator_cards_serving/public/${LAS_ENVIRONMENT}/las_video_edit/v1/clip_008.mp4",
                "file_size": 2910307,
                "confidence": 0.95,
                "meta": null
            }
        ],
        "video_duration": 300.091458,
        "resolution": "1920x800"
    }
}
```


<span id="error-code-1"></span>
### Error code

&nbsp;


|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |Invalid parameter. |Parameter is invalid |
|400 |Parameter.Missing |Missing required parameter. |Missing required parameter |
|400 |Url.Invalid |Invalid URL. |URL is invalid |
|400 |Video.Invalid |Invalid video file. |Video file is invalid |
|400 |Video.DownloadFailed |Video download failed. |Video download failed |
|400 |Video.FormatUnsupported |Video format not supported. |Video format not supported |
|400 |Video.Timeout |Video processing timeout. |Video processing timeout |
|400 |Video.VLMFailed |VLM call failed. |VLM call failed |
|400 |Video.UploadFailed |Video upload failed. |Video upload failed |
|400 |Video.DurationTooShort |Video duration too short. |Video duration is too short |
|400 |Video.FrameExtractionFailed |Frame extraction failed. |Frame extraction failed |
|400 |Tos.AccessFailed |TOS access failed. |TOS access failed |
|400 |ReferenceImage.DownloadFailed |Reference image download failed. |Reference image download failed |
|401 |Authorization.Missing |Missing Authorization. |Missing authorization |
|401 |ApiKey.InValid |The api key is invalid. |API is invalid |
|400 |Task.NotFound |Task not found. |Task does not exist |
|500 |Internal.ServerError |Internal server error. |Internal server error |
