---
title: "Video Script Planner"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/video-script-planner"
---

Provide a video topic and creative requirements, optionally with image, PDF, and video references and a visual style defined by a standalone image and text, to generate a production plan for downstream video creation. The plan turns an idea into a clear content structure, shot arrangement, material suggestions, and pacing, and assigns an appropriate generation mode to each scene. Each scene can use one of three generation modes: `video`, `frame`, or `hybrid`. `video` is used for pure\-video storytelling, character actions, story scenes, environments, emotions, cinematic transitions, and visual demonstrations that do not require accurate text rendering. `frame` is used for visual demonstrations requiring accurately rendered text or layouts, courseware pages, and charts. `hybrid` is used when the same scene requires both generated video imagery and accurately rendered text or layouts. It is suitable for planning educational and marketing video scripts that interleave video content with accurately rendered text.

<span id="operator-introduction"></span>
# Operator introduction

> Operator ID: `las_hypervideo_script_planner`


<span id="application-scenarios"></span>
## Application scenarios


* **Course explainers**: Pre\-production planning for educational videos such as Chinese classical poem reading, English vocabulary lessons, math example explanations, and scientific phenomenon explanations.

* **Advertising and marketing**: Advertising output and marketing video production.

* **Batch planning**: Produce consistently structured plans for a series of videos and reduce repetitive planning work.

* Mixed production scenarios that need to control the generation ratio between pure\-video imagery and accurately rendered text imagery, while ensuring accurate text is rendered in courseware frames.


<span id="core-capabilities"></span>
## Core capabilities


* **From idea to production plan**: Organizes the topic, audience, and communication goal into an actionable video plan.

* **Production planning**: Breaks down the video content and plans the generation mode, storyboard, duration, and transitions for each scene.

* **Mode routing**: Assigns scenes to `video`, `frame`, or `hybrid`. `video` is suitable for pure\-video scenes such as character actions, story settings, environmental atmosphere, and visual demonstrations. `frame` is suitable for text\-heavy scenes such as courseware pages, accurate text, formulas, phonetics, examples, exercises, charts, and summary pages. `hybrid` is suitable when the same scene requires both generated video imagery and accurately rendered text or layouts.

* **Reference understanding and image reuse**: Understands content images, PDFs, and videos. `ref_strategy` controls whether original content images become character, prop, or background state assets used by scenes. PDFs and videos are used for understanding only.

* **Image and text style**: `visual_style` accepts one style image, style text, or both. Explicit style text takes precedence in a conflict; style is independent of the content image reference strategy.

* **Asset states and character voices**: Each character, prop, or background can have multiple states. A state can retain multiple original content images, and each character state can have its own voice, selected by character and state references in the script.

* **Multiple content types**: Supports course explainers and advertising and marketing video planning.


<span id="effect-display"></span>
## Effect display

The following example shows a creative requirement and a downstream video produced from the operator's planning result. The operator itself returns planning files and does not directly generate video.


<columns>
<columnsItem zoneid="BWGmyJzeGm">

* Example input

   ```text
   Chinese language lesson: The moon as an image in classical poetry. Compare how different poets portray the moon to understand expressing emotions through scenery and the moon as a cultural symbol.
   ```
   

</columnsItem>
<columnsItem zoneid="q4nAPc0hoc">

* Example downstream video

   <video src="https://las-ai-ap-southeast-1-online-bp.tos-ap-southeast-1.bytepluses.com/operator_cards_serving/public/online/las_hypervideo_script_planner/v1/class-demo.mp4" controls></video>
   

</columnsItem>
</columns>


<span id="supported-regions"></span>
## Supported regions


* Asia Pacific(Johor)：ap\-southeast\-1


<span id="operator-performance"></span>
## Operator performance

&nbsp;


|Breakdown item |Performance impact |
|---|---|
|Submit RPM |600 |
|Poll RPM |600 |
|Processing time |Reference counts, PDF page count, and planned duration affect processing time. The operator does not return a dynamic completion estimate. |


<span id="input-and-output-requirements"></span>
# Input and output requirements

<span id="input-requirements"></span>
## Input requirements

&nbsp;


|Breakdown item |Detailed requirements |
|---|---|
|Supported input data modalities |* Text<br><br>* Image<br><br>* PDF<br><br>* Video |
|Input format: Text |* Creative requirements: Use `prompt` to describe the topic, audience, preferred duration, key information, and production goal.<br><br>* Visual style: `visual_style.prompt` supports up to 6,000 characters. |
|Input format: Image |* Content images: Up to 20 images in `ref_images`. Duplicate URLs are removed in order of first occurrence.<br><br>* Style image: `visual_style.ref_images` supports one standalone style image, which does not count against the content\-image quota. |
|Input format: PDF |Format: PDF. Up to 3 files with no more than 5 pages in total. |
|Input format: Video |Quantity: Up to 5 reference videos. |
|Input path requirements |Provide content images, the standalone style image, PDF files, and videos through `ref_images`, `visual_style.ref_images`, `ref_files`, and `ref_videos`. All entries must use accessible `http://` or `https://` URLs. |


<span id="output-requirements"></span>
## Output requirements

&nbsp;


|Breakdown item |Detailed requirements |
|---|---|
|Supported output data modalities |Text (JSON planning files) |
|Output format: Text |* Format: JSON planning files.<br><br>* Content: Returns video intent and production planning files. Optional outputs include a creative brief and reference analysis. The operator does not directly generate images, video, or audio.<br><br>* Planned duration: 30 seconds to 30 minutes.<br><br>* Language: Chinese and English; the default is Chinese. |
|Output path requirements |`output_tos_path` is required and must be a writable `tos://` object\-storage directory. Poll returns object paths and presigned download URLs. |


<span id="billing-information"></span>
# Billing information


* Billing standards

&nbsp;

   
   |Breakdown item |Billing standard description |
   |---|---|
   |Billing item |* Plan\-generation charge: billed by the planned output duration tier.<br><br>* Multimodal reference\-input surcharge: charged at most once per task when valid content images, PDFs, videos, or a standalone style image are provided. Creative or style text alone does not trigger the surcharge, and `ref_strategy=none` does not waive it. |
   |Billing type |Pay\-as\-you\-go, billed in USD. Charges are calculated per successful call according to the applicable billing item. |
   |Unit price |Unit prices vary by billing item. See Billing details. |
   

* Billing details

&nbsp;

   
   |Billing item |Planned output duration |Unit price |
   |---|---|---|
   |Plan\-generation charge |Output plan length ≤ 30 seconds |1.80 USD/call |
   ||30 seconds < output plan length ≤ 1 minute |2.30 USD/call |
   ||1 minute < output plan length ≤ 2 minutes |3.00 USD/call |
   ||2 minutes < output plan length ≤ 5 minutes |4.50 USD/call |
   ||5 minutes < output plan length ≤ 10 minutes |6.80 USD/call |
   ||Output plan length \> 10 minutes |6.80 USD base price, plus 3.70 USD for each additional 10\-minute tier; a partial tier is rounded up. |
   |Multimodal reference\-input surcharge |Not applicable |1.50 USD/call when applicable |
   


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

<span id="api-call-instructions"></span>
## API call instructions


* This operator uses asynchronous task APIs. Call the Submit interface to obtain a `task_id`, then call the Poll interface with that `task_id` to query the task status and retrieve the planning results after the task completes.


<span id="submit"></span>
## Submit

<span id="interface-description"></span>
### Interface description

Submit a video script planning task. A successful submission returns a task ID and the `PENDING` status. Use the Poll interface to query the final status. Planning files are available only after the task completes successfully; successful submission does not mean planning is complete.

Reference materials support content understanding. Depending on `ref_strategy`, `ref_images` may also be included as original images in entity states in the production plan. PDFs and videos are used only for understanding. `visual_style` independently defines the global visual style using one style image, text instructions, or both. The operator outputs planning JSON and does not directly generate images, videos, or audio.

<span id="request-parameters"></span>
### Request parameters



**operator_id** <span data-label="purple">string</span> <span data-api-tag="require|9bNxnY">必选</span> `Example value: las_hypervideo_script_planner`

Operator ID.



**operator_version** <span data-label="purple">string</span> <span data-api-tag="require|95byXh">必选</span> `Example value: v1`

Operator version.



**data** <span data-label="purple">HyperVideoScriptPlannerReqParams</span> <span data-api-tag="require|Q2elfY">必选</span>

Video script planning request parameters.


**prompt** <span data-label="purple">string</span> <span data-api-tag="require|FblfMK">必选</span> `Example value: Generate a 5-minute explainer video plan for the Grade 3 math topic "Area of Rectangles"`

Creative requirements. Must not be empty or whitespace\-only. Include the topic, target audience, and information that must appear.



**prompt_strategy** <span data-label="purple">string</span> `Optional` `Example value: education_v1`

Prompt strategy. `education_v1` is for education planning; `marketing_ecommerce_v1` is for marketing and e\-commerce planning. An explicitly supplied strategy takes precedence. If omitted, the education or marketing strategy is selected based on `planning.domain`. Keep these two settings consistent.



**total_duration_sec** <span data-label="purple">integer</span> `Optional` `Example value: 300`

Target total video duration in seconds, range [30, 1800]. If `min_total_duration_sec` or `max_total_duration_sec` is also supplied, the target must satisfy the corresponding lower or upper bound; omitted bounds do not participate in relationship validation. If omitted, the target is inferred from the creative requirements, falling back to 270 seconds if it cannot be determined. The final duration is the `total_duration_sec` returned by Poll.



**planning** <span data-label="purple">Planning</span> `Optional`

Planning domain and domain\-specific context. Defaults to the education domain if omitted, `null`, or an empty object.


**domain** <span data-label="purple">string</span> `Optional` `Example value: education`

Planning domain: `education` for education or `marketing` for marketing. Defaults to `education` if omitted, `null`, or blank. Values are case\-insensitive after trimming leading and trailing whitespace.



**context** <span data-label="purple">PlanningContext</span> `Optional` `Example value: {"target_grade":"Grade 3","subject":"Math","course_topic":"Area of Rectangles"}`

Domain context. If omitted, `null`, or an empty object, no domain context is added. `education` uses the three optional fields below. `marketing` accepts a custom JSON object with no fixed required child fields. Currently, include product, audience, and other marketing requirements in `prompt`; custom fields are not yet used to generate the plan.


**target_grade** <span data-label="purple">string</span> `Optional` `Example value: Grade 3`

Education domain only: target grade. If omitted or blank, this information is not supplied. Must be placed inside `planning.context`, not at the top level of `data`.



**subject** <span data-label="purple">string</span> `Optional` `Example value: Math`

Education domain only: subject. If omitted or blank, this information is not supplied.



**course_topic** <span data-label="purple">string</span> `Optional` `Example value: Area of Rectangles`

Education domain only: course topic. If omitted or blank, this information is not supplied.





**ref_images** <span data-label="purple">list of string</span> `Optional` `Example value: ["https://example.com/reference-01.png"]`

Content reference image URLs, up to 20 items. Provide accessible HTTP(S) image URLs. If omitted or an empty list, no content reference images are used. Duplicate URLs are removed while preserving their first\-occurrence order. Images support content understanding; `ref_strategy` determines whether scenes use them as original images in entity states. The independent style image does not count toward this limit.



**ref_files** <span data-label="purple">list of string</span> `Optional` `Example value: ["https://example.com/reference.pdf"]`

Reference file URLs, up to 3 items. Currently only PDFs are supported, with a maximum of 5 pages across all PDFs. Provide accessible HTTP(S) URLs. If omitted or an empty list, no reference files are used. PDF text and images within PDF pages are used only for content understanding and cannot be referenced as original images.



**ref_videos** <span data-label="purple">list of string</span> `Optional` `Example value: ["https://example.com/demo.mp4"]`

Reference video URLs, up to 5 items. Each item must be a string that, after trimming leading and trailing whitespace, is a non\-empty HTTP(S) URL of no more than 4096 characters. If omitted, `null`, or an empty list, no reference videos are used. Duplicate URLs are removed while preserving their first\-occurrence order. Videos are used only for content understanding and are not directly inserted into the final video. Whether a video's format, codec, size, and duration can be processed depends on the material\-understanding result.



**ref_strategy** <span data-label="purple">string</span> `Optional` `Example value: auto`

Strategy for referencing original content images. Accepts only lowercase `auto`, `none`, and `all`. If omitted, the legacy `reference_mode` value is used; if both are omitted, defaults to `auto`. `auto`: automatically selects relevant content images, possibly none. `none`: excludes original content images from execution assets, while the materials still support understanding. `all`: requires every deduplicated content image to be included in an entity state and used by a scene through `asset_refs`; the task fails if complete, valid bindings cannot be established. The strategy does not require referencing PDFs or videos and does not affect the global visual style. `none` does not waive material\-processing charges.



**visual_style** <span data-label="purple">VisualStyle</span> `Optional`

Global visual style, specified with an image, text, or both. The image provides a visual foundation, and the text supplements or adjusts it; explicit conflicts are resolved in favor of the style text. If omitted, `null`, an empty object, or both image and text are empty, the default style logic applies. The style applies under every reference strategy. Characters, objects, logos, and text in the style image are not automatically transferred, and pixel\-perfect reproduction is not guaranteed.


**ref_images** <span data-label="purple">list of string</span> `Optional` `Example value: ["https://example.com/watercolor-style.png"]`

Style reference image array, with a maximum of 1 image, counted separately from the 20 content images allowed in the top\-level `ref_images`. Each item must be a string that, after trimming leading and trailing whitespace, is a non\-empty HTTP(S) URL of no more than 4096 characters. If omitted, `null`, or an empty array, no style image is used. The style image is excluded from content\-reference coverage requirements and does not directly become a content asset. A supplied style image counts as multimodal input.



**prompt** <span data-label="purple">string</span> `Optional` `Example value: Preserve the watercolor brushwork, switch to a cool palette, and add more whitespace`

Style text instructions. Must be a string of no more than 6000 characters after trimming leading and trailing whitespace. If omitted, `null`, or blank, no style text is used. Can be used on its own without a style image. The text itself does not count as a separate multimodal material input.




**reference_mode** <span data-label="purple">string</span> `Optional` `Example value: auto`

Legacy name for `ref_strategy`, with the same values and semantics. If both fields have non\-`null` values, they must match exactly; otherwise, `Parameter.Invalid` is returned.



**output_tos_path** <span data-label="purple">string</span> <span data-api-tag="require|RWYtky">必选</span> `Example value: tos://bucket/output/script_planner/`

Object storage directory for result output. Supports only `tos://` addresses and must not be empty. The calling account must have write access to the target directory.



**output_language** <span data-label="purple">string</span> `Optional` `Example value: en`

Output language. Supports Chinese and English. Chinese aliases: `zh`, `cn`, `chinese`, `zh-cn`, `中文`. English aliases: `en`, `eng`, `english`, `en-us`, `英文`. Latin\-letter aliases are case\-insensitive. Default: `zh`.



**aspect_ratio** <span data-label="purple">string</span> `Optional` `Example value: 16:9`

Target video aspect ratio. Default: `16:9`.



**resolution** <span data-label="purple">string</span> `Optional` `Example value: 1920x1080`

Target video resolution in pixels, expressed as "widthxheight". Default: `1280x720`.



**fps** <span data-label="purple">integer</span> `Optional` `Example value: 25`

Target video frame rate in frames per second, range [1, 120]. Default: 30.



**video_target_ratio** <span data-label="purple">double</span> `Optional` `Example value: 0.6`

Target duration share of `video` scenes, range [0, 1]. Used for character actions, story situations, atmosphere, and visual demonstrations that do not require accurate text rendering. You may supply only some ratios. Ratios are normalized when all are supplied or the supplied positive values sum to at least 1. If exactly one mode is unspecified, it receives the remainder; in other cases, the model plans the ratios. At least one usable mode must remain after applying these rules. The marketing strategy defaults to `hybrid_target_ratio=0`, so `video_target_ratio` and `frame_target_ratio` cannot both be set to 0 in that case.



**frame_target_ratio** <span data-label="purple">double</span> `Optional` `Example value: 0.3`

Target duration share of `frame` scenes, range [0, 1]. Used for accurately rendered text, layouts, courseware pages, charts, and similar content. If omitted, this ratio is filled in according to the rules above or planned by the model.



**hybrid_target_ratio** <span data-label="purple">double</span> `Optional` `Example value: 0.1`

Target duration share of `hybrid` scenes, range [0, 1]. Used when the same scene requires both generated video imagery and accurately rendered text or layouts. If omitted for the education strategy, the template plans it automatically; if omitted for the marketing strategy, defaults to 0.



**video_max_scene_duration_sec** <span data-label="purple">integer</span> `Optional` `Example value: 8`

Maximum planned duration of a single `video` mode scene in seconds, range [4, 30]. Default: 15.



**min_total_duration_sec** <span data-label="purple">integer</span> `Optional` `Example value: 240`

Lower bound of the planned total duration in seconds, range [1, 1800]. If omitted, a lower bound is generated from the target duration, typically about 85% of the target.



**max_total_duration_sec** <span data-label="purple">integer</span> `Optional` `Example value: 300`

Upper bound of the planned total duration in seconds, range [1, 1800]. If omitted, an upper bound is generated from the target duration, typically about 115% of the target. If `min_total_duration_sec` is also supplied, this value must be greater than or equal to that lower bound.




&nbsp;

<span id="response-parameters"></span>
### Response parameters


**metadata** <span data-label="purple">metadata</span>

Request metadata.


**task_id** <span data-label="purple">string</span> `Example value: task-xxx`

Task ID returned after successful submission, used for Poll queries.



**task_status** <span data-label="purple">string</span> `Example value: PENDING`

`PENDING` upon successful submission, indicating that the task has been accepted. Query Poll for the final status.



**business_code** <span data-label="purple">string</span> `Example value: 0`

Business code. `0` indicates successful submission.



**error_msg** <span data-label="purple">string</span>

Error description; empty when no error occurs.



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
    "operator_id": "las_hypervideo_script_planner",
    "operator_version": "v1",
    "data": {
        "prompt": "Generate a 60-second product introduction video plan for a portable coffee cup aimed at commuters. Use the product images, specification document, and demonstration video to highlight its leakproof design and easy cleaning.",
        "prompt_strategy": "marketing_ecommerce_v1",
        "total_duration_sec": 60,
        "planning": {
            "domain": "marketing"
        },
        "ref_images": ["https://example.com/product-front.png"],
        "ref_files": ["https://example.com/product-specification.pdf"],
        "ref_videos": ["https://example.com/product-demo.mp4"],
        "ref_strategy": "all",
        "visual_style": {
            "ref_images": ["https://example.com/watercolor-style.png"],
            "prompt": "Preserve the watercolor brushwork from the reference image, use a cool palette, and add more whitespace while keeping product text clearly legible"
        },
        "output_tos_path": "tos://bucket/output/script_planner/",
        "output_language": "en",
        "aspect_ratio": "16:9",
        "resolution": "1920x1080",
        "fps": 25,
        "video_target_ratio": 0.6,
        "frame_target_ratio": 0.3,
        "hybrid_target_ratio": 0.1,
        "video_max_scene_duration_sec": 8,
        "min_total_duration_sec": 50,
        "max_total_duration_sec": 70
    }
}'
```


<span id="response-example"></span>
#### Response example

```json
{
  "metadata": {
    "task_id": "20250108_150000_abc123",
    "task_status": "PENDING",
    "business_code": "0",
    "error_msg": ""
  }
}
```


<span id="error-codes"></span>
### Error codes

&nbsp;


|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |The parameter is invalid. |Invalid request parameters, such as empty required fields, unsupported `planning.domain`, exceeded count or length limits, invalid material or style field types or URLs, conflicting `ref_strategy` and `reference_mode`, or invalid duration relationships. Material\-reading failures, excess PDF pages, model\-planning failures, and reference\-binding failures during execution are returned in Poll's terminal\-state metadata. |
|401 |Authorization.Missing |The authorization header is missing. |Missing authentication. |
|401 |ApiKey.Invalid |The api key is invalid. |Invalid API key. |
|500 |Server.InternalError |General Internal Error |Internal server error. |


<span id="poll"></span>
## Poll

<span id="interface-description-1"></span>
### Interface description

Query the status and result of an asynchronous video script planning task. After Submit accepts the task, poll with the same `task_id`. Use artifact URLs only when `task_status=COMPLETED` and `business_code=0`. Before a result is available, `data` is omitted or `null`. Creative briefs and reference analyses are returned with the completed task, not as early progress results.

For failures, inspect `metadata.business_code` and `metadata.error_msg`. A missing task returns `FAILED` and `TaskId.Invalid`. During execution, `Model.InputLimitExceeded` means the model input exceeds a limit: reduce reference materials or shorten the input. `Model.OutputLimitExceeded` means the model output exceeds a limit: shorten the planned duration or split the task. `Model.RateLimited` means model rate limiting: retry later. HTTP status alone does not establish task success.

<span id="request-parameters-1"></span>
### Request parameters



**operator_id** <span data-label="purple">string</span> <span data-api-tag="require|dMbMN0">必选</span> `Example value: las_hypervideo_script_planner`

Operator ID



**operator_version** <span data-label="purple">string</span> <span data-api-tag="require|nPLUck">必选</span> `Example value: v1`

Operator version



**task_id** <span data-label="purple">string</span> <span data-api-tag="require|6rsGkZ">必选</span> `Example value: task-xxx`

Task ID



&nbsp;

<span id="response-parameters-1"></span>
### Response parameters



**metadata** <span data-label="purple">metadata</span>

Request metadata


**task_id** <span data-label="purple">string</span> `Example value: task-xxx`

Task ID



**task_status** <span data-label="purple">string</span> `Example value: COMPLETED`

Task status. PENDING: Request received, RUNNING: In progress, COMPLETED: Completed, FAILED: Failed.



**submit_time** <span data-label="purple">string</span> `Example value: 2026-07-21T16:04:06+08:00`

Task submission time, in ISO 8601 timestamp format.



**end_time** <span data-label="purple">string</span> `Example value: 2026-07-21T16:04:06+08:00`

Task end time, in ISO 8601 timestamp format.



**business_code** <span data-label="purple">string</span> `Example value: 0`

Business code. `0` indicates success.



**error_msg** <span data-label="purple">string</span>

Error explanation for a task or query failure; interpret it together with `business_code`.




**data** <span data-label="purple">HyperVideoScriptPlannerResponse</span>

Task result; omitted or `null` before a result is available. Successful results contain artifact addresses and summary values.


**intent_profile_path** <span data-label="purple">string</span> `Example value: tos://bucket/out/run/intent_profile.json`

Object storage path of the intent profile JSON, using `tos://`.



**intent_profile_uri** <span data-label="purple">string</span> `Example value: https://example.com/intent_profile.json`

Presigned download URL of the intent profile JSON.



**production_plan_path** <span data-label="purple">string</span> `Example value: tos://bucket/out/run/production_plan.json`

Object storage path of the production plan JSON, using `tos://`.



**production_plan_uri** <span data-label="purple">string</span> `Example value: https://example.com/production_plan.json`

Presigned download URL of the production plan JSON.



**creative_brief_path** <span data-label="purple">string</span> `Example value: tos://bucket/out/run/creative_brief.json`

Optional. Object storage path of the creative brief JSON, returned after a marketing task that generates this artifact succeeds. Omitted for education tasks.



**creative_brief_uri** <span data-label="purple">string</span> `Example value: https://example.com/creative_brief.json`

Optional. Presigned download URL of the creative brief JSON; omitted when this artifact is not generated.



**reference_analysis_path** <span data-label="purple">string</span> `Example value: tos://bucket/out/run/reference_analysis.json`

Optional. Object storage path of the reference analysis JSON, returned when content references produce an analysis artifact. A standalone style image or style text alone does not produce it.



**reference_analysis_uri** <span data-label="purple">string</span> `Example value: https://example.com/reference_analysis.json`

Optional. Presigned download URL of the reference analysis JSON; omitted when this artifact is not generated.



**total_duration_sec** <span data-label="purple">double</span> `Example value: 60.0`

Total duration of the actual output plan in seconds; it may differ from the requested target duration.



**contains_multimodal_input** <span data-label="purple">boolean</span> `Example value: true`

Whether valid multimodal reference input was recorded. `true` when any input usage is greater than zero; `false` when there is no positive usage or the result contains no input statistics. Public inputs that can count are content images, PDFs, videos, and the standalone style image. Text in `prompt` or `visual_style.prompt` alone does not trigger this flag. `ref_strategy=none` does not disable input accounting.




&nbsp;

<span id="examples-1"></span>
### Examples

<span id="request-example-1"></span>
#### Request example

```bash
curl --location "${LAS_ENDPOINT}/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
    "operator_id": "las_hypervideo_script_planner",
    "operator_version": "v1",
    "task_id": "20250108_150000_abc123"
}'
```


<span id="response-example-1"></span>
#### Response example

This successful marketing task with content references shows all optional artifacts. Fields for artifacts that were not generated are omitted, rather than returned as empty file addresses, empty strings, or `null`. All files share the task output directory; storage paths use `tos://`. Use the corresponding presigned URLs to download them.

```json
{
  "metadata": {
    "task_id": "20250108_150000_abc123",
    "task_status": "COMPLETED",
    "submit_time": "2026-07-21T16:04:06+08:00",
    "end_time": "2026-07-21T16:04:06+08:00",
    "business_code": "0",
    "error_msg": ""
  },
  "data": {
    "intent_profile_path": "tos://bucket/out/run/intent_profile.json",
    "intent_profile_uri": "https://example.com/intent_profile.json",
    "production_plan_path": "tos://bucket/out/run/production_plan.json",
    "production_plan_uri": "https://example.com/production_plan.json",
    "creative_brief_path": "tos://bucket/out/run/creative_brief.json",
    "creative_brief_uri": "https://example.com/creative_brief.json",
    "reference_analysis_path": "tos://bucket/out/run/reference_analysis.json",
    "reference_analysis_uri": "https://example.com/reference_analysis.json",
    "total_duration_sec": 60.0,
    "contains_multimodal_input": true
  }
}
```


<span id="error-codes-1"></span>
### Error codes

&nbsp;


|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |The parameter is invalid. |Invalid parameter |
|401 |Authorization.Missing |The authorization header is missing. |Missing authentication |
|401 |ApiKey.Invalid |The api key is invalid. |Invalid API key |
|500 |Server.InternalError |General Internal Error |Internal server error |


<span id="reference:-description-of-output-json-file-fields"></span>
## Reference: Description of output JSON file fields

<span id="intent_profile.json"></span>
### intent_profile.json

`intent_profile.json` describes the content requested by the user. It mainly includes the video title, planning domain, topic, key knowledge points, audience, content goals, content units, total duration, aspect ratio, resolution, output language, global visual style, text policy, audio policy, constraints, and assumptions. Key fields include:

&nbsp;


|Name |Type |Description |
|---|---|---|
|video_title |string |Suggested video title. |
|planning_domain |string |Detected planning domain. Currently supports education (`education`) and marketing (`marketing`). |
|scenario_type |string |Specific scenario type within the domain, such as classical poetry. |
|topic |object |Topic information, including the main topic, key knowledge points, and category. |
|target_audience |object |Target audience information, including age range, cognitive level, and attention characteristics. |
|content_goal |string |Overall content goal of the video. |
|key_messages |array |Key messages or objectives to communicate. |
|content_units |array |Structured content units, such as formula explanations, operation steps, and product selling points. |
|total_duration_sec |integer |Planned total video duration in seconds. |
|aspect_ratio |string |Target video aspect ratio. |
|resolution |string |Target video resolution. |
|language |string |Video output language. |
|global_style |object |Global style, including visual style, text policy, audio style, and music policy. |


<span id="production_plan.json"></span>
### production_plan.json

`production_plan.json` describes how the downstream pipeline should produce the video. It mainly includes:

&nbsp;


|Name |Type |Description |
|---|---|---|
|content_structure |array |Content structure. Each item contains a section ID, name, goal, duration, and recommended generation mode. |
|generation_mix_strategy |object |Duration ratio strategy for `video` / `frame` / `hybrid`. |
|asset_plan |array |Assets to generate or reuse. Characters, props, and backgrounds use entities with `states`; covers, standalone illustrations, icons, and charts can retain a flat structure. |
|scene_plan |array |Executable scene list. Each scene uses `generation_type` to distinguish `video`, `frame`, or `hybrid`. |
|assembly_plan |object |Final assembly order, default transition, transition duration, audio normalization, and background music policy. |
|metadata |object |Additional planning information. `asset_schema_version="v3"` identifies the current asset and voice structure; the operator version remains `v1`. |


<span id="asset_plan-key-fields"></span>
#### asset_plan key fields

A character, prop, or background root identifies an entity; visual generation information belongs to its single level of `states`. Different ages or outfits of one character, intact or broken versions of one prop, or daytime and nighttime appearances of one background use different states of the same entity. Different views of one appearance can share a state with multiple original images.

&nbsp;


|Name |Type |Description |
|---|---|---|
|asset_id |string |Unique entity ID. Script `character_id` references character identity; visual scene references use specific state IDs. Entity, state, and other asset IDs are globally unique. |
|asset_type |string |Entity type: `character`, `prop`, or `background`. Flat assets such as covers and standalone illustrations use their corresponding asset types. |
|name |string |Entity name. |
|purpose |string |Purpose of the asset in the video. |
|states |array |One level of visual states. Visible entities have at least one state, and states cannot contain nested `states`. Voice\-only characters use an empty array. |
|voice_only |boolean |Applies to characters only; defaults to `false`. `true` identifies a voice\-only character, including a narrator, without visual states or image generation. |
|audio |object |`null` for visible characters, whose voices belong to their states. Voice\-only characters store `speaker_role` and `voice_style` here. Props and backgrounds have no voice settings. |
|metadata |object |Additional asset information. |


<span id="states-key-fields"></span>
#### states key fields

&nbsp;


|Name |Type |Description |
|---|---|---|
|asset_id |string |Unique state ID, referenced by scene `asset_refs` and character script `character_state_id`. |
|state_name |string |State name, such as childhood, adulthood, broken, or nighttime. |
|asset_type |string |Visual type matching the parent entity: `video_character_reference_image` / `frame_character_reference_image`, `video_prop_reference_image` / `frame_prop_reference_image`, or `video_background_reference_image` / `frame_background_reference_image`. |
|purpose |string |Purpose of this state in the video. |
|prompt |string |Complete visual generation description containing both shared identity features and this state's appearance. At least one of `prompt` and an existing `uri` is nonempty. |
|negative_prompt |string |Negative visual generation constraints for this state. |
|generation_model |string |Recommended generation model; `null` when reusing original content images. |
|uri |string |Existing primary image address. When reusing original images, it equals `reference_images[0].uri`; it is not a newly generated image or a merged result of all images. |
|reference_images |array |All original content images retained by this state. Each item has a `reference_id` and original input `uri`, sourced only from top\-level `ref_images`, excluding PDF images, videos, and standalone style images. |
|audio |object |Character state voice settings: a nonempty `speaker_role` and a `voice_style` describing timbre, accent, or delivery. Empty `voice_style` means no additional requirements. Silent states use `null`; props and backgrounds have no voice settings. |
|metadata |object |Additional state information. |


Scenes reference visual states by state `asset_id`. A `ref_image_*` identifies an original image and must not be used in `asset_refs`. Retain all of a state's `reference_images`; reading only its primary `uri` does not consume the remaining images. Logical entities do not directly generate images. Flat assets such as covers retain their own model, prompts, and URI. New plans no longer output `reference_materials` or `reference_refs`.

<span id="scene_plan-key-fields"></span>
#### scene_plan key fields

&nbsp;


|Name |Type |Description |
|---|---|---|
|scene_id |string |Unique scene ID. |
|section_id |string |ID of the containing section, whose plan is defined in `content_structure`. |
|scene_title |string |Scene title. |
|generation_type |string |Scene generation mode. Supports `video`, `frame`, or `hybrid`. |
|duration_sec |double |Planned scene duration in seconds. |
|scene_goal |string |Content goal to accomplish in the scene. |
|scene_function |string |Scene function, such as hook, context, explanation, demonstration, or recap. |
|content_summary |string |Scene content summary. |
|asset_refs |array |IDs of specific visual states or flat assets used by the scene. Characters, props, and backgrounds use state `asset_id`, never a logical entity ID or `ref_image_*`. |
|storyboards |array |Video storyboard list, including duration, visual prompt, camera design, and storyboard audio. |
|frame_prompt |object |Visual, text, layout, and animation plan for a frame or hybrid scene. |
|audio |object |Scene\-level audio plan retaining script, timing, and voice references. Voice settings are resolved using `character_id` and `character_state_id`, as described below. |
|transition |object |Transition requirements for entering and leaving the scene. |


<span id="scene-and-storyboard-audio"></span>
#### Scene and storyboard audio

&nbsp;


|Name |Type |Description |
|---|---|---|
|need_audio |boolean |Whether this audio segment is needed. |
|audio_type |string |Audio type, such as `dialogue`. |
|character_id |string |Speaking character's root `asset_id`; cannot reference a prop, background, or state. |
|character_state_id |string |Speaking state's `asset_id`. It must belong to the selected character and have valid `audio` voice settings. `null` for voice\-only characters, whose root voice is used. |
|text |string |Scene or storyboard script, stored here rather than in entity or state voice settings. |
|sync_required |boolean |Whether audiovisual synchronization is required. |
|allow_bgm |boolean |Whether background music is allowed. |
|allow_sfx |boolean |Whether sound effects are allowed. |


A `video` scene with storyboards uses `storyboards[*].audio` and has empty scene\-level audio. `frame` uses `scene.audio`; `hybrid` places speech in `scene.audio` and disables storyboard audio. Scene and storyboard audio no longer directly contain `speaker_role` or `voice_style`. The speaking state may differ from the visual state, such as an adult voice narrating a childhood scene. Keep scripts from different characters or voice states separate.

The following production plan excerpt shows two content images assigned to the same character state and the voice references used by its script. Other section, scene, and assembly fields are omitted.

```json
{
  "asset_plan": [
    {
      "asset_id": "character_aming",
      "asset_type": "character",
      "name": "Aming",
      "voice_only": false,
      "audio": null,
      "states": [
        {
          "asset_id": "aming_child",
          "state_name": "Childhood",
          "asset_type": "video_character_reference_image",
          "reference_images": [
            {
              "reference_id": "ref_image_001",
              "uri": "https://example.com/child-front.png"
            },
            {
              "reference_id": "ref_image_002",
              "uri": "https://example.com/child-side.png"
            }
          ],
          "uri": "https://example.com/child-front.png",
          "generation_model": null,
          "audio": {
            "speaker_role": "Young Aming",
            "voice_style": "Clear, youthful child voice"
          }
        }
      ]
    }
  ],
  "scene_plan": [
    {
      "scene_id": "scene_childhood",
      "generation_type": "video",
      "asset_refs": [
        "aming_child"
      ],
      "audio": {},
      "storyboards": [
        {
          "storyboard_id": "board_01",
          "audio": {
            "need_audio": true,
            "audio_type": "dialogue",
            "character_id": "character_aming",
            "character_state_id": "aming_child",
            "text": "Let us set off.",
            "sync_required": true,
            "allow_bgm": false,
            "allow_sfx": false
          }
        }
      ]
    }
  ],
  "metadata": {
    "asset_schema_version": "v3"
  }
}
```


<span id="creative_brief.json-(optional)"></span>
### creative_brief.json (optional)

Returned when a marketing task generates a creative brief; omitted for education tasks. The `creative_brief` string preserves the creative text used for planning, including its original paragraph breaks. It is not a second structured production plan.

```json
{
  "creative_brief": "# Creative concept\n\nIntroduce the main selling point through a product use case, then close with a call to action."
}
```


<span id="reference_analysis.json-(optional)"></span>
### reference_analysis.json (optional)

Returned when content references such as images, PDFs, or videos produce an analysis, for both education and marketing. It is omitted without content references, including when only a standalone style image or style text is provided. References can still produce analysis with `ref_strategy=none`; source identifiers in the analysis do not establish that scenes use the original images.

&nbsp;


|Name |Type |Description |
|---|---|---|
|source_purpose |string |Purpose of the reference materials. |
|summary |string |Summary of the reference content. |
|evidence |array |Supporting facts and constraints. Items may include `evidence_id`, `kind`, `content`, `source_refs`, and `attributes`. |
|ambiguities |array |Uncertain or ambiguous information in the references. |
|image_entities |array |Content image entity and state groups. Items contain `entity_key`, `entity_type`, `name`, and `states`; empty when no usable grouping is available. |


An `image_entities` item's `entity_type` is `character`, `prop`, or `background`. Each of its `states` contains `state_key`, `state_name`, `description`, and `image_refs`. `image_refs` identifies original content images using `ref_image_*`. The analysis `entity_key` and `state_key` explain recognition groups; execution references use entity and state `asset_id` values in the production plan. The file contains the analysis object directly, without an extra `reference_analysis` wrapper.

Poll returns artifact addresses after the entire task succeeds. Optional files that were not generated have their `path` and `uri` fields omitted, and no empty files are produced. See the Poll API for paths and return conditions.
