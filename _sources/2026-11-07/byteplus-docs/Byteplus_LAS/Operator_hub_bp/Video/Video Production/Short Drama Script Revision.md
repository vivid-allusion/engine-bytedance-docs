---
title: "Short Drama Script Revision"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Short_drama_script_revision"
---

The Short Drama Script Revision operator performs controlled, explainable local revisions on an existing short drama generation result. It reads the TOS directory produced by `las_short_drama_script_gen`, applies the submitted revision instruction to the global character, scene, and prop tables, updates episode Markdown scripts and optional structured episode files, and writes the final artifacts to TOS.

# **Operator introduction**

> Operator ID: las_short_drama_script_revision

## Application scenarios

* **Name replacement**: Update character names, aliases, organization names, location names, or translated proper nouns.

* **Asset description adjustment**: Revise character looks, makeup, props, prop descriptions, or scene descriptions.

* **Local text cleanup**: Remove or replace residual terms, incorrect titles, or inconsistent expressions in scripts and asset tables.

* **Localization revision**: Transliterate English proper nouns into Chinese while preserving regular English business terms.

* **Post\-generation edits**: Apply small\-scope revisions after script generation without regenerating the full series.

## Core capabilities

* **Generation result revision**: Reads a generated short drama output directory and reuses its character table, prop table, scene table, and episode scripts.

* **Local scope check**: Checks whether the instruction is a local simple revision before execution, so plot rewrites and episode\-structure changes can be rejected early.

* **Global table synchronization**: Updates character names, aliases, identity descriptions, looks, scene names, location names, prop names, and prop descriptions.

* **Episode script revision**: Updates episode Markdown scripts based on the revised global tables and normalized revision plan.

* **Structured artifact support**: If the input contains `structured/`, the operator updates structured episode files. If not, it automatically falls back to script\-only revision.

* **TOS artifact delivery**: Returns revised global tables, the episode script directory, an optional structured directory, the full script, and the diff directory.

* **Token usage statistics**: Returns model token usage details, including cached input tokens, for cost estimation.

## Effect demonstration

The following example changes the character name Yang Xuanxuan to Sun Wan'er and updates the related character table and episode script.

* Before revision

   * [Original episode script](https://las-ai-ap-southeast-1-online-bp.tos-ap-southeast-1.bytepluses.com/operator_cards_serving/public/online/las_short_drama_script_revision/yiwanzhuixu_zh/scripts/ep_001.md)

   * [Original character table](https://las-ai-ap-southeast-1-online-bp.tos-ap-southeast-1.bytepluses.com/operator_cards_serving/public/online/las_short_drama_script_revision/yiwanzhuixu_zh/character_table.json)

* After revision

   * [Revised episode script](https://las-ai-ap-southeast-1-online-bp.tos-ap-southeast-1.bytepluses.com/operator_cards_serving/public/online/las_short_drama_script_revision/yiwanzhuixu_zh_after/scripts/ep_001.md)

   * [Revised character table](https://las-ai-ap-southeast-1-online-bp.tos-ap-southeast-1.bytepluses.com/operator_cards_serving/public/online/las_short_drama_script_revision/yiwanzhuixu_zh_after/character_table.json)

## Supported regions

* Asia Pacific (Johor): `ap-southeast-1`

## Operator performance

|Subcategory |Performance limit |
|---|---|
|Maximum Submit RPM |600 |
|Maximum Poll RPM |600 |
|Maximum concurrency |10 |

# Input and output requirements

## Input requirements

|Subcategory |Detailed requirements |
|---|---|
|Input data modality |Text |
|Input format |* Short drama generation output directory: The directory must directly contain `character_table.json`, `scene_table.json`, `prop_table.json`, and a `scripts/` episode script directory.<br><br>   * Global table files with a `final_` prefix are also supported. If prefixed and non\-prefixed files both exist, the non\-prefixed files take precedence.<br><br>* Input manifest JSON: The manifest must contain `character_table.uri`, `scene_table.uri`, `prop_table.uri`, and a non\-empty `scripts` list.<br><br>   * Each script item must contain `uri`. The optional `episode_id` is used to determine the local episode number. |
|Revision instruction |The instruction must describe an explicit, local, and replaceable revision. Plot rewrites, episode\-count changes, full translation, full expansion, and global style changes are not supported. |
|Input path requirements |Set `input_tos_path` to the short drama generation output directory or input manifest JSON file. Only TOS paths in the format `tos://bucket/path` are supported. The TOS bucket must belong to the same primary account and region as the current LAS service, and the input objects must exist and have read permission. |

## Output requirements

|Subcategory |Detailed requirements |
|---|---|
|Output data modality |Text |
|Output results |Revised character, scene, and prop tables; revised episode Markdown scripts; an optional structured episode directory; an optional full script; revision diff files; and token usage statistics. |
|Output path requirements |Set `output_tos_path` to the TOS root directory for saving results, in the format `tos://bucket/path`. The TOS bucket must belong to the same primary account and region as the current LAS service, and the directory must have write permission. The operator appends a task\-level directory to this path. |

# Billing instructions

* Billing standard

   |Item |Billing standard description |
   |---|---|
   |Billing items |There are three billing items: **model input, model output, and cache\-hit input**. The total payable fee is the sum of all billing items.<br><br><br>* `token_usage.prompt_tokens`: Model input token usage.<br><br>* `token_usage.completion_tokens`: Model output token usage.<br><br>* `token_usage.cached_tokens`: Input tokens that hit the cache. |
   |Billing type |Pay\-as\-you\-go in `USD/million tokens`, billed hourly based on actual usage. |
   |Unit price |* Model input: 1.25 USD/million tokens.<br><br>* Model output: 7.5 USD/million tokens.<br><br>* Cache\-hit input: 0.25 USD/million tokens. |

# Caution and prerequisites

|Details |Caution and prerequisites |
|---|---|
|Enable LAS |Ensure that LAS is enabled for the BytePlus account before invoking the operator. Enabling LAS without using billable features does not incur fees. |
|Costs |Understand the model input, model output, and cache\-hit input charges before invoking the operator. |
|Authentication (API Key) |Generate an LAS API Key and configure it as an environment variable before invoking the operator. For details, see [Obtain and configure the API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|Base URL |Determine the Base URL based on the region where LAS is deployed. For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The following examples use the Asia Pacific (Johor) endpoint. |

# **Rest API invocation**

## API call instructions

* This operator uses asynchronous APIs. Call Submit to create a task and obtain a `task_id`, and then call Poll with the `task_id` to query task status and results.

* A `task_id` remains valid for three days after submission. After three days, the task result can no longer be queried with that `task_id`.

## Submit

### Interface description

Submit the `las_short_drama_script_revision` operator to run a local short drama script revision task.

### Request parameters

**operator_id** string 必选 `Example value: las_short_drama_script_revision`

Operator ID. The value is fixed to `las_short_drama_script_revision`.

**operator_version** string 必选 `Example value: v1`

Operator version. Currently, only `v1` is supported.

**data** ShortDramaScriptRevisionReqParams 必选

Operator parameters.

**instruction** string 必选 `Example value: Transliterate English proper nouns in the script into Chinese`

Revision instruction. Explicit local replacements or local asset adjustments are recommended.

**script_type** string `Optional` `Example value: full`

Script output type. `full` also outputs `scripts/full_script.md`; `compact` outputs only episode scripts. Default: `full`.

**input_tos_path** string 必选 `Example value: tos://bucket/path/script_gen_output`

TOS directory of a short drama generation result, or a TOS JSON input manifest. It must start with `tos://`. Directory input must directly contain the three global tables and `scripts/`; JSON manifest input must declare `character_table.uri`, `scene_table.uri`, `prop_table.uri`, and `scripts[].uri`. The bucket must belong to the same primary account and region as LAS, and the input objects must have read permission.

**output_tos_path** string 必选 `Example value: tos://bucket/path/revision_output`

TOS output root directory for saving results. The bucket must belong to the same primary account and region as LAS, and the directory must have write permission.

### Response parameters

**metadata** metadata

Request metadata.

**task_id** string `Example value: task-xxx`

Task ID in asynchronous mode, used to query task status.

**task_status** string `Example value: PENDING`

Task status. `PENDING`: Request received; `RUNNING`: In progress; `COMPLETED`: Finished; `FAILED`: Failed; `TIMEOUT`: Timed out.

**business_code** string `Example value: 0`

Business code.

**error_msg** string

Detailed exception information returned when an exception occurs.

### Example

#### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_short_drama_script_revision",
    "operator_version": "v1",
    "data": {
        "instruction": "Transliterate English proper nouns in the script into Chinese and keep regular English business terms unchanged",
        "script_type": "full",
        "input_tos_path": "tos://bucket/path/script_gen_output",
        "output_tos_path": "tos://bucket/path/revision_output"
    }
}'
```

#### Response example

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

### Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |invalid parameter |A parameter is invalid, such as a malformed TOS path, an empty `instruction`, or another parameter outside its valid range. |
|400 |Parameter.Missing |Missing required parameter |A required parameter such as `input_tos_path` or `instruction` is missing, or TOS credentials are unavailable when required. |
|400 |Tos.AccessFailed |Failed to access TOS path with provided credentials |The TOS path cannot be accessed, or the credentials are invalid. |
|400 |DramaScriptRevision.InputMissing |missing required input file |The input directory is missing required global tables or episode scripts, or the input manifest is missing required URIs. |
|400 |DramaScriptRevision.ScopeRejected |revision scope rejected |The instruction is not a clear local revision and is rejected. |
|400 |DramaScriptRevision.LLMFailed |LLM call failed during script revision |The model call failed during script revision. |
|401 |Authorization.Missing |Missing Authorization. |Authentication is missing. |
|401 |ApiKey.InValid |The api key is invalid. |The API Key is invalid. |
|500 |InternalError |Internal error |Internal server error. |

## Poll

### Interface description

Query the execution status and result of a short drama script revision task.

### Request parameters

**operator_id** string 必选 `Example value: las_short_drama_script_revision`

Operator ID. The value is fixed to `las_short_drama_script_revision`.

**operator_version** string 必选 `Example value: v1`

Operator version. Currently, only `v1` is supported.

**task_id** string 必选 `Example value: task-xxx`

Task ID returned by Submit.

### Response parameters

**metadata** metadata

Request metadata.

**task_id** string `Example value: task-xxx`

Asynchronous task ID.

**task_status** string `Example value: COMPLETED`

Task status. `PENDING`: Request received; `RUNNING`: In progress; `COMPLETED`: Finished; `FAILED`: Failed; `TIMEOUT`: Timed out.

**submit_time** string `Example value: 2026-07-24T13:00:00+08:00`

Task submission time in ISO 8601 format.

**end_time** string `Example value: 2026-07-24T13:05:00+08:00`

Task end time in ISO 8601 format.

**business_code** string `Example value: 0`

Business code.

**error_msg** string

Detailed exception information returned when an exception occurs.

**data** ShortDramaScriptRevisionResponse

Revision result returned when `task_status` is `COMPLETED`.

**output_dir** string `Example value: tos://bucket/path/revision_output/task-xxx`

Actual output directory. A task\-level directory is appended to `output_tos_path`.

**character_table_path** string `Example value: tos://bucket/path/revision_output/task-xxx/character_table.json`

TOS path of the revised character table JSON.

**scene_table_path** string `Example value: tos://bucket/path/revision_output/task-xxx/scene_table.json`

TOS path of the revised scene table JSON.

**prop_table_path** string `Example value: tos://bucket/path/revision_output/task-xxx/prop_table.json`

TOS path of the revised prop table JSON.

**scripts_path** string `Example value: tos://bucket/path/revision_output/task-xxx/scripts`

Directory of revised episode Markdown scripts.

**structured_path** string `Example value: tos://bucket/path/revision_output/task-xxx/structured`

Revised structured episode directory. It may be empty if the input has no structured files.

**full_script_path** string `Example value: tos://bucket/path/revision_output/task-xxx/scripts/full_script.md`

Full script path returned when `script_type=full`.

**diffs_path** string `Example value: tos://bucket/path/revision_output/task-xxx/diffs`

Revision diff directory.

**input_episode_count** integer `Example value: 3`

Number of input episodes.

**generated_script_count** integer `Example value: 3`

Number of generated episode scripts.

**token_usage** TokenUsage `Example value: {"prompt_tokens":10063,"completion_tokens":681,"total_tokens":10744,"cached_tokens":0}`

Model token usage details.

**prompt_tokens** integer `Example value: 10063`

Input token count.

**completion_tokens** integer `Example value: 681`

Output token count.

**total_tokens** integer `Example value: 10744`

Sum of input and output tokens.

**cached_tokens** integer `Example value: 0`

Number of input tokens that hit the cache.

### Example

#### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_short_drama_script_revision",
    "operator_version": "v1",
    "task_id": "task-20260724130000-abc123"
}'
```

#### Response example

```JSON
{
  "metadata": {
    "task_id": "task-20260724130000-abc123",
    "task_status": "COMPLETED",
    "submit_time": "2026-07-24T13:00:00+08:00",
    "end_time": "2026-07-24T13:07:05+08:00",
    "business_code": "0",
    "error_msg": ""
  },
  "data": {
    "output_dir": "tos://bucket/path/revision_output/task-20260724130000-abc123",
    "package_url": null,
    "character_table_path": "tos://bucket/path/revision_output/task-20260724130000-abc123/character_table.json",
    "scene_table_path": "tos://bucket/path/revision_output/task-20260724130000-abc123/scene_table.json",
    "prop_table_path": "tos://bucket/path/revision_output/task-20260724130000-abc123/prop_table.json",
    "scripts_path": "tos://bucket/path/revision_output/task-20260724130000-abc123/scripts",
    "structured_path": "tos://bucket/path/revision_output/task-20260724130000-abc123/structured",
    "full_script_path": "tos://bucket/path/revision_output/task-20260724130000-abc123/scripts/full_script.md",
    "diffs_path": "tos://bucket/path/revision_output/task-20260724130000-abc123/diffs",
    "input_episode_count": 3,
    "generated_script_count": 3,
    "token_usage": {
      "prompt_tokens": 10063,
      "completion_tokens": 681,
      "total_tokens": 10744,
      "cached_tokens": 0
    }
  }
}
```

### Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |invalid parameter |A parameter is invalid, such as an empty `task_id` or a task parameter outside its valid range. |
|400 |Parameter.Missing |Missing required parameter |A required parameter is missing. |
|400 |Tos.AccessFailed |Failed to access TOS path with provided credentials |The TOS path cannot be accessed, or the credentials are invalid. |
|400 |DramaScriptRevision.InputMissing |missing required input file |The input directory is missing required global tables or episode scripts, or the input manifest is missing required URIs. |
|400 |DramaScriptRevision.ScopeRejected |revision scope rejected |The instruction is not a clear local revision and is rejected. |
|400 |DramaScriptRevision.LLMFailed |LLM call failed during script revision |The model call failed during script revision. |
|401 |Authorization.Missing |Missing Authorization. |Authentication is missing. |
|401 |ApiKey.InValid |The api key is invalid. |The API Key is invalid. |
|500 |InternalError |Internal error |Internal server error. |
