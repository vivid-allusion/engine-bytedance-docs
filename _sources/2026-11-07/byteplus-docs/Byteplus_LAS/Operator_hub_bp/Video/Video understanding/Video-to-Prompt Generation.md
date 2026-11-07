---
title: "Video-to-Prompt Generation"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/video-to-prompt-generation"
---

The Video\-to\-Prompt Generation operator is designed for video recreation and storyboard\-based adaptation. It first extracts facts from the source video, then combines the time ranges and reference images in a storyboard bundle to produce an actionable prompt per segment. The recommended input is the `storyboard_bundle_url` returned by the Video Storyboard operator. Supply inline segments only when constructing or editing the storyboard yourself.

# Operator introduction

> Operator ID: `las_viral_reverse_prompt`

# Core capabilities

* Generates a prompt for each storyboard time window based on source\-video facts, preventing content from leaking across segments.

* Preserves verified subject identity, spatial relationships, key action order, verbatim dialogue, and audio delivery.

* Supports specifying a target visual style and voice timbre without changing the source\-video facts.

* Binds and returns reference images. Different references sharing a name receive readable suffixes synchronized with Prompt @mentions. The same reference reuses its name across segments.

* Returns the number of model requests, total token usage, and whether usage information is complete.

## Recommended: Use a storyboard bundle

Use the `storyboard_bundle_url` returned by the Video Storyboard operator. This value must be the complete, stable URI of `storyboard_bundle_manifest.json`; do not pass a directory or substitute `segments_url` or `shot_registry_url`. Model selection is optional and defaults to `pro`.

```json
{
  "storyboard_bundle_url": "tos://bucket/storyboard/storyboard_bundle_manifest.json",
  "source_video_url": "tos://bucket/source.mp4",
  "output_language": "en",
  "ark_api_key": "<YOUR_ARK_API_KEY>"
}
```

## Model selection

|`lite` |`standard` |`pro` |Verified `model_name` examples |
|---|---|---|---|
|`seed-2-0-lite-260428` |`dola-seed-2-1-turbo-260628` |`seed-2-0-pro-260328` |The three tier models plus `seed-2-0-mini-260428` |

Model selection affects only Stage 2 prompt generation. Stage 1 fact extraction always uses the Lite model configured for the current region. We recommend `model_tier`; to pin a revision, send a non\-empty `model_name`, which the service forwards to ModelArk unchanged. Do not pass both fields. The examples are not an admission allowlist; verify regional availability and ModelArk API\-key access before submitting.

## Prompt template selection

|prompt_profile |Use case |
|---|---|
|`general` |General video recreation and adaptation; use this template when unsure |
|`beauty` |Beauty, skincare, and personal\-care content, emphasizing product presentation, visible subject state, and application actions |
|`home_textile` |Home\-textile content, emphasizing fabric texture, structure, folds, and contact relationships |

The template changes only the industry\-specific emphasis of the output prompt. Subjects, scenes, actions, dialogue, and other facts still come from the source video and storyboard input.

## Effect display

* Example source video and storyboard information

   ```text
   Source video, 0–8 seconds: In a kitchen in the early morning, a silver coffee machine completes grinding and brewing; the shot pushes in from a medium shot to a close-up of the brewing outlet.
   ```

* Example prompt generated for the storyboard segment

   ```text
   [Task type]
   Recreate a product showcase segment in which a silver coffee machine completes grinding and brewing in a kitchen in the early morning.
   [Visual specifications]
   An 8-second product video that retains the warm morning light and realistic metallic texture.
   [Action sequence]
   Show the coffee machine in a medium shot as the camera slowly pushes in. Coffee beans enter the grinder, followed by a close-up of the brewing outlet that retains details of the steam and flowing coffee.
   ```

## Supported regions

* Asia Pacific (Johor): `ap-southeast-1`

## Operator performance

|Breakdown item |Detailed requirements |
|---|---|
|Submit RPM |200 |
|Poll RPM |300 |

# Input and output requirements

## Input requirements

|Breakdown item |Detailed requirements |
|---|---|
|Supported input data modalities |* Video<br><br>* Image<br><br>* Text |
|Input format: Video |\* Duration: The measured source\-video duration must be greater than 0 and at most 360 seconds. Inline storyboards support 1–24 ordered, non\-overlapping time windows; there is no separate 4–30\-second segment limit. |
|Input format: Image |\* There is no nine\-image cap per segment. Reference IDs must be unique within the segment and positions must be contiguous starting at 1. |
|Input format: Text |\* Size: The storyboard bundle manifest and each referenced JSON file must not exceed 2 MiB. |
|Input path requirements |Provide operator inputs through request parameters such as `source_video_url` and `storyboard_bundle_url`:<br><br><br>* **Public URL**: Use an accessible `http://` or `https://` URL, including a valid presigned URL. Preserve all signature parameters and keep the URL valid throughout processing; the service does not renew signatures.<br><br>* **TOS path**: Use a readable object in a TOS bucket under the same primary account and in the same region as the current LAS service. The calling account must have permission to read the object. Format: `tos://bucket/path/file`. |

## Output requirements

|Breakdown item |Detailed requirements |
|---|---|
|Supported output data modalities |\* Text |
|Output format: Text |Prompts are returned in input storyboard order, together with the reference images bound to each segment.<br><br><br>* Output language: `output_language` supports `zh` and `en` and defaults to `zh`. Original dialogue remains in its source language. |
|Output path requirements |No output storage path is required. After the task is complete, Poll returns results in `data.items`. |

## Operator pricing

Set a valid ModelArk API key when invoking this operator. Charges are based on actual model usage. For model prices, see [Model pricing](https://docs.byteplus.com/en/docs/modelark/model-pricing).

# Cautions and prerequisites

## Activate ModelArk

This operator invokes ModelArk models activated under your own account, and the corresponding charges appear on your ModelArk bill. Before using the operator, activate the required ModelArk models and obtain an `ark_api_key`. You can select the Stage 2 model by tier or specify a non\-empty exact model name that is forwarded to ModelArk unchanged.

## General cautions

|Details |Cautions and prerequisites |
|---|---|
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |

# Rest API call

## Submit

> **Note**

> Currently, only single\-task Submit is supported. Platform batch\-task APIs are not supported.

### Interface description

Submit an asynchronous video\-to\-prompt generation task. The request header uses a LAS API key for authentication, and the request body must include a valid Ark API key. Stage 1 always uses Lite for source\-video fact extraction; `model_tier` or `model_name` selects only the Stage 2 prompt\-generation model. A successful submission returns a task ID for Poll.

The recommended input is `data.storyboard_bundle_url` from the Video Storyboard operator's Poll result. It is the complete URI of a `storyboard_bundle_manifest.json` file, not a directory. The operator uses the manifest to load segments and their character, scene, prop, and reference\-image data.

For a first request, start with `storyboard_bundle_url`, then provide `source_video_url` and `ark_api_key`. `prompt_profile` selects the Prompt template and defaults to the general template.

When a bundle contains episodes, `source_video_url` must uniquely match one source video. The operator uses that episode's local time windows and prefers `global_segment_id` for segment association. Missing or ambiguous matches, or inconsistent episodes between segments and shots, fail; one request does not combine multiple source videos.

For multiple segments, time ranges must be ordered and non\-overlapping. A legacy segment `video_url` does not override the input: clips come from `source_video_url` and the time window. Removing reference\-count and segment\-duration caps applies only to this operator; downstream video generation retains its own limits.

### Request parameters

**operator_id** string 必选 `Example value: las_viral_reverse_prompt`

Operator ID

**operator_version** string 必选 `Example value: v1`

Operator version

**data** ViralReversePromptInfo 必选

Video\-to\-prompt parameters

**storyboard_bundle_url** string `Conditionally required` `Example value: tos://bucket/storyboard/storyboard_bundle_manifest.json`

Recommended storyboard input: the complete manifest file URI returned by Video Storyboard Poll, including a valid presigned HTTPS URL. Do not pass a directory, `segments_url`, or `shot_registry_url`.

**source_video_url** string 必选 `Example value: tos://bucket/source.mp4`

Must identify the same source video as the storyboard. Supports `tos://`, `http://`, and `https://`, including valid presigned URLs. Measured duration must be greater than 0 and at most 360 seconds.

**ark_api_key** string 必选 `Example value: <YOUR_ARK_API_KEY>`

A valid ModelArk API key.

**prompt_profile** string `Optional` `Example value: general`

Prompt template: `general`, `beauty`, or `home_textile`; defaults to `general`. The template changes industry emphasis without changing source\-video subjects, actions, dialogue, or other facts.

**output_language** string `Optional` `Example value: zh`

Language for descriptive prompt text: `zh` or `en`; defaults to `zh`. Original dialogue remains in its source language.

**model_tier** string `Optional` `Example value: pro`

Recommended Stage 2 model selector: `lite`, `standard`, or `pro`; defaults to `pro`.

**model_name** string `Optional` `Example value: seed-2-0-mini-260428`

Advanced exact\-model selector for Stage 2. The service forwards a non\-empty model name to ModelArk unchanged. Make sure the model is available in the current region and accessible to the ModelArk API key. Do not send it with `model_tier`.

**video_style** string `Optional` `Example value: Warm cinematic look`

Target visual style, up to 1,000 characters after trimming. It changes presentation only, not source\-video facts.

**voice_style** string `Optional` `Example value: Calm, natural adult female voice`

Target timbre for verified human speech, up to 1,000 characters after trimming. It does not create dialogue or speakers absent from the source.

**storyboard_segments** list of StoryboardSegment `Conditionally required`

Use when no bundle exists or when supplying an edited storyboard. Supports 1–24 items; use an array of length one for a single segment. Choose either `storyboard_bundle_url` or `storyboard_segments`.

**segment_id** string 必选 `Example value: segment-001`

Segment ID, unique within the request.

**source_segment_id** string `Optional` `Example value: source-segment-001`

Source\-segment provenance ID; multiple segments may reuse it. Defaults to `segment_id` when omitted.

**visual_description** string `Optional` `Example value: A silver coffee machine grinds and brews in a morning kitchen`

Legacy storyboard metadata; may be omitted, null, or empty. Generation uses the actual source\-video clip within the time window.

**start_time** float 必选 `Example value: 0`

Start time in source\-video seconds; must be finite and nonnegative. Fractional seconds are supported.

**end_time** float 必选 `Example value: 8`

Finite source end time greater than `start_time`; there is no separate 4–30\-second limit. Segments must be ordered and non\-overlapping. Ends at most 0.1 seconds beyond measured source duration are clamped when the start is inside the source. Larger overruns or segments entirely outside the source fail.

**references** list of ReversePromptReference `Optional`

Reference images for this segment; no nine\-image cap. Unique IDs and contiguous positions are still required.

**reference_id** string 必选 `Example value: product-1`

Reference image ID, unique within the segment.

**position** integer 必选 `Example value: 1`

Image order, contiguous starting at 1.

**name** string 必选 `Example value: Silver coffee machine`

Reference image name. Different references sharing a name receive readable suffixes in the output, with matching @mentions in the Prompt.

**uri** string 必选 `Example value: tos://bucket/coffee-machine.png`

Accessible image URI using `tos://`, `http://`, or `https://`, including valid presigned URLs.

**callback** Callback `Optional`

Optional task callback. Requires an enabled callback policy for the current account, operator, and version. Otherwise, omit `callback` and use Poll, or submission fails.

**url** string 必选 `Example value: https://example.com/callback`

Publicly accessible HTTPS callback URL.

Prefer `storyboard_bundle_url`. Use `storyboard_segments` only when no bundle exists or when supplying an edited storyboard; do not send both.

The manifest referenced by `storyboard_bundle_url` must use `storyboard_bundle_v2` with `storage_mode=split` and reference readable `segments` and `shots` JSON files. Character, scene, prop, and other registries are optional. The manifest and every referenced JSON file must not exceed 2 MiB.

Auxiliary references are deduplicated in order and unknown references are skipped. A reference with conflicting URIs, an ambiguous variant, or an inline URI inconsistent with the asset registry is skipped instead of being selected arbitrarily; retained references are renumbered. Different segments may reuse an image. A bare `res_` identifier is not a substitute for an accessible image URI or an explicit variant association.

### Response parameters

**metadata** metadata

Request metadata

**task_id** string `Example value: task-xxx`

Asynchronous task ID used to query status and result.

**task_status** string `Example value: PENDING`

Task status: PENDING, RUNNING, COMPLETED, FAILED, EXPIRED, CANCELLED, or TIMEOUT. PENDING and RUNNING are non\-terminal; stop polling for all other states. EXPIRED means the task expired while pending; CANCELLED means it was cancelled.

**business_code** string `Example value: 0`

Business code.

**error_msg** string

Error details.

### Request example

```bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
  "operator_id": "las_viral_reverse_prompt",
  "operator_version": "v1",
  "data": {
    "storyboard_bundle_url": "tos://bucket/storyboard/storyboard_bundle_manifest.json",
    "source_video_url": "tos://bucket/source.mp4",
    "prompt_profile": "general",
    "output_language": "en",
    "ark_api_key": "<YOUR_ARK_API_KEY>"
  }
}'
```

### Response example

```json
{
  "metadata": {
    "task_id": "task-20260914121000-abc123",
    "task_status": "PENDING",
    "business_code": "0",
    "error_msg": ""
  }
}
```

### Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |The parameter is invalid. |Invalid request, such as missing ModelArk credentials, an empty `model_name`, multiple model selectors, an invalid segment schema or time range, or a batch submission attempt |
|401 |Authorization.Missing |Missing Authorization. |LAS authentication is missing |
|401 |ApiKey.Invalid |The api key is invalid. |The LAS API key is invalid |
|500 |Server.InternalError |General Internal Error. |Internal service error |

## Poll

### Interface description

Query the status and per\-segment result of a video\-to\-prompt generation task.

A task returns `COMPLETED` only when every segment succeeds. `data.items` retains input order and contains all successful results. If any segment generation or processing fails, the entire task returns `FAILED` and does not return partial\-success items.

Non\-empty generated prompts are retained even when longer than 32,000 characters, containing control characters, imperfectly formatted, or returned with a non\-normal finish. Review and edit incomplete text before downstream use. Empty output, provider failures, timeouts, and necessary input validation can still fail; no automatic retry is added.

If measured resolution or aspect ratio is unavailable, those specifications are omitted while the generated text is retained.

Names are unique across distinct references in the task, for example `Metal cup_1` and `Metal cup_2`. Existing names are reserved to avoid suffix collisions. The same original (`name`, `reference_id`, `uri`) tuple reuses its name across segments. Only names and corresponding Prompt @mentions change; retained IDs, URIs, positions, order, and count stay unchanged. Returned presigned URIs keep their original expiry; Poll does not renew them.

Poll does not provide `metadata.submit_time` or `metadata.end_time` in this version. HTTP 200 does not mean that task execution succeeded; inspect `metadata.task_status`, `metadata.business_code`, and `metadata.error_msg`.

If source\-fact extraction fails or produces unusable facts, generation may continue with degraded facts. The task can still be `COMPLETED` when all segment prompts succeed. Public results do not expose internal quality or warning fields; `COMPLETED` does not certify factual accuracy or output quality, and `usage.complete` only indicates usage\-data completeness.

### Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|operator_id |string |Yes |las_viral_reverse_prompt |Operator ID |
|operator_version |string |Yes |v1 |Operator version |
|task_id |string |Yes |task\-xxx |Asynchronous task ID |

### Response parameters

**metadata** metadata

Request metadata

**task_id** string `Example value: task-xxx`

Asynchronous task ID.

**task_status** string `Example value: COMPLETED`

Task status: PENDING, RUNNING, COMPLETED, FAILED, EXPIRED, CANCELLED, or TIMEOUT. PENDING and RUNNING are non\-terminal; stop polling for all other states. EXPIRED means the task expired while pending; CANCELLED means it was cancelled. When `task_status=COMPLETED`, the task has finished and all segments succeeded; see `data.items` for the results.

**business_code** string `Example value: 0`

Business code. A successful task normally has `task_status=COMPLETED` and `business_code=0`.

**error_msg** string

Error details.

**data** ViralReversePromptResult

Per\-segment prompts and usage summary returned when the task succeeds

**items** list of ReversePromptItem

Prompts returned in input segment order

**segment_id** string `Example value: segment-001`

Segment ID from the request.

**source_segment_id** string `Example value: source-segment-001`

Source segment ID; defaults to the input `segment_id` when `source_segment_id` is omitted.

**prompt** string `Example value: Recreate a coffee-machine product shot...`

Video prompt generated for this segment. When the task is `COMPLETED`, this field is non\-empty; review the text before use.

**references** list of ReversePromptReference

Retained reference images. Ambiguous bundle references are skipped. If no usable references remain, an empty array is returned.

**reference_id** string `Example value: product-1`

Reference image ID.

**position** integer `Example value: 1`

Image order.

**name** string `Example value: Silver coffee machine`

Reference image name.

**uri** string `Example value: tos://bucket/coffee-machine.png`

Reference image URI.

**usage** ReversePromptUsage

Aggregate usage for ModelArk invocations in this task

**request_count** integer `Example value: 2`

Total ModelArk requests, including source\-video understanding and per\-segment prompt expansion.

**total_tokens** integer `Example value: 4096`

Total tokens across all ModelArk requests; may be empty if any invocation lacks usage data.

**complete** boolean `Example value: true`

Whether model invocation usage information is complete. This field does not indicate task status. Usage for a failed task may include model requests that were already executed. Actual charges follow the ModelArk bill.

### Request example

```bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
  "operator_id": "las_viral_reverse_prompt",
  "operator_version": "v1",
  "task_id": "task-20260914121000-abc123"
}'
```

### Response example

```json
{
  "metadata": {"task_id": "task-xxx", "task_status": "COMPLETED", "business_code": "0", "error_msg": ""},
  "data": {
    "items": [
      {"segment_id": "segment-001", "source_segment_id": "segment-001", "prompt": "A generated video prompt.", "references": []}
    ],
    "usage": {"request_count": 2, "total_tokens": 4096, "complete": true}
  }
}
```

### Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|200 |TaskId.Invalid |The task id is invalid. |The task is missing or inaccessible to this account; `metadata.task_status=FAILED` and the code is in `metadata.business_code` |
|401 |Authorization.Missing |Missing Authorization. |LAS authentication is missing |
|401 |ApiKey.Invalid |The api key is invalid. |The LAS API key is invalid |
|200 |Video.VLMFailed |Model output or model service invocation failed. |Check the provider reason code in `error_msg` and handle it as described below |
|500 |Server.InternalError |General Internal Error. |Internal service error |

When `business_code` is `Video.VLMFailed`, `error_msg` may contain one of the following provider reason codes:

|Provider reason code |Description and recommended action |
|---|---|
|PROVIDER_AUTHENTICATION_FAILED |Model resource authentication failed. Check the ModelArk API key. |
|PROVIDER_PERMISSION_DENIED |Permission to the model resource was denied. Check whether the ModelArk API key can access the selected model. |
|PROVIDER_RATE_LIMITED |The model service is rate\-limited. Retry with backoff. |
|PROVIDER_TIMEOUT |The model service call timed out. Retry with backoff. |
|PROVIDER_UNAVAILABLE |The model service is temporarily unavailable. Retry with backoff. |
|PROVIDER_FAILURE |Another model service failure occurred. Contact the service provider and provide the `task_id`. |
