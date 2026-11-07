---
title: "Short drama script fission"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Short_drama_script_fission"
---

The short drama script fission operator (`las_short_drama_script_fission`) is used to perform targeted adaptation based on existing episodic scripts. The operator retains the core character structure, conflict chain, emotional curve, and key highlights of the original script, systematically rewrites character identities, worldview settings, regional context, industry background, and key terminology, and generates new script versions tailored to the target market and subject matter. The output includes the diversified episodic script catalog, the complete script, the outline, and the mapping table between the original and new versions, making it suitable for short drama overseas distribution, blockbuster remakes, and content direction testing.

<span id="operator-introduction"></span>
# Operator introduction

> Operator ID: las_short_drama_script_fission


<span id="application-scenarios"></span>
## Application scenarios


* **Short drama overseas adaptation**: Rewrites existing Chinese short drama scripts into versions suitable for the target country's market, for localized remakes or content testing.

* **Hit script adaptation**: Expands existing blockbuster scripts into new versions across multiple genres while retaining the original key highlights.

* **Content direction A/B testing**: Quickly generates multiple genre or regional versions based on the same original script for distribution testing and content selection.

* **Platform\-based script production**: Provides structured diversified script assets for downstream video generation, storyboarding, narration, voice\-over, or scriptwriting teams.


<span id="core-capabilities"></span>
## Core capabilities


* **Targeted adaptation with plot skeleton retention**: Retains the original script's character functions, character relationships, key event sequence, and main storyline logic, only adapting surface settings and dialogue context.

* **Regional adaptation**: Supports generating target scripts for different regional contexts, including coordinated adaptation of character naming styles, institutional backgrounds, dialogue expressions, and social relationship logic.

* **Genre\-based rewriting**: Supports overall style migration according to the target genre, adapting the same plot skeleton into new scripts reusable across different genres.

* **Batch episode processing**: Supports submitting multiple episodes of scripts at once via directory or list, processes them in input order, and maintains narrative continuity across the entire series.

* **Structured result delivery**: Outputs post\-fission episode scripts, full series scripts, outlines, and mapping tables to facilitate subsequent video production, proofreading, manual refinement, and effect review.

   * **Episode script directory**: Each episode script after fission is typically located at `{output_tos_path}/{task_id}/episodes/`.

   * **Full series script**: The complete fission script linked together for overall review.

   * **Script outline**: The refined structured outline for quickly viewing the main storyline.

   * **Mapping table**: Records the mapping relationships of characters, events, conflicts, and terminology before and after fission, facilitating manual proofreading and review.


<span id="effect-demonstration"></span>
## Effect demonstration


<columns>
<columnsItem zoneid="rIEsV1lGCZ">

* Sample input script

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3195101d0284447880a5405f55f92f90~tplv-goo7wpa0wc-raw.image" name="full_script.md">full_script.md</Attachment>
   

* Adaptation requirement: Adapt the above Chinese script into a script about an elite American family business.

   ```JSON
   "target_region": "American",
   "target_genre": "wall_street_finance",
   ```
   

</columnsItem>
<columnsItem zoneid="tb5hTSw8eY">

* Outline of the adapted script

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b36baf5e84154ce3bb582e793366760c~tplv-goo7wpa0wc-raw.image" name="outline.md">outline.md</Attachment>
   

* Adapted script

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd274a2ecb614dacaf82610c46858066~tplv-goo7wpa0wc-raw.image" name="full_script.md">full_script.md</Attachment>
   

</columnsItem>
</columns>


<span id="supported-regions"></span>
## Supported regions


* Asia Pacific(Johor)：ap\-southeast\-1


<span id="supported-fission-genres"></span>
## Supported fission genres

LAS provides script fission genres for four target regions: China, the United States, Thailand, and Indonesia. When invoking the operator, you must specify the target region (`target_region`) and target genre (`target_genre`) for fission when submitting the task, and `target_genre` must belong to the selectable set under `target_region`; otherwise, the task cannot be executed normally.

&nbsp;


|Supported target regions (`target_region`) |Supported fission genres (`target_genre`) |Fission genre description |
|---|---|---|
|`Chinese` |`urban_family_identity` |Urban elite identity reversal |
|`Chinese` |`live_commerce_platform` |Live commerce comeback |
|`Chinese` |`ancient_court_identity` |Ancient costume identity reversal |
|`Chinese` |`medical_hospital_system` |Medical workplace drama |
|`Chinese` |`republican_shanghai_business` |Business rivalry in Republican\-era Shanghai |
|`Chinese` |`chinese_entertainment_industry` |Revival of the Chinese entertainment industry |
|`Chinese` |`street_food_entrepreneurship` |Street food entrepreneurship success story |
|`Chinese` |`campus_power_structure` |Campus power reversal |
|`Chinese` |`cultivation_sect_world` |Rise of the cultivation sect |
|`Chinese` |`1990s_business_or_family` |1990s business families |
|`American` |`law_firm_litigation` |American legal drama |
|`American` |`urban_fantasy_pack_or_coven` |Werewolf/vampire urban fantasy |
|`American` |`hollywood_entertainment` |Hollywood reputation crisis |
|`American` |`family_trust_estate` |Family trust inheritance |
|`American` |`wall_street_finance` |Wall Street capital contest |
|`American` |`elite_family_business` |American elite family business |
|`American` |`corporate_workplace` |American corporate workplace turnaround |
|`American` |`us_election_politics` |American election political contest |
|`American` |`1990s_media_and_tabloid` |1990s American traditional media |
|`American` |`ai_platform_corporate_power` |AI platform corporate power |
|`Thai` |`thai_family_conglomerate` |Marriage and romance among Thai elite families |
|`Thai` |`thai_entertainment_industry` |Revival of the Thai entertainment industry |
|`Thai` |`thai_public_reputation_media` |Thai public opinion reputation defense |
|`Thai` |`thai_urban_workplace` |Bangkok workplace turnaround |
|`Thai` |`thai_supernatural_family_conglomerate` |Thai\-style supernatural fated elite families |
|`Thai` |`thai_medical_hospital_system` |Thai satisfying medical workplace drama |
|`Thai` |`thai_legal_litigation` |Thai legal drama |
|`Thai` |`thai_live_commerce_platform` |Thai live commerce turnaround |
|`Thai` |`thai_family_estate_inheritance` |Thai family estate inheritance |
|`Thai` |`thai_food_local_business` |Thai local food and beverage entrepreneurship |
|`Indonesia` |`indonesia_preserve_original` |Indonesia preserve original genre |


<span id="operator-performance"></span>
## Operator performance

&nbsp;


|Subcategory |Performance impact description |
|---|---|
|Maximum RPM |600 |
|Maximum concurrency |10 |


<span id="input-and-output-requirements"></span>
# Input and output requirements

<span id="input-requirements"></span>
## Input requirements

&nbsp;


|Subcategory |Detailed requirements |
|---|---|
|Input data modality |Text |
|Input format: text |* Format: supports `Markdown`, `TXT`<br><br>* Each task supports input of one or more script files<br><br>* The total number of words in the input scripts must not exceed 600,000<br><br>* Other: Ensure that the input episodic scripts are complete; missing episodes, disorder, or missing key plot segments may cause task failure. |
|Input path requirements |Provide operator input data via request parameter `episodes_script_dir` or `episodes_script_list` (choose one; when both are provided, `episodes_script_dir` has higher priority). Currently, two methods are supported: public URL and TOS path.<br><br><br>* Public URL: a publicly accessible URL, format is `http/https`. `episodes_script_dir` input parameter is not supported.<br><br>   * Public URLs that require login status or additional header authentication are not supported; temporary URLs must be valid during task execution.<br><br>* TOS path: Upload the data to be processed to the TOS Bucket under the same primary account and region as the current LAS service, then provide the TOS path in the format `tos://bucket_name/demo`.<br><br>   * The TOS object must exist and have read permissions. |


<span id="output-requirements"></span>
## Output requirements

&nbsp;


|Subcategory |Detailed requirements |
|---|---|
|Output data modality |Text (script Markdown file) |
|Output path: TOS |Specify the operator output result storage path via request parameter `output_tos_path`; currently, setting to TOS path is supported.<br><br>TOS path: The TOS Bucket directory with write permissions, under the same primary account and region as the LAS service. Format: `tos://bucket/output/`. |


<span id="billing-instructions"></span>
# Billing instructions


* Billing standard

&nbsp;

   
   |Item |Billing standard description |
   |---|---|
   |Billing items |There are two billing items: **model input, model output**. The total fee payable is the sum of the fees for all billing items.<br><br><br>* After the process completes the task, you can view the model's token usage in the result returned by the poll interface.<br><br>* `token_usage.prompt_tokens`: Token usage for model input.<br><br>* `token_usage.completion_tokens`: Token usage for model output. |
   |Billing type |Pay\-as\-you\-go, unit: `USD per million tokens`, billed hourly based on actual usage. |
   |Unit price |The unit prices for **model input and model output** are different.<br><br><br>* Input: 1.25 USD per million tokens<br><br>* Output: 7.5 USD per million tokens |
   


<span id="caution-and-prerequisites"></span>
# Caution and prerequisites

&nbsp;


|Details |Caution and prerequisites |
|---|---|
|Costs |Before calling an operator, you need to understand the model invocation costs associated with using the operator. For details, see [Large model billing](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |


<span id="rest-api-invocation"></span>
# Rest API invocation

<span id="api-call-instructions"></span>
## API call instructions


* This operator's API is an asynchronous task interface. Submit a task through the `Submit` interface to obtain the `task_id`. Then use the `Poll` interface to check the status of the corresponding task (`task_id`) and retrieve the operator's processing result.

* Caution: After a task is submitted, the `task_id` is valid for 3 days. After 3 days, the `task_id` cannot be used to retrieve the operator's processing result.


<span id="submit"></span>
## Submit

<span id="interface-description"></span>
### Interface description

Submit the `las_short_drama_script_fission` operator to perform a short drama script fission task. After successful submission, a task ID is returned. You can obtain the fission script results via the query interface.

<span id="request-parameters"></span>
### Request parameters



**operator_id** <span data-label="purple">string</span> <span data-api-tag="require|GMqZDY">必选</span> `Example value: las_short_drama_script_fission`

Operator ID



**operator_version** <span data-label="purple">string</span> <span data-api-tag="require|O0rg2S">必选</span> `Example value: v1`

Operator version. Currently only `v1` is supported.



**data** <span data-label="purple">ShortDramaScriptFissionReqParams</span> <span data-api-tag="require|QGJlnI">必选</span>

Operator request parameters


**episodes_script_dir** <span data-label="purple">string</span> `Example value: tos://bucket/scripts/`

Source episode\-script directory. Only `tos://` is supported. The directory must contain complete episode scripts named in order, such as `ep001.md` and `ep002.txt`. The total input script length must not exceed 600,000 Chinese characters. This field is mutually exclusive with `episodes_script_list`; if both are provided, this field takes precedence.



**episodes_script_list** <span data-label="purple">list of string</span> `Example value: ["tos://bucket/ep001.md", "tos://bucket/ep002.txt"]`

Source episode\-script path list. The list must not contain more than 1,000 items. Supports `tos://`, `http://`, and `https://`. This field is mutually exclusive with `episodes_script_dir`. The caller must ensure the list order matches the episode order, the input script is complete, and the total input script length does not exceed 600,000 Chinese characters.



**target_region** <span data-label="purple">string</span> <span data-api-tag="require|eDeU2m">必选</span> `Example value: American`

Target region. Currently supported values are `Chinese`, `American`, `Thai`, and `Indonesia`.



**target_genre** <span data-label="purple">string</span> <span data-api-tag="require|ZgUjYs">必选</span> `Example value: law_firm_litigation`

Target genre. It must match the supported genre set under the selected `target_region`.



**output_tos_path** <span data-label="purple">string</span> <span data-api-tag="require|cAqCHD">必选</span> `Example value: tos://bucket/fission_output/`

Output directory for rewritten results. Episode scripts, the full script, the outline, and the mapping file are written under this directory.




&nbsp;

<span id="response-parameters"></span>
### Response parameters


**metadata** <span data-label="purple">metadata</span>

Request metadata


**task_id** <span data-label="purple">string</span> `Example value: fission-abc123`

Task ID in asynchronous mode, used for job status queries.



**task_status** <span data-label="purple">string</span> `Example value: PENDING`

Task status in asynchronous mode. `PENDING`: Request received, `RUNNING`: Running, `COMPLETED`: Completed, `FAILED`: Failed, `TIMEOUT`: Timed out.



**business_code** <span data-label="purple">string</span> `Example value: 0`

Business code.



**error_msg** <span data-label="purple">string</span>

If an exception occurs, detailed exception information will be returned.



&nbsp;

<span id="example"></span>
### Example

**Request example**

```Bash
# Set INPUT_SCRIPT_DIR to the TOS directory containing episode scripts
export INPUT_SCRIPT_DIR="tos://bucket/scripts/"
# Set OUTPUT_TOS_PATH to the TOS directory writable by this account
export OUTPUT_TOS_PATH="tos://bucket/fission_output/"

curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_short_drama_script_fission",
    "operator_version": "v1",
    "data": {
        "episodes_script_dir": "$INPUT_SCRIPT_DIR",
        "target_region": "American",
        "target_genre": "law_firm_litigation",
        "output_tos_path": "$OUTPUT_TOS_PATH"
    }
}'
```


**Response example**

```JSON
{
  "metadata": {
    "task_id": "fission-abc123",
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
|400 |MISSING_REQUIRED_PARAMETER |Missing required parameter. |Missing required parameters, such as `target_region`, `target_genre`, `output_tos_path`, or neither `episodes_script_dir` nor `episodes_script_list` is provided. |
|400 |INVALID_PARAMETER |Invalid parameter. |Invalid parameter, such as unsupported input path protocol, unsupported script format, or genre not matching the target region. |
|400 |TOS_ACCESS_FAILED |TOS access failed. |TOS path access failed or credentials are missing. |
|400 |TASK_INPUT_INVALID |Invalid input script. |Missing episode scripts, abnormal order, or the provided content is not a valid script. |
|400 |VLM_CALL_FAILED |VLM call failed. |Model call failed. |
|401 |Authorization.Missing |Missing Authorization. |Authorization is missing. |
|401 |ApiKey.InValid |The api key is invalid. |API Key is invalid. |
|500 |Internal.ServerError |Internal server error. |Internal service error. |


<span id="poll"></span>
## Poll

<span id="interface-description-1"></span>
### Interface description

Query the execution status and results of the short drama script fission task. After the task is completed, you can obtain the fissioned full series script, outline, episode script directory, mapping table, and other results.

<span id="request-parameters-1"></span>
### Request parameters



**operator_id** <span data-label="purple">string</span> <span data-api-tag="require|RqjyZk">必选</span> `Example value: las_short_drama_script_fission`

Operator ID.



**operator_version** <span data-label="purple">string</span> <span data-api-tag="require|JH5ECz">必选</span> `Example value: v1`

Operator version.



**task_id** <span data-label="purple">string</span> <span data-api-tag="require|ydOoPU">必选</span> `Example value: fission-abc123`

The task ID returned by the Submit API.



&nbsp;

<span id="response-parameters-1"></span>
### Response parameters



**metadata** <span data-label="purple">metadata</span>

Request metadata


**task_id** <span data-label="purple">string</span> `Example value: fission-abc123`

Task ID.



**task_status** <span data-label="purple">string</span> `Example value: COMPLETED`

Task status. `PENDING`: Request received, `RUNNING`: Running, `COMPLETED`: Completed, `FAILED`: Failed, `TIMEOUT`: Timed out.



**submit_time** <span data-label="purple">string</span> `Example value: 2026-07-27T19:30:00+08:00`

Task submission time, in ISO 8601 timestamp format.



**end_time** <span data-label="purple">string</span> `Example value: 2026-07-27T19:42:00+08:00`

Task end time, in ISO 8601 timestamp format.



**business_code** <span data-label="purple">string</span> `Example value: 0`

Business code.



**error_msg** <span data-label="purple">string</span>

If an exception occurs, detailed exception information will be returned.




**data** <span data-label="purple">ShortDramaScriptFissionResponse</span>

Returned data


**title** <span data-label="purple">string</span> `Example value: Pact of the Mountain Glass`

Title of the script after fission.



**total_episodes** <span data-label="purple">integer</span> `Example value: 5`

Total number of episodes after fission.



**target_region** <span data-label="purple">string</span> `Example value: american`

The actual target region executed.



**target_genre** <span data-label="purple">string</span> `Example value: urban_fantasy_pack_or_coven`

The actual target genre executed.



**outline_path** <span data-label="purple">string</span> `Example value: tos://bucket/fission_output/task-xxx/outline.md`

Outline file path of the script after fission.



**full_script_path** <span data-label="purple">string</span> `Example value: tos://bucket/fission_output/task-xxx/full_script.md`

Full script path after fission.



**fission_episodes_script_dir** <span data-label="purple">string</span> `Example value: tos://bucket/fission_output/task-xxx/episodes/`

Directory for saving episode scripts after fission. The directory usually contains files such as `ep001.md`, `ep002.md` and more.



**mapping_path** <span data-label="purple">string</span> `Example value: tos://bucket/fission_output/task-xxx/mapping.json`

Mapping file path before and after fission.



**token_usage** <span data-label="purple">TokenUsage</span> `Example value: {"prompt_tokens":416893,"completion_tokens":51708,"total_tokens":468601}`

Token usage details.


**prompt_tokens** <span data-label="purple">integer</span> `Example value: 416893`

Number of input tokens.



**completion_tokens** <span data-label="purple">integer</span> `Example value: 51708`

Number of output tokens.



**total_tokens** <span data-label="purple">integer</span> `Example value: 468601`

Total number of input and output tokens.





&nbsp;

<span id="example-1"></span>
### Example

<span id="request-example"></span>
#### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_short_drama_script_fission",
    "operator_version": "v1",
    "task_id": "06ecbd66031e7006022d"
}'
```


<span id="response-example"></span>
#### Response example

```JSON
{
  "metadata": {
    "task_id": "06ecbd66031e7006022d",
    "task_status": "COMPLETED",
    "submit_time": "2026-07-27T19:30:00+08:00",
    "end_time": "2026-07-27T19:42:00+08:00",
    "business_code": "0",
    "error_msg": ""
  },
  "data": {
    "title": "Pact of the Mountain Glass",
    "total_episodes": 5,
    "target_region": "american",
    "target_genre": "urban_fantasy_pack_or_coven",
    "outline_path": "tos://bucket/fission_output/task-xxx/outline.md",
    "full_script_path": "tos://bucket/fission_output/task-xxx/full_script.md",
    "fission_episodes_script_dir": "tos://bucket/fission_output/task-xxx/episodes/",
    "mapping_path": "tos://bucket/fission_output/task-xxx/mapping.json",
    "token_usage": {
      "prompt_tokens": 416893,
      "completion_tokens": 51708,
      "total_tokens": 468601
    }
  }
}
```


<span id="error-codes-1"></span>
### Error codes

&nbsp;


|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Missing |Missing required parameter. |Required parameter is missing. |
|400 |Parameter.Invalid |Invalid parameter. |Invalid parameter. |
|400 |Task.NotFound |Task not found. |Task does not exist. |
|401 |Authorization.Missing |Missing Authorization. |Authorization is missing. |
|401 |ApiKey.InValid |The api key is invalid. |API Key is invalid. |
|500 |Internal.ServerError |Internal server error. |Internal service error. |
