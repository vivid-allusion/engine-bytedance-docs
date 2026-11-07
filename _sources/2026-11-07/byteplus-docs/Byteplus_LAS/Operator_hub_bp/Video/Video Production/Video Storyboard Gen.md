---
title: "Video Storyboard Gen"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/video-storyboard-gen"
---

The Reference Video to Product Voiceover and Storyboard operator jointly understands reference videos, target product images, and optional natural\-language requirements, then produces standard storyboard bundles for downstream text\-to\-video workflows.

# Operator introduction

> Operator ID: `las_video_storyboard_gen`

## Core capabilities

* Jointly understands reference visuals, voiceover content, and target product images to identify core uses, selling points, and camera\-visible product evidence.

* Uses `user_prompt` to emphasize storyboard structure, copywriting, selling points, hooks, or additional product requirements.

* Generates multiple candidates with different creative categories and hook directions. Up to `N+1` candidates are returned by default, where `N` is the number of input videos, capped at 6.

* Returns a standard `storyboard_bundle_manifest.json` for each successful candidate, including voiceover, a readable storyboard, structured shot descriptions, generation basis, and creative rationale.

## Effect display

* Input examples

   * Reference voiceover video 1

      [video](https://las-ai-ap-southeast-1-online-bp.tos-ap-southeast-1.bytepluses.com/operator_cards_serving/public/online/las_video_storyboard_gen/v1/input_video_01.mp4)

   * Reference voiceover video 2

      [video](https://las-ai-ap-southeast-1-online-bp.tos-ap-southeast-1.bytepluses.com/operator_cards_serving/public/online/las_video_storyboard_gen/v1/input_video_02.mp4)

   * Reference product image

      ![图片](https://las-ai-ap-southeast-1-online-bp.tos-ap-southeast-1.bytepluses.com/operator_cards_serving/public/online/las_video_storyboard_gen/v1/input_image_01.png)

* Output examples

   * The operator generates multiple storyboard candidates. Download the following example result packages:

      * [variant_001.zip](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fde78fe153634287b6699491480fefaa~tplv-goo7wpa0wc-image.image)

      * [variant_002.zip](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99a08bbca0554e54a8662fd38eb9e63a~tplv-goo7wpa0wc-image.image)

      * [variant_003.zip](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fca2c37dea814ff7869fa2291f0b62f0~tplv-goo7wpa0wc-image.image)

   * An example of the generated voiceover is:

> Still struggling with an overgrown yard and the time and effort required for manual trimming? This walk\-behind electric lawn mower cuts the lawn evenly and efficiently, handles corners and gentle slopes with ease, withstands minor bumps, and automatically collects grass clippings in the rear bag. Make lawn care easier and more efficient.

   * You can use an operator\-generated storyboard in a downstream text\-to\-video workflow. The following is an example marketing video generated from one of the storyboard results:

      [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74432c64413a451d84ea8d5df90d043a~tplv-goo7wpa0wc-image.image)

Note: This operator does not directly generate the final video.

## Supported regions

* Asia Pacific (Johor): `ap-southeast-1`

## Operator performance

|Breakdown item |Performance impact |
|---|---|
|Submit RPM |600 |
|Poll RPM |600 |
|Processing time |Reference videos and candidate scripts are processed concurrently. More or longer reference videos increase processing time; the Pro tier may take longer. |

# Input and output requirements

## Input requirements

|Breakdown |Detailed requirements |
|---|---|
|Supported input data modalities |* Video<br><br>* Image<br><br>* Text (Prompt) |
|Input format: Video |* Format: MP4, MOV, MKV/Matroska, and WebM are supported.<br><br>* Quantity: `1–5` reference videos.<br><br>* Duration: Each reference video can be up to `360` seconds long, and all reference videos can have a combined duration of up to `1800` seconds. |
|Input format: Image |* Format: JPEG, PNG, and WebP are supported.<br><br>* Quantity: `1–9` target product images. |
|Input path requirements |Provide input data to the operator through the `video_urls` and `product_image_urls` request parameters. Public URLs and TOS paths are supported.<br><br><br>* **Public URL**: A publicly accessible URL in `http://` or `https://` format.<br><br>   * Public URLs that require a login session or additional header authentication are not supported. Temporary URLs must remain valid while the task is running.<br><br>* **TOS path**: Upload the input data to a TOS bucket under the same primary account and in the same region as the current LAS service. Then provide the TOS path in the format `tos://bucket/path/file`.<br><br>   * The TOS object must exist, and the calling account must have read permission for it. |

## Output requirements

|Breakdown |Detailed requirements |
|---|---|
|Output data modality |* Text (storyboard bundle) |
|Output path: TOS |Use the `output_tos_path` request parameter to specify where the operator stores its output. A TOS path is supported.<br><br><br>* **TOS path**: Specify a writable TOS bucket directory under the same primary account and in the same region as the current LAS service. The calling account must have write permission for the directory. Format: `tos://bucket/output/`. |

# Billing information

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing items |Charges consist of the **Basic Call Fee** and the **Copywriting Generation \- Basic Fee**. The total task fee is the sum of both billing items.<br><br><br>* **Basic Call Fee**: Charged once each time the operator is successfully called.<br><br>* **Copywriting Generation \- Basic Fee**: Charged for generating product voiceover and storyboard copywriting. Usage is calculated from the total input\-video duration and adjusted by the billing\-duration conversion factor associated with the operator model tier specified by `model_tier`. |
   |Billing type |Usage\-based billing in USD, with charges generated hourly based on actual billable usage. Billing precision is millisecond\-level and rounded to the nearest millisecond. |
   |Unit price |The two billing items have different unit prices. See Billing details. |

* Billing details

   Billing formula: `Total fee = Basic Call Fee + Copywriting Generation fee = 0.14 USD + 0.21 USD/minute × Total input-video duration × Billing-duration conversion factor`

   |Billing item |Unit price |Operator model tier |Billing\-duration conversion factor |
   |---|---|---|---|
   |Basic Call Fee |0.14 USD/call |Not applicable |Not applicable |
   |Copywriting Generation \- Basic Fee |0.21 USD/minute |Standard: `model_tier` is `standard` |1 |
   |||Pro: `model_tier` is `pro` |2 |

* Billing example

   If you input three reference videos, each one minute long, and set `model_tier` to `pro`:

   * The billing\-duration conversion factor is 2.

   * The actual fee is:

      `Fee = 0.14 USD + 0.21 USD/minute × 1 minute × 3 × 2 = 1.40 USD`

# Cautions and prerequisites

|Details |Cautions and prerequisites |
|---|---|
|Authentication |Generate an LAS API Key and configure it as an environment variable. See [Obtain and configure the API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Select the LAS BaseURL for the region in which the service is deployed. See [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). |
|Product facts |Use `user_prompt` to supply verified product facts, required selling points, audience, style, and prohibited claims. Review generated copy before publication. |

# Rest API call

The operator uses asynchronous Submit and Poll APIs.

## Submit

### Interface description

Submit a task that generates product voiceover and storyboard candidates from reference videos and target product images.

### Request parameters

**operator_id** string 必选 `Example value: las_video_storyboard_gen`

Operator ID.

**operator_version** string 必选 `Example value: v1`

Operator version.

**data** VideoStoryboardGenReqParams 必选

Storyboard generation parameters.

**video_urls** array of string 必选 `Example value: ["tos://bucket/reference.mp4"]`

Provide 1–5 unique reference\-video URLs using HTTP(S) or TOS. Each video can be up to 360 seconds, with a combined maximum of 1800 seconds.

**product_image_urls** array of string 必选 `Example value: ["tos://bucket/product.png"]`

Provide 1–9 unique target\-product image URLs using HTTP(S) or TOS.

**user_prompt** string `Optional`

Ecommerce generation requirements, up to 4000 characters. May specify reference focus, product facts, selling points, audience, style, and prohibited claims.

**model_tier** string `Optional` `Example value: standard`

`standard` or `pro`. Default: `standard`.

**target_duration_sec** integer `Optional` `Example value: 40`

Target duration per candidate, 15–90 seconds. Default: 40. When omitted, the operator may adapt it to the reference\-video duration.

**min_shot_duration** float `Optional` `Example value: 4.0`

Minimum shot duration, 4–15 seconds. Default: 4.

**max_shot_duration** float `Optional` `Example value: 15.0`

Maximum shot duration, 4–15 seconds. Default: 15; must not be lower than `min_shot_duration`.

**output_tos_path** string `Optional` `Example value: tos://bucket/output/`

Writable TOS output directory in the current account and region.

**callback** Callback `Optional`

Optional status callback. Use Poll when omitted.

**url** string 必选 `Example value: https://example.com/callback`

Publicly accessible HTTPS callback URL.

### Response parameters

**metadata** metadata

Request metadata.

**task_id** string

Asynchronous task ID used to query status and results.

**task_status** string `Example value: PENDING`

`PENDING`, `RUNNING`, `COMPLETED`, `FAILED`, or `TIMEOUT`.

**business_code** string `Example value: 0`

Business code.

**error_msg** string

Error details.

### Request example

```bash
export OUTPUT_TOS_PATH="tos://example-bucket/video-storyboard-gen"

curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data @- <<JSON
{
  "operator_id": "las_video_storyboard_gen",
  "operator_version": "v1",
  "data": {
    "video_urls": [
      "https://example.com/reference-01.mp4",
      "https://example.com/reference-02.mp4"
    ],
    "product_image_urls": ["https://example.com/product.png"],
    "user_prompt": "Emphasize the pain-point hook, comparison proof, durability, and easy cleaning.",
    "output_tos_path": "${OUTPUT_TOS_PATH}"
  }
}
JSON
```

### Error codes

|HttpStatusCode |Error code |Description |
|---|---|---|
|400 |Parameter.Invalid |Invalid input count, URL, media format, video duration, target duration, shot count, or speech rate. |
|400 |Video.VLMFailed |Video or product understanding, prompt review, or candidate generation failed. |
|400 |Tos.AccessFailed |Input download, internal staging, or result upload failed. |
|401 |Authorization.Missing |Missing authentication. |
|401 |ApiKey.InValid |Invalid API key. |
|500 |Internal.ServerError |Internal service error. |

## Poll

### Interface description

Query the status and results of a product voiceover and storyboard generation task.

### Request parameters

**operator_id** string 必选 `Example value: las_video_storyboard_gen`

Operator ID.

**operator_version** string 必选 `Example value: v1`

Operator version.

**task_id** string 必选

Asynchronous task ID.

### Response parameters

**metadata** metadata

Task metadata.

**task_id** string

Asynchronous task ID.

**task_status** string `Example value: COMPLETED`

`PENDING`, `RUNNING`, `COMPLETED`, `FAILED`, or `TIMEOUT`.

**submit_time** string

Submission time in ISO 8601 format.

**end_time** string

Completion time in ISO 8601 format.

**business_code** string `Example value: 0`

Business code.

**error_msg** string

Error details.

**data** VideoStoryboardGenResponse

Returned when the task succeeds.

**result_urls** array of string

Standard storyboard\-bundle manifest URLs for successful candidates. Up to `N+1`, capped at 6, with at least one result.

Each manifest identifies an independent candidate containing `shot_registry.json`, `characters_registry.json`, `scene_registry.json`, `prop_registry.json`, and `change_report.json`. Full voiceover, readable storyboard, and creative rationale are stored in `shot_registry.script_summary`; per\-shot voiceover and visual descriptions are stored in `shot_registry.shots`.

### Request example

```bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
  "operator_id": "las_video_storyboard_gen",
  "operator_version": "v1",
  "task_id": "task-20260812150000-abc123"
}'
```

### Response example

```json
{
  "metadata": {
    "task_id": "task-20260812150000-abc123",
    "task_status": "COMPLETED",
    "business_code": "0",
    "error_msg": ""
  },
  "data": {
    "result_urls": [
      "tos://bucket/output/runs/run_x/variants/variant_001/storyboard_bundle_manifest.json"
    ]
  }
}
```
