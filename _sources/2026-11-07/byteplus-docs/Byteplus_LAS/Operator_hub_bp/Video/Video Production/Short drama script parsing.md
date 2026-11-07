---
title: "Short drama script parsing"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Short_drama_script_parsing"
---

The short drama script asset parsing operator converts multilingual scripts into structured asset tables. It reads one or more script files, automatically detects the script language and structure, extracts character, prop, and scene assets, and enriches them with visual descriptions.

<span id="operator-introduction"></span>
# Operator introduction

> Operator ID: las_short_drama_script_parse


<span id="applicable-scenarios"></span>
## Applicable scenarios


* **Short drama asset breakdown**: Quickly generate lists of characters, props, and scenes from scripts to support production, art, costume, makeup, and props, and visual asset planning.

* **Preprocessing for text\-to\-image/text\-to\-video**: Decompose script text into reusable structured visual assets for character styling, scene generation, and shot generation.

* **Multi\-episode script asset merging**: Parse multiple short drama episodes in a unified manner, merge duplicate assets across episodes, and form a series\-level asset table.

* **Overseas content localization**: Supports multilingual script parsing with English asset table output for non\-Chinese languages, streamlining global short drama production and localization workflows.

* **Cost and scale evaluation**: Returns token consumption aggregated by model to assist in estimating the cost of parsing large scripts.


<span id="core-capabilities"></span>
## Core capabilities


* **Multi\-script input parsing**: Supports input of one or more script files, concatenated and processed in input order, suitable for single\-episode, multi\-episode, or full\-series script parsing.

* **Character asset table extraction**: Identifies character names, gender, basic appearance, and scenes in which the character appears, and supplements main characters with multiple styling descriptions consistent with the script background.

* **Prop asset table extraction**: Identify key props, the scene positions where they appear in the series, visual characteristics, and changes in prop status to assist prop design and asset management.

* **Scene asset table extraction**: Identifies main scenes, spatial types, time settings, atmosphere, and visual arrangements to assist with scene construction and storyboard generation.

* **Multilingual parsing**: Automatically detects the source language. Chinese scripts produce Chinese asset tables, while scripts in other languages (English, Thai, Vietnamese, Korean, Japanese, Indonesian, and more) produce English asset tables. Proper character names and Latin\-script scene names are kept verbatim, while generic scene/prop labels and descriptions are translated into English.

* **Robust processing of ultra\-long scripts**: Automatically splits scripts exceeding the threshold by scene boundaries to reduce the risk of timeout and truncation caused by excessively long context requests.

* **TOS asset delivery**: Writes the character table, prop table, scene table, script context, complete normalized script, and per\-episode scripts to TOS and returns their paths.


<span id="results-demonstration"></span>
## Results demonstration


* **Script input:** 



<columns>
<columnsItem zoneid="t2C794Ep7E">

* Typically, the input script only contains the core plot and simple descriptions of relevant characters or environments. For example:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39caa87428964301b4854d7472be63d6~tplv-goo7wpa0wc-topic.webp) </span>

</columnsItem>
<columnsItem zoneid="O0BNZVxtSU">

Supports input of multi\-episode scripts; the following are two input examples.


* Episode 1

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3358dca1a2544fd5afc50888df40c7a7~tplv-goo7wpa0wc-raw.image" name="ep_001.md">ep_001.md</Attachment>
   

* Episode 2

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01afd727be7b49c299ccfb94ddc6829f~tplv-goo7wpa0wc-raw.image" name="ep_002.md">ep_002.md</Attachment>
   

</columnsItem>
</columns>



* **Script analysis results:** 



<columns>
<columnsItem zoneid="yFs0Yp4gJE">

* Character asset table:

   Based on the global script, aggregate the character list, record character gender and the episodes in which the character appears, and expand and supplement with details such as character appearance and styling as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b79eaf83018944288c0817024e848a9a~tplv-goo7wpa0wc-topic.webp) </span>

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6bb1a095691044aeb7bbdfd9864d8ae2~tplv-goo7wpa0wc-raw.image" name="character_table.json">character_table.json</Attachment>
   

</columnsItem>
<columnsItem zoneid="G6F9NbXWyS">

* Prop asset table:

   Based on the global script, aggregate the prop list, record the status changes of props, and expand and supplement with details on the appearance characteristics of props as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d00331c242944ed2a74a7b20768789c9~tplv-goo7wpa0wc-topic.webp) </span>

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b50fb44f2b954538814f09319a722dc1~tplv-goo7wpa0wc-raw.image" name="prop_table.json">prop_table.json</Attachment>
   

</columnsItem>
<columnsItem zoneid="N2k3vpsIey">

* Scene asset table:

   Based on the global script, aggregate the scene list, and expand and supplement with details such as the spatial type and time status of the scene as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39bba11cc4404850877edb013f40b8a7~tplv-goo7wpa0wc-topic.webp) </span>

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/45d55c22f8114cc1ba0806208b39d484~tplv-goo7wpa0wc-raw.image" name="scene_table.json">scene_table.json</Attachment>
   

</columnsItem>
</columns>


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


<span id="input-and-output-requirements"></span>
# Input and output requirements

<span id="input-requirements"></span>
## Input requirements

&nbsp;


|Sub\-item |Detailed requirements |
|---|---|
|Input data modality |Text |
|Input format: Text |* Format: Supports Markdown, TXT<br><br>* Quantity: Each task supports inputting one or more script files<br><br>* Script content style: Script content must use UTF\-8 encoding, and the content cannot be empty. Multilingual scripts are supported. Chinese scripts produce Chinese asset tables, while scripts in other languages produce English asset tables; for more requirements, please refer to [Reference 1: Script input content style requirements](https://docs.byteplus.com/en/docs/297/117688#reference-1:-script-input-content-style-requirements).<br><br>* Other: When the input script is too long, causing the input length to the operator model to exceed the LAS threshold (200,000 characters), the operator will split by scene boundaries and merge the asset tables in the output. |
|Input path requirements |Provide input data to the operator via the `script_urls` request parameter. Currently, two methods are supported: public URL and TOS path.<br><br><br>* Public URL: A publicly accessible URL in the format `http/https`.<br><br>   * Public URLs that require login status or additional header authentication are not supported; temporary URLs must remain valid during task execution.<br><br>* TOS path: After uploading the data to be processed to the TOS Bucket under the same primary account and region as the current LAS service, you can provide the file address under the TOS path in the format `tos://bucket_name/ demo.md`.<br><br>   * The TOS object must exist and have read permissions. |


<span id="output-requirements"></span>
## Output requirements

&nbsp;


|Sub\-item |Detailed requirements |
|---|---|
|Output data modality |* Text<br><br>* Format: JSON |
|Output path: TOS |You can specify the storage path for the operator's output results via the request parameter `output_tos_path`. Currently, setting a TOS path is supported.<br><br>TOS path: A writable TOS Bucket directory under the same primary account and region as the LAS service. Format: `tos://bucket/output/`. |
|Output path: Presigned URL |If you do not configure the `output_tos_path` parameter, after the task completes, the generated result will be returned via a presigned link. You can click the corresponding link to download directly. The link is valid for 11 hours. |


<span id="billing-information"></span>
# Billing information


* Billing standards

&nbsp;

   
   |Sub\-items |Billing standard description |
   |---|---|
   |Billing items |There are two billing items: **model input, model output**. The total fee payable is the sum of all billing items.<br><br><br>* The model's token usage can be viewed in the result returned by the poll interface after the operator completes the task.<br><br>* `token_usage.prompt_tokens`: Token usage for model input.<br><br>* `token_usage.completion_tokens`: Token usage for model output. |
   |Billing type |Usage\-based billing, unit: `USD/million tokens`, billed hourly based on actual usage. |
   |Unit price |The unit prices for **model input, model output** are different.<br><br><br>* Input: 1.25 USD/million Tokens<br><br>* Output: 6.25 USD/million Tokens |
   


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


* This operator's API is an asynchronous task interface. Submit a task through the `Submit` interface to obtain the `task_id`. Then use the `Poll` interface to check the status of the corresponding task (`task_id`) and retrieve the operator's processing result.

* Caution: After a task is submitted, the `task_id` is valid for 3 days. After 3 days, the `task_id` cannot be used to retrieve the operator's processing result.


<span id="submit"></span>
## Submit

<span id="interface-description"></span>
### Interface description

Submit the las_short_drama_script_parse operator to parse assets from a multilingual short drama script. The operator automatically detects the script language and structure and normalizes Chinese script formatting.

<span id="request-parameters"></span>
### Request parameters



**operator_id** <span data-label="purple">string</span> <span data-api-tag="require|FhxYZb">必选</span> `Example value: las_short_drama_script_parse`

Operator ID.



**operator_version** <span data-label="purple">string</span> <span data-api-tag="require|UOLbT8">必选</span> `Example value: v1`

Operator version. Only v1 is supported currently.



**data** <span data-label="purple">ShortDramaScriptParseReqParams</span> <span data-api-tag="require|ydpTz6">必选</span>

Operator parameters.


**script_urls** <span data-label="purple">list of string</span> <span data-api-tag="require|BwPEVs">必选</span> `Example value: ["tos://bucket/scripts/demo.md"]`

List of multilingual script file URLs. `http`, `https`, and BytePlus TOS (`tos://bucket/key`) are supported. Multiple files are concatenated in the submitted order. The concatenated input is limited to 1,000,000 characters and 1,000 episodes.



**output_tos_path** <span data-label="purple">string</span> `Example value: tos://bucket/output/script_parse/`

TOS directory where results will be saved. If not provided, results will be written to the LAS internal bucket and presigned URLs will be returned.




&nbsp;

<span id="response-parameters"></span>
### Response parameters


**metadata** <span data-label="purple">metadata</span>

Request metadata.


**task_id** <span data-label="purple">string</span> `Example value: task-xxx`

Task ID in asynchronous mode, used for job status queries.



**task_status** <span data-label="purple">string</span> `Example value: PENDING`

Asynchronous task status.


* PENDING: Request received

* RUNNING: Running

* COMPLETED: Completed

* FAILED: Failed

* TIMEOUT: Timed out



**business_code** <span data-label="purple">string</span> `Example value: 0`

Business code.



**error_msg** <span data-label="purple">string</span>

If an exception occurs, detailed exception information will be returned.



&nbsp;

<span id="example"></span>
### Example

**Request example**

```Bash
# Please set INPUT_PATH to an accessible script file path
export INPUT_PATH="tos://bucket/scripts/demo_script.md"
# Please set OUTPUT_PATH to a writable TOS output directory
export OUTPUT_PATH="tos://bucket/output/script_parse/"

curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data @- <<EOF
{
    "operator_id": "las_short_drama_script_parse",
    "operator_version": "v1",
    "data": {
        "script_urls": ["$INPUT_PATH"],
        "output_tos_path": "$OUTPUT_PATH"
    }
}
EOF
```


**Response example**

```JSON
{
  "metadata": {
    "task_id": "task-20260724130000-abc123",
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
|400 |Parameter.Invalid |invalid parameter |Invalid parameter, such as `script_urls` being empty, URL protocol not being `http`/`https`/`tos`, or other input parameters out of range. |
|400 |Parameter.Missing |Missing required parameter |Missing required parameter, such as missing `script_urls`; or when the input contains `tos://` or `output_tos_path` is specified, the customer TOS credential is missing. |
|400 |Tos.AccessFailed |Failed to access TOS path with provided credentials |Failed to access TOS path or invalid credentials. |
|400 |DramaScript.Invalid |invalid drama script |Invalid script file, such as non\-UTF\-8 text, empty content, or unparseable. |
|400 |DramaScript.TooLong |drama script exceeds maximum character count |The concatenated script exceeds 1,000,000 characters. |
|400 |DramaScript.TooManyEpisodes |drama script exceeds maximum episode count |The script contains more than 1,000 episodes. |
|400 |DramaScript.NoBeat |no valid beat found in drama script |No valid beat identified in the script. |
|400 |DramaScript.ExtractEmpty |script asset extraction returned empty result |Asset extraction result is empty; no characters, props, or scenes were extracted. |
|400 |DramaScript.LLMTruncated |LLM output was truncated |Model output was truncated (`finish_reason=length`). |
|400 |DramaScript.LLMFailed |LLM call failed during drama script parsing |Model call failed during script parsing. |
|401 |Authorization.Missing |Missing Authorization. |Missing authorization. |
|401 |ApiKey.InValid |The api key is invalid. |API Key is invalid. |
|500 |InternalError |Internal error |Internal service error. |


<span id="poll"></span>
## Poll

<span id="interface-description-1"></span>
### Interface description

Query the execution status and results of a short drama script asset parsing task.

<span id="request-parameters-1"></span>
### Request parameters



**operator_id** <span data-label="purple">string</span> <span data-api-tag="require|9Dkwlh">必选</span> `Example value: las_short_drama_script_parse`

Operator ID.



**operator_version** <span data-label="purple">string</span> <span data-api-tag="require|gylUg6">必选</span> `Example value: v1`

Operator version.



**task_id** <span data-label="purple">string</span> <span data-api-tag="require|d85PGG">必选</span> `Example value: task-xxx`

Task ID returned by the Submit API.



&nbsp;

<span id="response-parameters-1"></span>
### Response parameters



**metadata** <span data-label="purple">metadata</span>

Request metadata.


**task_status** <span data-label="purple">string</span> `Example value: COMPLETED`

Task status.


* PENDING: Request received

* RUNNING: Running

* COMPLETED: Completed

* FAILED: Failed

* TIMEOUT: Timeout



**submit_time** <span data-label="purple">string</span> `Example value: 2026-07-24T13:00:00+08:00`

Task submission time. The format is an ISO 8601 timestamp.



**end_time** <span data-label="purple">string</span> `Example value: 2026-07-24T13:05:00+08:00`

Task end time. The format is an ISO 8601 timestamp.



**business_code** <span data-label="purple">string</span> `Example value: 0`

Business code.



**error_msg** <span data-label="purple">string</span>

If an exception occurs, detailed exception information will be returned.



**task_id** <span data-label="purple">string</span> `Example value: task-xxx`

Asynchronous task ID.




**data** <span data-label="purple">ShortDramaScriptParseResponse</span>

The parsing result is returned when task_status is COMPLETED.


**script_char_count** <span data-label="purple">integer</span> `Example value: 60702`

Total character count of the input script. For multiple files, this is the character count after concatenation.



**character_count** <span data-label="purple">integer</span> `Example value: 6`

Number of character asset entries.



**prop_count** <span data-label="purple">integer</span> `Example value: 5`

Number of prop asset entries.



**scene_count** <span data-label="purple">integer</span> `Example value: 10`

Number of scene asset entries.



**artifacts** <span data-label="purple">Artifacts</span>

Artifact paths and pre\-signed URLs.


**character_table_path** <span data-label="purple">string</span> `Example value: tos://bucket/output/character_table.json`

TOS path of the character asset table JSON.



**prop_table_path** <span data-label="purple">string</span> `Example value: tos://bucket/output/prop_table.json`

TOS path of the prop asset table JSON.



**scene_table_path** <span data-label="purple">string</span> `Example value: tos://bucket/output/scene_table.json`

TOS path of the scene asset table JSON.



**script_context_path** <span data-label="purple">string</span> `Example value: tos://bucket/output/script_context.json`

TOS path of the script background information JSON. Includes: script genre, historical background, ethnicity, region, and other information. This serves as input for operators to expand character appearance, prop descriptions, and scene outputs, ensuring that all expanded content aligns with the script background.



**normalized_script_path** <span data-label="purple">string</span> `Example value: tos://bucket/output/normalized_script.md`

TOS path of the complete normalized script Markdown.



**episode_scripts_dir_path** <span data-label="purple">string</span> `Example value: tos://bucket/output/episodes`

TOS directory containing per\-episode scripts.



**episode_script_paths** <span data-label="purple">list of string</span> `Example value: ["tos://bucket/output/episodes/episode_001.md"]`

TOS paths of per\-episode Markdown scripts, ordered by episode number.



**character_table_url** <span data-label="purple">string</span> `Example value: https://example.com/character_table.json`

If the output_tos_path request parameter is not configured when submitting the task, after the task is completed, the generated result will be returned via a pre\-signed link. You can click the corresponding link to download directly. The link is valid for 11 hours. This parameter is the pre\-signed URL for the character asset table.



**prop_table_url** <span data-label="purple">string</span> `Example value: https://example.com/prop_table.json`

If the output_tos_path request parameter is not configured when submitting the task, after the task is completed, the generated result will be returned via a pre\-signed link. You can click the corresponding link to download directly. The link is valid for 11 hours. This parameter is the pre\-signed URL for the prop asset table.



**scene_table_url** <span data-label="purple">string</span> `Example value: https://example.com/scene_table.json`

If the output_tos_path request parameter is not configured when submitting the task, after the task is completed, the generated result will be returned via a pre\-signed link. You can click the corresponding link to download directly. The link is valid for 11 hours. This parameter is the pre\-signed URL for the scene asset table.



**script_context_url** <span data-label="purple">string</span> `Example value: https://example.com/script_context.json`

If the output_tos_path request parameter is not configured when submitting the task, after the task is completed, the generated result will be returned via a pre\-signed link. You can click the corresponding link to download directly. The link is valid for 11 hours. This parameter is the pre\-signed URL for the script background information.



**normalized_script_url** <span data-label="purple">string</span> `Example value: https://example.com/normalized_script.md`

Presigned URL of the complete normalized script, returned only when writing to the internal bucket.



**episode_script_urls** <span data-label="purple">list of string</span> `Example value: ["https://example.com/episodes/episode_001.md"]`

Presigned URLs of per\-episode scripts, returned only when writing to the internal bucket.




**token_usages** <span data-label="purple">list of ModelTokenUsage</span>

Token consumption aggregated by model.


**token_usage** <span data-label="purple">TokenUsage</span>

Token consumption details.


**prompt_tokens** <span data-label="purple">integer</span> `Example value: 100000`

Number of input tokens.



**completion_tokens** <span data-label="purple">integer</span> `Example value: 20000`

Number of output tokens.



**total_tokens** <span data-label="purple">integer</span> `Example value: 120000`

Total number of input and output tokens.






&nbsp;

<span id="example-1"></span>
### Example

**Request example**

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_short_drama_script_parse",
    "operator_version": "v1",
    "task_id": "task-20260724130000-abc123"
}'
```


**Response example**

```JSON
{
  "metadata": {
    "task_id": "task-20260724130000-abc123",
    "task_status": "COMPLETED",
    "submit_time": "2026-07-21T16:04:06+08:00",
    "end_time": "2026-07-21T16:04:06+08:00",
    "business_code": "0",
    "error_msg": ""
  },
  "data": {
    "script_char_count": 60702,
    "character_count": 6,
    "prop_count": 5,
    "scene_count": 10,
    "artifacts": {
      "character_table_path": "tos://bucket/output/character_table.json",
      "prop_table_path": "tos://bucket/output/prop_table.json",
      "scene_table_path": "tos://bucket/output/scene_table.json",
      "script_context_path": "tos://bucket/output/script_context.json",
      "normalized_script_path": "tos://bucket/output/normalized_script.md",
      "episode_scripts_dir_path": "tos://bucket/output/episodes",
      "episode_script_paths": [
        "tos://bucket/output/episodes/episode_001.md"
      ]
    },
    "token_usages": [
      {
        "token_usage": {
          "prompt_tokens": 100000,
          "completion_tokens": 20000,
          "total_tokens": 120000
        }
      }
    ]
  }
}
```


<span id="error-code-1"></span>
### Error code

&nbsp;


|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |invalid parameter |Invalid parameter, such as `script_urls` being empty, URL protocol not being `http`/`https`/`tos`, or other input parameters out of range. |
|400 |Parameter.Missing |Missing required parameter |Missing required parameter, such as missing `script_urls`; or when the input contains `tos://` or `output_tos_path` is specified, the customer TOS credential is missing. |
|400 |Tos.AccessFailed |Failed to access TOS path with provided credentials |Failed to access TOS path or invalid credentials. |
|400 |DramaScript.Invalid |invalid drama script |Invalid script file, such as non\-UTF\-8 text, empty content, or unparseable. |
|400 |DramaScript.TooLong |drama script exceeds maximum character count |The concatenated script exceeds 1,000,000 characters. |
|400 |DramaScript.TooManyEpisodes |drama script exceeds maximum episode count |The script contains more than 1,000 episodes. |
|400 |DramaScript.NoBeat |no valid beat found in drama script |No valid beat identified in the script. |
|400 |DramaScript.ExtractEmpty |script asset extraction returned empty result |Asset extraction result is empty; no characters, props, or scenes were extracted. |
|400 |DramaScript.LLMTruncated |LLM output was truncated |Model output was truncated (`finish_reason=length`). |
|400 |DramaScript.LLMFailed |LLM call failed during drama script parsing |Model call failed during script parsing. |
|401 |Authorization.Missing |Missing Authorization. |Missing authorization. |
|401 |ApiKey.InValid |The api key is invalid. |API Key is invalid. |
|500 |InternalError |Internal error |Internal service error. |


<span id="reference"></span>
# Reference

<span id="reference-1:-script-input-content-style-requirements"></span>
## Reference 1: Script input content style requirements

<span id="general-format-requirements"></span>
#### General format requirements

When entering script content, each scene must include a separate scene marker line. The basic format is:

```Plain
X-Y 场次描述
```


This format does not restrict the language of the main text, for example `1-1 日 外 秦岭山中` and `1-1 INT.` `OFFICE - DAY` can also be recognized.


* Detailed format requirements

   * `X` represents the episode number, `Y` represents the scene number within the episode, each consisting of 1 to 3 digits.

   * Only the half\-width hyphen `-` or underscore `_` is supported as a separator between episode and scene numbers.

   * Spaces may be present on both sides of the separator, for example `1 - 2`.

   * If there is a scene description after the scene number, it must be separated by a space, for example `1-1 日 外 山中`; if the number is on a line by itself, you can simply start a new line.

   * The scene marker must be on a separate line and written as close to the left margin as possible; if indentation is needed, a maximum of 3 spaces can be kept at the beginning of the line.

   * Before the number, you may add `#`, `##`, `###`, `Scene number:`, or `场号：`, for example `### 1-1 日 外 山中`.

* Content example

   ```Markdown
   # 第 1 集剧本
   
   ## 正文剧本
   
   ## 1-1 内景 航空管制中心大厅 日
   
   出场人物：苏星晚、陆霆川
   
   △ 冷光灯照亮航空管制中心大厅，墙面上的多块监测屏幕显示着航班轨迹、气象雷达等信息，苏星晚身着藏青色空管制服坐在管制台的黑色办公椅上，视线看向前方屏幕。
   
   苏星晚（神色严肃）：中南8562，前方两公里强雷雨回波，立即右转航道120，否则有坠毁风险！
   ……
   ```
   


<span id="english-hollywood/fountain-format"></span>
#### English Hollywood/Fountain format

English scripts can use the above `X-Y` episode\-scene numbering format, or identify scenes via Hollywood/Fountain slug lines.


* Detailed format requirements

   * Supports `INT.`, `EXT.`, `EST.`, `I/E.`, `INT./EXT.` and `EXT./INT.`.

   * Scene type is not case\-sensitive, periods may be omitted, but standard notation is recommended.

   * There must be a space and a non\-empty scene description after the scene type.

   * When using the Hollywood/Fountain format and automatic recognition by the operator, the script should contain at least two valid English scene headings.

   * Supports `EPISODE 1`, `EP.` `2`, `EP 3` and other episode titles.

   * If there is no episode title, the entire English script will be regarded as episode 1, and scene numbers will be automatically generated in order of appearance.

* Content example

   ```Markdown
   EPISODE 1
   
   INT. COFFEE SHOP - DAY
   Sarah sits beside the window, holding a red notebook.
   
   SARAH
   We need to leave before noon.
   
   EXT./INT. CAR - NIGHT
   John starts the engine and checks the rear-view mirror.
   ```
   


<span id="reference:-explanation-of-fields-in-the-analysis-result-table"></span>
## Reference: Explanation of fields in the analysis result table

After the operator completes the task, tables for characters, props, scenes, and script background assets will be generated. The explanations for the corresponding table fields are as follows.

&nbsp;


|Field name |Character asset table |Prop asset table |Scene asset table |
|---|---|---|---|
|`id` |The unique identifier of the character in the current table |The unique identifier of the prop in the current table |The unique identifier of the scene in the current table |
|`name` |Character name |Prop name |Scene name |
|`gender` |Character gender |Not applicable |Not applicable |
|`location` |Not applicable |Not applicable |The coarse\-grained main location to which the scene belongs |
|`appearance`/`description` |Basic description of the character's appearance and image |Description of the prop's appearance features or basic default state |Description of the scene environment, spatial structure, visual arrangement, and more |
|`makeups` |Description of the character's clothing, makeup, and age group |Description of prop status changes |Description of scene time period, state, or variations in atmosphere |
|`occur_beats` |The scene numbers in which the character appears, in the format `beat_X_Y` |The scene numbers in which the prop appears, in the format `beat_X_Y` |The scene numbers in which the scene appears, in the format `beat_X_Y` |
|`total_count` |Total number of characters |Total number of props |Total number of scenes |
|`version` |Schema version |Schema version |Schema version |
