---
title: "Video Prompt Generation"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/video-prompt-generation"
---

The Video Prompt Generation operator turns natural\-language creative requirements into an actionable video\-generation prompt. You may provide up to nine reference images to help the model understand people, products, scenes, or visual styles. Set a ModelArk API key, then optionally select a model tier or specify an exact model.

# Operator introduction

> Operator ID: `las_video_prompt_generate`

## Core capabilities

* Converts creative goals, content requirements, and language requirements into one video\-generation prompt.

* Accepts an existing prompt, requested changes, and preservation requirements together in `requirements`, and returns a complete revised prompt without additional fields.

* Uses optional reference images to describe people, products, scenes, and visual styles.

* Returns request\-count and token\-usage data for consumption tracking.

## Model selection

|`lite` |`standard` |`pro` |Verified `model_name` examples |
|---|---|---|---|
|`seed-2-0-lite-260428` |`dola-seed-2-1-turbo-260628` |`seed-2-0-pro-260328` |The three tier models plus `seed-2-0-mini-260428` |

Use `model_tier` for the normal path so the service can maintain concrete model mappings without request changes. To pin a revision, send a non\-empty `model_name`; the service forwards it to ModelArk unchanged. Do not send both fields. ModelArk rejects models that do not exist, are unavailable in the region, or are inaccessible to the API key. The service does not downgrade or retry automatically. The examples are not an admission allowlist.

## Recommendations for writing `requirements`

* From scratch: describe the target duration, subjects, setting, actions, camera, lighting, style, and audio requirements.

* Improve an existing prompt: label the existing prompt, requested changes, and unchanged content, then ask for the complete revised prompt.

* Apply a global change: state the scope and target value, such as changing the total duration to 20 seconds or applying warm natural light to every shot, and list the subject facts and action order that must remain unchanged.

* The operator regenerates a complete prompt from the full `requirements` text. Explicitly state anything that must be preserved.

### Generate a prompt from scratch

```json
{
  "parameters": {
    "locale": "en-US",
    "requirements": "Generate a 15-second coffee-machine product video prompt. The subject is a silver fully automatic coffee machine in a modern kitchen with natural morning light. Start with a medium shot of the whole machine, then show coffee beans entering the grinder, coffee pouring into a white cup, and rising steam in close-up. Keep it realistic with a concise premium pace. Do not generate brand text or subtitles."
  },
  "ark_api_key": "<YOUR_ARK_API_KEY>"
}
```

### Improve an existing prompt

```json
{
  "parameters": {
    "locale": "en-US",
    "requirements": "Improve the existing prompt below and return the complete revised prompt.\nExisting prompt: A 10-second product video. A white coffee machine sits on a kitchen counter as the camera pushes from a medium shot to a close-up of the coffee stream.\nRequested changes: Add more detail to the grinding, brewing, and steam actions, with a tighter pace.\nKeep unchanged: the white coffee machine, kitchen setting, shot order, and total duration of 10 seconds."
  },
  "ark_api_key": "<YOUR_ARK_API_KEY>"
}
```

### Apply a global change to an existing prompt

```json
{
  "parameters": {
    "locale": "en-US",
    "requirements": "Revise the existing prompt globally and return one complete new prompt.\nExisting prompt: A 10-second product video in which a silver coffee machine grinds and brews in a morning kitchen, moving from a medium shot to a close-up of the brewing outlet.\nGlobal changes: change the total duration to 20 seconds; use warm natural light and a realistic look for every shot; redistribute shot durations to match the action rhythm.\nKeep unchanged: the coffee machine appearance, kitchen setting, and grinding-then-brewing action order."
  },
  "ark_api_key": "<YOUR_ARK_API_KEY>"
}
```

## Effect display

* Example input

   ```text
   Generate a prompt for a 10-second product showcase video: In a kitchen in the early morning, a silver coffee machine automatically grinds and brews coffee, emphasizing the metallic texture and steam details.
   ```

* Example output

   ```text
   A 10-second product advertisement. In a kitchen lit by warm morning light, show a silver coffee machine in a medium shot as the camera slowly pushes in. Coffee beans fall into the grinder, followed by a close-up of the brewing outlet, with clear details of the steam and flowing coffee. Keep the machine's metallic texture, main subject, and spatial relationships consistent, with a concise and premium overall pace.
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
|Supported input data modalities |* Text<br><br>* Image |
|Input format: Text |* For the general\-requirements template, `requirements` can contain up to 32,000 characters and can describe a new prompt or include an existing prompt, requested changes, and content to preserve. `locale` supports `zh-CN` and `en-US`.<br><br>* For the spoken\-shot template, `project_text` can contain up to 5,000 characters, the five text fields can contain up to 32,000 characters in total, and `duration_seconds` must be 4–30 seconds. |
|Input format: Image |\* Number: Up to nine reference images. `position` values must be contiguous starting at 1. |
|Input path requirements |Provide text requirements through `data.parameters`. Reference images in `data.references[].uri` support the following path forms:<br><br><br>* **Public URL**: Use a stable, directly accessible `http://` or `https://` URL. The URL must not depend on a signed\-in session, cookies, or additional authentication headers. Temporary presigned URLs with signature parameters are not supported.<br><br>* **TOS path**: Use a readable object in a TOS bucket under the same primary account and in the same region as the current LAS service. The calling account must have permission to read the object. Format: `tos://bucket/path/file`. |

## Output requirements

|Breakdown item |Detailed requirements |
|---|---|
|Supported output data modalities |Text |
|Output format: Text |Returns a video\-generation prompt based on the creative requirements and optional reference images.<br><br><br>* Language: For the general\-requirements template, use `locale` to select `zh-CN` or `en-US`. The spoken\-shot template produces Chinese output. |
|Output path requirements |No output storage path is required. After the task is complete, retrieve the generated prompt from `data.prompt` in the Poll response. |

# Billing information

Set a valid ModelArk API key when invoking this operator. Charges are based on actual model usage. For model prices, see [Model pricing](https://docs.byteplus.com/en/docs/modelark/model-pricing).

# Cautions and prerequisites

## Activate ModelArk

This operator invokes ModelArk models activated under your own account, and the corresponding charges appear on your ModelArk bill. Before using the operator, activate the required ModelArk models and obtain an `ark_api_key`. You can select the model by tier or specify a non\-empty exact model name that is forwarded to ModelArk unchanged.

## General cautions

|Details |Caution and prerequisites |
|---|---|
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |

# Rest API call

# Credential notes

* The `Authorization: Bearer <LAS_API_KEY>` request header authenticates the LAS request.

* `data.ark_api_key` authenticates ModelArk calls. Do not log, share, or commit real keys.

## Submit

### Interface description

> **Note**

> Currently, only single\-task Submit is supported. Platform batch\-task APIs are not supported.

Submit an asynchronous video prompt generation task.

* The `Authorization: Bearer <LAS_API_KEY>` request header authenticates the LAS request. `ark_api_key` in the request body must be a valid ModelArk API key. The Pro tier is used by default. Use `model_tier` to select a tier or a non\-empty `model_name` to specify an exact model; the service forwards the exact name to ModelArk unchanged.

* A successful submission returns a task ID that you can use with Poll to query the result.

### Request parameters

**operator_id** string 必选 `Example value: las_video_prompt_generate`

Operator ID

**operator_version** string 必选 `Example value: v1`

Operator version

**data** PromptGenerateInfo 必选

Prompt generation parameters

**template_id** string `Optional` `Example value: video-prompt-from-requirements`

Prompt template. Defaults to `video-prompt-from-requirements` for general requirements. Also supports `spoken-shot-generate` for one spoken shot and `video-prompt-revise` for explicit revision.

**parameters** PromptGenerateParameters 必选

Fields depend on `template_id`. Send only fields supported by the selected template. The five spoken\-shot text fields have a combined 32,000\-character limit.

**locale** string `Optional` `Example value: en-US`

Optional for the requirements template: `zh-CN` or `en-US`; defaults to `zh-CN`. The spoken\-shot template does not accept this field and produces Chinese output.

**requirements** string `Conditionally required` `Example value: Generate a 10-second coffee-machine product video prompt`

Required only for the requirements template. It may describe a new prompt or include an existing prompt plus requested changes and ask for a complete revised prompt. It must not be blank after trimming and can contain up to 32,000 characters.

**source_type** string `Optional` `Example value: direct`

Optional for the spoken\-shot template; defaults to `direct`. Valid values are `direct` and `copywriting`; `copywriting` reinforces the current\-shot boundary.

**project_text** string `Conditionally required` `Example value: A coffee-machine product commercial`

Required only for the spoken\-shot template. Project background; must not be blank after trimming and can contain up to 5,000 characters.

**shot_title** string `Conditionally required` `Example value: Brewing coffee`

Required only for the spoken\-shot template. Current\-shot title; must not be blank after trimming.

**visual_description** string `Conditionally required` `Example value: The coffee machine pours coffee into a cup`

Required only for the spoken\-shot template. Current\-shot visuals and actions; must not be blank after trimming.

**dialogue** string `Optional` `Example value: Enjoy a cup of freshly ground coffee`

Accepted only by the spoken\-shot template. Current\-shot dialogue; defaults to an empty string without inventing dialogue.

**duration_seconds** integer `Conditionally required` `Example value: 6`

Required only for the spoken\-shot template. Current\-shot duration, from 4 to 30 seconds.

**director_style** string `Optional` `Example value: Natural kitchen lighting`

Accepted only by the spoken\-shot template. Together with `project_text`, `shot_title`, `visual_description`, and `dialogue`, the five text fields can contain up to 32,000 characters.

**original_prompt** string `Conditionally required` `Example value: @old-cup on a table`

Required only for explicit revision. Original prompt, non\-blank after trimming, up to 32,000 characters.

**revision_requirements** string `Conditionally required` `Example value: Replace @old-cup with @new-cup`

Required only for explicit revision. Requested changes, non\-blank after trimming, up to 32,000 characters.

**generation_parameters** VideoGenerationParameters `Optional`

Explicit\-revision target specifications that override conflicting values in the original prompt or requested changes.

**ratio** string `Optional` `Example value: 16:9`

Target aspect ratio, non\-blank and at most 64 characters.

**resolution** string `Optional` `Example value: 720p`

Target resolution, non\-blank and at most 64 characters.

**ark_api_key** string 必选 `Example value: <YOUR_ARK_API_KEY>`

A valid ModelArk API key.

**model_tier** string `Optional` `Example value: pro`

Recommended model selector: `lite`, `standard`, or `pro`; defaults to `pro`. Each tier maps to a model supported in the current region.

**model_name** string `Optional` `Example value: seed-2-0-mini-260428`

Advanced exact\-model selector. The service forwards a non\-empty model name to ModelArk unchanged. Make sure the model is available in the current region and accessible to the ModelArk API key. Do not send it together with `model_tier`.

**references** list of PromptGenerateReference `Optional`

Up to nine reference images. `position` values must be contiguous starting at 1, and `reference_id` and `name` must be unique.

**reference_id** string 必选 `Example value: product-1`

Reference image ID, unique within the request.

**position** integer `Optional` `Example value: 1`

Defaults to the one\-based array position. If supplied, it must match that position and remain contiguous; null is invalid.

**name** string 必选 `Example value: Silver coffee machine`

Reference image name, unique within the request.

**uri** string 必选 `Example value: tos://bucket/coffee-machine.png`

Stable image URI accessible to the model: `tos://`, `http://`, or `https://`. Temporary presigned URLs with signature parameters are not accepted.

**type** string `Optional` `Example value: image`

Only `image` is supported; defaults to `image`.

**asset_id** string `Optional` `Example value: customer-cup`

Optional caller\-owned asset ID. It is preserved in returned references and does not trigger asset import.

**callback** Callback `Optional`

Optional task callback. Requires an enabled callback policy for the current account, operator, and version. Otherwise, omit `callback` and use Poll, or submission fails.

**url** string 必选 `Example value: https://example.com/callback`

Publicly accessible HTTPS callback URL.

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

#### General video requirements scenario

```bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
  "operator_id": "las_video_prompt_generate",
  "operator_version": "v1",
  "data": {
    "parameters": {
      "locale": "en-US",
      "requirements": "Generate a 10-second product video prompt set in a morning kitchen. Show a silver coffee machine automatically grinding and brewing, emphasizing metallic texture and steam."
    },
    "ark_api_key": "<YOUR_ARK_API_KEY>"
  }
}'
```

#### Spoken\-shot request

```json
{
  "operator_id": "las_video_prompt_generate",
  "operator_version": "v1",
  "data": {
    "template_id": "spoken-shot-generate",
    "parameters": {
      "source_type": "direct",
      "project_text": "Coffee machine product commercial",
      "shot_title": "Brewing coffee",
      "visual_description": "The coffee machine pours coffee into a cup",
      "dialogue": "Enjoy a cup of freshly ground coffee",
      "duration_seconds": 6
    },
    "ark_api_key": "<YOUR_ARK_API_KEY>"
  }
}
```

#### Explicit prompt revision request

```json
{
  "operator_id": "las_video_prompt_generate",
  "operator_version": "v1",
  "data": {
    "template_id": "video-prompt-revise",
    "parameters": {
      "original_prompt": "@old-cup on a wooden table, warm morning light, 16:9, 720p.",
      "revision_requirements": "Replace @old-cup with @new-cup and use cool studio lighting.",
      "generation_parameters": {
        "ratio": "9:16",
        "resolution": "1080p"
      }
    },
    "ark_api_key": "<YOUR_ARK_API_KEY>",
    "model_tier": "pro",
    "references": [
      {
        "reference_id": "new-cup",
        "position": 1,
        "name": "New cup",
        "uri": "tos://bucket/new-cup.png",
        "type": "image",
        "asset_id": "customer-new-cup"
      }
    ]
  }
}
```

### Response example

```json
{
  "metadata": {
    "task_id": "task-20260914120000-abc123",
    "task_status": "PENDING",
    "business_code": "0",
    "error_msg": ""
  }
}
```

### Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |The parameter is invalid. |Invalid request, such as missing ModelArk credentials, an empty `model_name`, both `model_tier` and `model_name`, invalid reference\-image parameters, or a batch submission attempt |
|401 |Authorization.Missing |Missing Authorization. |LAS authentication is missing |
|401 |ApiKey.Invalid |The api key is invalid. |The LAS API key is invalid |
|500 |Server.InternalError |General Internal Error. |Internal service error |

## Poll

### Interface description

Query the status and result of a video prompt generation task.

Poll does not provide `metadata.submit_time` or `metadata.end_time` in this version. HTTP 200 does not mean that task execution succeeded; inspect `metadata.task_status`, `metadata.business_code`, and `metadata.error_msg`.

### Request parameters

|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|operator_id |string |Yes |las_video_prompt_generate |Operator ID |
|operator_version |string |Yes |v1 |Operator version |
|task_id |string |Yes |task\-xxx |Asynchronous task ID |

### Response parameters

**metadata** metadata

Request metadata

**task_id** string `Example value: task-xxx`

Asynchronous task ID.

**task_status** string `Example value: COMPLETED`

Task status: PENDING, RUNNING, COMPLETED, FAILED, EXPIRED, CANCELLED, or TIMEOUT. PENDING and RUNNING are non\-terminal; stop polling for all other states. EXPIRED means the task expired while pending; CANCELLED means it was cancelled.

**business_code** string `Example value: 0`

Business code. A successful task normally has `task_status=COMPLETED` and `business_code=0`.

**error_msg** string

Error details.

**data** PromptGenerateResult

Generated prompt and usage returned when the task succeeds

**prompt** string `Example value: 10-second product commercial in a warm morning kitchen...`

Generated video prompt.

**usage** PromptGenerateUsage

Usage for this ModelArk model invocation

**request_count** integer `Example value: 1`

Number of ModelArk model requests.

**prompt_tokens** integer `Example value: 1024`

Input token count; may be empty if not returned by the provider.

**completion_tokens** integer `Example value: 256`

Output token count; may be empty if not returned by the provider.

**total_tokens** integer `Example value: 1280`

Total token count; may be empty if not returned by the provider.

### Request example

```bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
  "operator_id": "las_video_prompt_generate",
  "operator_version": "v1",
  "task_id": "task-20260914120000-abc123"
}'
```

### Response example

```json
{
  "metadata": {
    "task_id": "task-20260914120000-abc123",
    "task_status": "COMPLETED",
    "business_code": "0",
    "error_msg": ""
  },
  "data": {
    "prompt": "10-second product commercial in a warm morning kitchen. Show a silver coffee machine in a medium shot as the camera slowly pushes in...",
    "usage": {
      "request_count": 1,
      "prompt_tokens": 1024,
      "completion_tokens": 256,
      "total_tokens": 1280
    }
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
