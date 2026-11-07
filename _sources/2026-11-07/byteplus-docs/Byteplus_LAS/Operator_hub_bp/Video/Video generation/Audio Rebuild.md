---
title: "Audio Rebuild"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/audio-rebuild"
---

The Audio Rebuild operator supports both consistent assembly of multiple AI\-generated clips and audio\-only generation from an authoritative script. In video mode, it concatenates visuals in `segments` order, replans a full\-length audio timeline, generates unified audio, and replaces the source audio track. In audio\-only mode, it directly generates voiceover audio. Results include the output mode, composed video or audio, standalone rebuilt audio, and SRT subtitles.

<span id="operator-introduction"></span>
# Operator introduction

> Operator ID: `las_video_merge_audio_rebuild`


<span id="application-scenarios"></span>
## Application scenarios


* **Unified assembly of AI\-generated clips**: Connect upstream storyboards or video\-generation outputs and standardize narration, voice style, audio atmosphere, and subtitles across clips.

* **Authoritative\-copy voiceover**: When final narration copy already exists, bypass source\-audio content organization and generate a controllable voiceover directly from the script.

* **Video\-free audio production**: Generate natural\-duration or target\-duration audio from an authoritative script alone.

* **Segment\-prompt\-driven production**: When only source audio and generation prompts are available, use source audio as the content basis and prompts for correction or explicit\-line extraction.

* **Product explainers, marketing, and tutorials**: Turn multiple product shots, demonstrations, or marketing scenes into a complete video with unified audio and subtitles.


<span id="core-capabilities"></span>
## Core capabilities


* **Ordered multi\-clip merge**: Concatenates video clips in request order to form a single video.

* **Authoritative script passthrough**: Strictly uses `voiceover_script` as the only spoken content when provided, without consuming clip audio or semantically rewriting or expanding the script.

* **Audio\-only voiceover generation**: Generates audio without videos, using either an explicit `target_duration` or the model's natural duration.

* **Per\-clip prompt\-guided correction**: `prompt` is the prompt used to generate an individual video clip. Without a full\-video script, it can correct proper nouns and pronunciations in the clip audio to help ensure accurate pronunciation.

* **Safe explicit\-line extraction**: When no speech is recognized, extracts only explicitly marked dialogue, spoken copy, or narration from `prompt` and filters out action, subtitle, lip\-sync, and visual instructions. It does not fabricate speech when no explicit spoken content exists.

* **Cross\-clip audio consistency**: Reconciles speakers and audio styles across clips, plans a continuous timeline, and routes content into speech, sound, or silence to improve consistency across the final video.

* **Automatic audio generation and assembly**: Automatically chooses full\-track, layered, or chunked generation based on duration and timeline complexity. Voice, delivery, BGM, sound\-effect, and mixing cues in prompts can guide the newly generated track, but source BGM and effects are not preserved.

* **Speech\-density control**: For a full\-video script, checks whether the copy fits the available duration to avoid overly dense narration.

* **Controllable output storage**: Writes final artifacts to a caller\-selected TOS directory and returns original object paths so access URLs can be regenerated after expiration.

* **Multiple outputs**: Returns the output mode, composed video or audio\-only result, standalone audio, SRT subtitles, target duration, and rebuilt\-audio duration.


<span id="effect-display"></span>
## Effect display


---



<div style="text-align: center">
AI\-generated clips assembled with rebuilt English audio</div>



<columns>
<columnsItem zoneid="Gh2dFatEGM">

* Input videos

   * clip_01

      <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3491faa1c0e44fd4a115cb673fb50f83~tplv-goo7wpa0wc-image.image" controls></video>
      

   * clip_02

      <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5595fd9c800491bbf4308379f227564~tplv-goo7wpa0wc-image.image" controls></video>
      

</columnsItem>
<columnsItem zoneid="jceqNiWDNR">

* Task example – core parameters

   This example joins two 15.07\-second AI\-generated clips depicting the poet Xin Qiji and replaces their original audio with one continuous English soundtrack. The rebuilt track uses a weathered elderly male voice, follows the clip order, recites an English rendering of the selected verse, and adds restrained traditional Chinese instrumental music that matches the historical setting.

   ```json
   {
     "data": {
       "segments": [
         {
           "clip_id": "scene_001",
           "video_url": "https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3491faa1c0e44fd4a115cb673fb50f83~tplv-goo7wpa0wc-image.image"
         },
         {
           "clip_id": "scene_002",
           "video_url": "https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5595fd9c800491bbf4308379f227564~tplv-goo7wpa0wc-image.image"
         }
       ],
       "audio_prompt": "Rebuild the complete soundtrack in English. Use one consistent elderly male voice with a weathered, reflective tone that gradually becomes resolute and martial. Recite only these English lines, in this order: Drunk, I trim the lamp and gaze at my sword; in dreams, bugles sound across the barracks. Roast beef is shared among the troops; martial music rings beyond the frontier as soldiers muster for the autumn campaign. Pace the narration naturally across the two clips. Add restrained traditional Chinese instrumental background music that supports the historical atmosphere without overpowering the voice. All spoken content must be in English. Do not speak Chinese.",
       "scene_mode": "voiceover",
       "output_object_storage_dir": "tos://las-doctest-bp/las-ai/output/las_video_merge_audio_rebuild/english_xin_qiji/"
     }
   }
   ```
   

</columnsItem>
<columnsItem zoneid="zzob1DcfhM">

* Output example

   <video src="https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/53092cab-654d-4ef8-bfe2-c199b5418424.mp4" controls></video>
   


<div style="text-align: right">
The operator merges the clips in input order, rebuilds the complete audio track from the English audio prompt, and replaces the source audio. The video imagery is not edited.</div>


</columnsItem>
</columns>



---



<span id="supported-regions"></span>
## Supported regions


* Asia Pacific(Johor)：ap\-southeast\-1


<span id="operator-performance"></span>
## Operator performance

&nbsp;


|Breakdown item |Performance impact |
|---|---|
|Submit RPM |5 |
|Poll RPM |300 |


<span id="input-and-output-requirements"></span>
# Input and output requirements

<span id="input-requirements"></span>
## Input requirements

&nbsp;


|Breakdown item |Detailed requirements |
|---|---|
|Supported input data modalities |* Video<br><br>* Text |
|Input format: Video |* Quantity: Without `audio_prompt` or `voiceover_script`, provide 1 to 200 clips. With either direct text parameter, videos are optional and up to 200 clips are supported.<br><br>* Total duration: No more than 1,800 seconds without a direct text parameter, or 110 seconds with one.<br><br>* Order: Clips are merged in the order in which they appear in `segments`. |
|Input format: Text |* Complete audio description: `audio_prompt` must not be blank after trimming and supports up to 2,500 characters.<br><br>* Voiceover script: `voiceover_script` must not be blank after trimming and supports up to 2,500 characters. `audio_prompt` and `voiceover_script` are mutually exclusive.<br><br>* Clip prompt: Each `segments[].prompt` supports up to 8,000 characters and has no effect when either direct text parameter is provided.<br><br>* Audio\-only request: A request with `audio_prompt` or `voiceover_script` and no videos can set `target_duration` within `(0, 110]` seconds. Do not use it with input videos or without a direct text parameter. |
|Input path requirements |Provide clips through `segments[].video_url`. Accessible `http://`, `https://`, and `tos://` addresses are supported. |


<span id="output-requirements"></span>
## Output requirements

&nbsp;


|Breakdown item |Detailed requirements |
|---|---|
|Supported output data modalities |* Video<br><br>* Audio<br><br>* Text (SRT subtitles) |
|Output format: Video |* Format: MP4. Video\-mode tasks return a composed video with the rebuilt audio track. Source dialogue, BGM, and sound effects are replaced rather than preserved.<br><br>* Scope: The operator does not reorder or edit video imagery and is not intended for lip\-synced dubbing or overlaying narration on preserved source dialogue. |
|Output format: Audio |Returns a standalone rebuilt\-audio artifact. Script\-only requests can return audio without video. |
|Output format: Text |Format: SRT subtitle file. |
|Output path requirements |`output_object_storage_dir` is optional. A non\-empty value must be a writable `tos://` directory of no more than 4,096 characters. If omitted, the platform stores the output. Poll returns presigned artifact URLs valid for 24 hours; save the object paths when URLs must be regenerated later. |


<span id="billing-information"></span>
# Billing information


* Billing standards

&nbsp;

   
   |Breakdown item |Billing standard description |
   |---|---|
   |Billing item |Rebuilt\-audio duration returned in `total_duration_sec` by a successful Poll response. Text\-model tokens are not billed separately. |
   |Billing type |Usage\-based billing in `USD/minute`. |
   |Unit price |0.77 USD/minute. |
   


<span id="cautions-and-prerequisites"></span>
# Cautions and prerequisites

&nbsp;


|Details |Caution and prerequisites |
|---|---|
|Costs |Before calling an operator, you need to understand the model invocation costs associated with using the operator. For details, see [Large model billing](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |


<span id="rest-api-call"></span>
# Rest API call

<span id="submit"></span>
## Submit

<span id="interface-description"></span>
### Interface description

Submit an asynchronous Audio Rebuild task. The operator can merge videos in input order and rebuild unified audio, or generate audio directly from a complete audio description or a legacy voiceover script. A successful submission returns a task ID that can be used with the Poll API to query task status and results.

<span id="request-parameters"></span>
### Request parameters



**operator_id** <span data-label="purple">string</span> <span data-api-tag="require|n9SA0x">必选</span> `Example value: las_video_merge_audio_rebuild`

Operator ID



**operator_version** <span data-label="purple">string</span> <span data-api-tag="require|5fVtPu">必选</span> `Example value: v1`

Operator version



**data** <span data-label="purple">VideoMergeAudioRebuildRequest</span> <span data-api-tag="require|mSmJWX">必选</span>

Audio Rebuild request parameters


**segments** <span data-label="purple">list of Segment</span> `Optional`

Video clips merged in array order, up to 200 clips. At least one clip is required without `audio_prompt` or `voiceover_script`; the field may be omitted or empty for direct audio\-only requests. Total video duration is limited to 1,800 seconds without a direct parameter and 110 seconds with one


**clip_id** <span data-label="purple">string</span> `Optional` `Example value: scene_001`

Optional video clip ID, 1 to 64 characters. It may contain only ASCII letters, digits, underscores, and hyphens, and must start with a letter or digit. Explicit IDs must be unique within the request. When omitted or `null`, the service generates one from the input position



**video_url** <span data-label="purple">string</span> <span data-api-tag="require|3EtOi1">必选</span> `Example value: https://example.com/scene_001.mp4`

Video URL. Supports `http://`, `https://`, and `tos://` and must be accessible to the service



**prompt** <span data-label="purple">string</span> `Optional` `Example value: Product introduction video with a warm, natural voiceover`

Prompt used to generate this video clip. Without `audio_prompt` or `voiceover_script`, it can correct proper nouns and pronunciations in the clip audio to help ensure accurate pronunciation. It has no effect when either direct parameter is provided. Up to 8,000 characters




**audio_prompt** <span data-label="purple">string</span> `Optional` `Example value: Soft music underneath, with a warm, natural female voice saying: “Welcome to our new product.”`

Complete SeedAudio description. It must not be blank after trimming and supports up to 2,500 characters, including voice, BGM, ambience, and sound effects. The service adds only the target\-duration prefix; it does not parse or rewrite the content or apply speech\-density checks. When provided, the operator uses one `direct_audio_prompt` generation call. Mutually exclusive with `voiceover_script`



**voiceover_script** <span data-label="purple">string</span> `Optional` `Example value: Welcome to our new product, designed to make every use easier.`

Deprecated voice\-only compatibility parameter. It must not be blank after trimming and supports up to 2,500 characters. When provided, the operator uses one `direct_voiceover` generation call, does not transcribe clip audio, does not rewrite or expand the script, and ignores `segments[].prompt`. Mutually exclusive with `audio_prompt`



**target_duration** <span data-label="purple">float</span> `Optional` `Example value: 10`

Target duration in seconds for direct audio\-only output. Range: `(0, 110]`. It is valid only with `audio_prompt` or `voiceover_script` and without video segments; providing it with videos or without either direct parameter returns `Parameter.Invalid`. When omitted, the model determines the audio duration naturally



**output_object_storage_dir** <span data-label="purple">string</span> `Optional` `Example value: tos://bucket/output/audio-rebuild`

Optional custom TOS directory for final artifacts, up to 4,096 characters, formatted as `tos://bucket/path`. Omit it, pass `null`, or pass an empty string to use platform storage. When set to a non\-empty directory, artifacts are uploaded with caller\-side credentials and original object paths are returned by Poll



**scene_mode** <span data-label="purple">string</span> `Optional` `Example value: voiceover`

Compatibility field, up to 64 characters. Default: `voiceover`; v1 is applicable only to the voiceover scenario. If an input video is not voiceover content, the task does not fail for that reason, but generated audio may not align with lip movements



**voiceover** <span data-label="purple">Voiceover</span> `Optional`

Speech\-density configuration for the legacy `voiceover_script` path. Defaults are used when omitted; the `audio_prompt` path ignores this configuration


**enable_speech_density_check** <span data-label="purple">boolean</span> `Optional` `Example value: true`

Deprecated. Whether to check if the legacy `voiceover_script` fits the target duration. Default: `true`. The `audio_prompt` path ignores it



**max_speech_chars_per_sec** <span data-label="purple">float</span> `Optional` `Example value: 20`

Maximum readable characters per second. Range: `(0, 50]`; default: 20. It applies only when the legacy `voiceover_script` is provided and density checking is enabled. Audio\-only requests without a target duration use the 110\-second single\-call budget





&nbsp;

<span id="response-parameters"></span>
### Response parameters


**metadata** <span data-label="purple">Metadata</span>

Request metadata


**task_id** <span data-label="purple">string</span> `Example value: task-20260809120000-abc123`

Asynchronous task ID used for Poll queries



**task_status** <span data-label="purple">string</span> `Example value: PENDING`

Task status. A successful submission usually returns `PENDING`



**business_code** <span data-label="purple">string</span> `Example value: 0`

Standard LAS business code. `0` indicates successful submission



**error_msg** <span data-label="purple">string</span>

Error message. Empty on successful submission



**request_id** <span data-label="purple">string</span> `Example value: 20260809120000ABCDEF`

Request ID for log tracing and troubleshooting



&nbsp;

<span id="examples"></span>
### Examples

<span id="request-example"></span>
#### Request example

```bash
curl --location "${LAS_ENDPOINT}/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
  "operator_id": "las_video_merge_audio_rebuild",
  "operator_version": "v1",
  "data": {
    "segments": [
      {
        "clip_id": "scene_001",
        "video_url": "https://las-ai-ap-southeast-1-online-bp.tos-ap-southeast-1.bytepluses.com/operator_cards_serving/public/online/las_video_merge_audio_rebuild/v1/segments/scene_001.mp4",
        "prompt": "Product introduction video with a warm, natural voiceover"
      },
      {
        "video_url": "https://las-ai-ap-southeast-1-online-bp.tos-ap-southeast-1.bytepluses.com/operator_cards_serving/public/online/las_video_merge_audio_rebuild/v1/segments/scene_002.mp4"
      }
    ],
    "audio_prompt": "Soft music underneath, with a warm, natural female voice saying: Welcome to our new product, designed to make every use easier.",
    "scene_mode": "voiceover",
    "output_object_storage_dir": "tos://las-ai-ap-southeast-1-online-bp/audio-rebuild-output"
  }
}'
```


<span id="response-example"></span>
#### Response example

```json
{
  "metadata": {
    "task_id": "task-20260809120000-abc123",
    "task_status": "PENDING",
    "business_code": "0",
    "error_msg": "",
    "request_id": "20260809120000ABCDEF"
  }
}
```


<span id="error-codes"></span>
### Error codes

&nbsp;


|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |The parameter is invalid. |Invalid request parameters, including missing conditionally required fields, out\-of\-range values, invalid media or output\-directory formats, duplicate clip IDs, providing both `audio_prompt` and `voiceover_script`, an invalid `target_duration` dependency or conflict, and unknown fields |
|400 |Operator.InvalidId |The operator is invalid. |Invalid operator ID |
|400 |Operator.InvalidVersion |The operator version is invalid. |Invalid operator version |
|401 |Authorization.Missing |The authorization header is missing. |Missing authentication |
|401 |ApiKey.Invalid |The api key is invalid. |Invalid API Key |
|429 |Server.Busy |Server is Busy, please try again later. |Service busy or rate limited |
|500 |Server.InternalError |General Internal Error |Internal server error |


<span id="poll"></span>
## Poll

<span id="interface-description-1"></span>
### Interface description

Query the execution status and result of an Audio Rebuild task by task ID. Continue polling while the task is non\-terminal. When completed, the response contains the output mode and URLs for the composed video or audio\-only result, standalone audio, and subtitles.

<span id="request-parameters-1"></span>
### Request parameters



**operator_id** <span data-label="purple">string</span> <span data-api-tag="require|luBUCV">必选</span> `Example value: las_video_merge_audio_rebuild`

Operator ID



**operator_version** <span data-label="purple">string</span> <span data-api-tag="require|lk3Cxl">必选</span> `Example value: v1`

Operator version



**task_id** <span data-label="purple">string</span> <span data-api-tag="require|QnFo5g">必选</span> `Example value: task-20260809120000-abc123`

Asynchronous task ID returned by Submit



&nbsp;

<span id="response-parameters-1"></span>
### Response parameters



**metadata** <span data-label="purple">Metadata</span>

Task metadata


**task_id** <span data-label="purple">string</span> `Example value: task-20260809120000-abc123`

Asynchronous task ID



**task_status** <span data-label="purple">string</span> `Example value: COMPLETED`

Task status: `PENDING` (waiting), `RUNNING` (processing), `COMPLETED` (successful), `FAILED` (failed), `EXPIRED` (expired while waiting), `CANCELLED` (cancelled), or `TIMEOUT` (processing timed out)



**business_code** <span data-label="purple">string</span> `Example value: 0`

Standard LAS business code. `0` indicates success. Failed tasks return a standard caller\-facing error code



**error_msg** <span data-label="purple">string</span>

Error message. Empty on success; a caller\-safe failure reason is returned when the task fails



**request_id** <span data-label="purple">string</span> `Example value: 20260809120100ABCDEF`

Request ID for this Poll call, used for log tracing and troubleshooting



**submit_time** <span data-label="purple">string</span> `Example value: 2026-08-09T12:00:00+08:00`

Task submission time in ISO 8601 format



**end_time** <span data-label="purple">string</span> `Example value: 2026-08-09T12:01:00+08:00`

Task end time in ISO 8601 format; may be empty before the task ends




**data** <span data-label="purple">VideoMergeAudioRebuildResponse</span>

Task result. Complete fields are returned only when `task_status=COMPLETED`; the object may be empty for non\-terminal or failed states


**output_mode** <span data-label="purple">string</span> `Example value: video`

Output type: `video` for a composed video or `audio` for audio\-only output



**video_url** <span data-label="purple">string</span> `Example value: https://example.com/final_video.mp4`

TOS presigned URL of the composed video, valid for a fixed 24 hours; empty in audio\-only mode



**video_object_storage_path** <span data-label="purple">string</span> `Example value: tos://bucket/output/final_video.mp4`

Original TOS object path of the composed video. Returned only when Submit explicitly sets `output_object_storage_dir` and video is produced



**audio_url** <span data-label="purple">string</span> `Example value: https://example.com/rebuilt_audio.m4a`

TOS presigned URL of the standalone rebuilt audio, valid for a fixed 24 hours



**audio_object_storage_path** <span data-label="purple">string</span> `Example value: tos://bucket/output/rebuilt_audio.m4a`

Original TOS object path of the standalone audio. Returned only when Submit explicitly sets `output_object_storage_dir`



**subtitle_url** <span data-label="purple">string</span> `Example value: https://example.com/subtitle.srt`

TOS presigned URL of the SRT subtitles, valid for a fixed 24 hours; may be empty when there are no valid subtitles



**subtitle_object_storage_path** <span data-label="purple">string</span> `Example value: tos://bucket/output/subtitle.srt`

Original TOS object path of the subtitles. Returned only when Submit explicitly sets `output_object_storage_dir` and non\-empty subtitles are produced



**generation_mode** <span data-label="purple">string</span> `Example value: direct_audio_prompt`

Actual generation mode. It is `direct_audio_prompt` when `audio_prompt` is provided and `direct_voiceover` for the legacy `voiceover_script`; the current public default path without either direct parameter is `parallel_clip_mix`



**target_duration_sec** <span data-label="purple">float</span> `Example value: 24.313`

Target audio duration in seconds. For video output, this is the actual total video duration. For audio\-only output, it is the explicit `target_duration`; it is empty for natural\-duration audio\-only generation



**total_duration_sec** <span data-label="purple">float</span> `Example value: 24.313`

Total rebuilt\-audio duration in seconds and the billable duration for this task




&nbsp;

Presigned URLs cannot be downloaded after expiration. With a custom output directory, use the returned `*_object_storage_path` to generate a new access URL.

<span id="examples-1"></span>
### Examples

<span id="request-example-1"></span>
#### Request example

```bash
curl --location "${LAS_ENDPOINT}/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
  "operator_id": "las_video_merge_audio_rebuild",
  "operator_version": "v1",
  "task_id": "task-20260809120000-abc123"
}'
```


<span id="response-example-1"></span>
#### Response example

```json
{
  "metadata": {
    "task_id": "task-20260809120000-abc123",
    "task_status": "COMPLETED",
    "business_code": "0",
    "error_msg": "",
    "request_id": "20260809120100ABCDEF",
    "submit_time": "2026-08-09T12:00:00+08:00",
    "end_time": "2026-08-09T12:01:00+08:00"
  },
  "data": {
    "output_mode": "video",
    "video_url": "https://example.com/final_video.mp4",
    "video_object_storage_path": "tos://bucket/output/final_video.mp4",
    "audio_url": "https://example.com/rebuilt_audio.m4a",
    "audio_object_storage_path": "tos://bucket/output/rebuilt_audio.m4a",
    "subtitle_url": "https://example.com/subtitle.srt",
    "subtitle_object_storage_path": "tos://bucket/output/subtitle.srt",
    "generation_mode": "direct_audio_prompt",
    "target_duration_sec": 24.313,
    "total_duration_sec": 24.313
  }
}
```


<span id="error-codes-1"></span>
### Error codes

&nbsp;


|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |TaskId.Invalid |The task id is invalid. |The task ID is empty, the task does not exist, or the caller is not authorized to access it |
|400 |Operator.InvalidId |The operator is invalid. |Invalid operator ID |
|400 |Operator.InvalidVersion |The operator version is invalid. |Invalid operator version |
|401 |Authorization.Missing |The authorization header is missing. |Missing authentication |
|401 |ApiKey.Invalid |The api key is invalid. |Invalid API Key |
|429 |Server.Busy |Server is Busy, please try again later. |Service busy or rate limited |
|500 |Server.InternalError |General Internal Error |Task execution failure, incomplete result, or internal server error |
