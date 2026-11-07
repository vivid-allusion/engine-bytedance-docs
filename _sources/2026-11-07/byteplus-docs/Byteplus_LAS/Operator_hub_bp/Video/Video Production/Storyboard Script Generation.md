---
title: "Storyboard Script Generation"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Storyboard_Script_Generation"
---

The LAS Storyboard Rewrite operator is designed for script production and e\-commerce voice\-over video workflows, converting input text into a standard `storyboard_bundle`. Currently, two capabilities are provided: generating storyboards from scripts combined with character, prop, and scene asset JSON files, and directly generating storyboards from voice\-over scripts.

<span id="834599d7"></span>
# Operator introduction

> Operator ID: las_storyboard_rewrite


<span id="4c40e6bd"></span>
## Key features


* Script and authoritative asset table to storyboard: Retains the identifiers and settings of input character, prop, and scene assets, decomposes the script into shots, and binds each shot to the corresponding asset.

* Voice\-over script to storyboard: Preserves the original intent and core selling points of the voice\-over, organizes shot duration, visual actions, voice\-over, and structured descriptions that can be directly used for subsequent video generation based on semantics.

* Faithful visual expansion: When visuals and actions are already present in the input, they are prioritized and supplemented with necessary details; when only a voice\-over is provided, visuals are designed based on verifiable content in the script to avoid unfounded fabrication.

* Standard result delivery: Outputs a unified `storyboard_bundle_manifest.json`, associating storyboards, characters, scenes, props, and change and validation reports.


<span id="142d70ed"></span>
## Effect demonstration


---



<div style="text-align: center">
<strong>[Script to storyboard]</strong></div>



* Input example

   * Script example

      <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1054ec58c7f40069bc57c763d261695~tplv-goo7wpa0wc-image.image" name="ep_001.md">ep_001.md</Attachment>
      

   * Asset JSON example

      <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c4a4d50368d48e29d8f4b63a2d4e4cd~tplv-goo7wpa0wc-image.image" name="final_character_table.json">final_character_table.json</Attachment>
      

&nbsp;

      <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c980ad3fc2041ecb0e7c8da5bfa3c27~tplv-goo7wpa0wc-image.image" name="final_prop_table.json">final_prop_table.json</Attachment>
      

&nbsp;

      <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/89407fb48737482abfeaef8555260a85~tplv-goo7wpa0wc-image.image" name="final_scene_table.json">final_scene_table.json</Attachment>
      


<div style="text-align: right">
—The above is an input example using the output of the <a href="https://docs.byteplus.com/docs/undefined/69f326f9837de40528dd71f1">Short Drama Script Generation</a> operator</div>



* Generated storyboard result example

   * Storyboard result generation summary, verification status, pending assets, and generation diagnostics

      <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35a4a76f1178489c950f969194ae3529~tplv-goo7wpa0wc-image.image" name="change_report.json">change_report.json</Attachment>
      

   * Camera shots and their visual settings

      <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d3510e0a83644e2b2c6a5eedd3319fa~tplv-goo7wpa0wc-image.image" name="shot_registry.json">shot_registry.json</Attachment>
      

   * Character assets and their visual settings

      <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54736920cc284d7ca06b8d606649ca0a~tplv-goo7wpa0wc-image.image" name="characters_registry.json">characters_registry.json</Attachment>
      

   * Prop assets and their visual settings

      <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c69598eb62644e7b929f530b49a064d~tplv-goo7wpa0wc-image.image" name="prop_registry.json">prop_registry.json</Attachment>
      

   * Scene assets and their visual settings

      <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1762aa954e424b709648059272243aa3~tplv-goo7wpa0wc-image.image" name="scene_registry.json">scene_registry.json</Attachment>
      


<div style="text-align: right">
—The above is a result example; actual generated result fields are subject to the operator's returned results.</div>



---



<span id="0cd6fa2d"></span>
## Supported regions


* Asia Pacific(Johor)：ap\-southeast\-1


<span id="6d91feb9"></span>
## Operator performance


|Subdivision |Performance impact description |
|---|---|
|Maximum RPM |600 |
|Duration |* Total duration is mainly affected by text length, number of shots, asset table size, number of reference images, and model invocation count.<br><br>* Long scripts are processed in chunks based on text or episode boundaries and are merged into unified assets and storyboard results after generation. |


<span id="7a3a4638"></span>
# Input and output requirements

<span id="94bc4a9a"></span>
## Input requirements


|Subdivision |Detailed requirements |
|---|---|
|Supported input data modalities |* Text<br><br>* Image |
|Input format: Text |Use the request parameter `input_url`or `source_text` to input the script or voiceover for storyboard conversion into the operator.<br><br><br>* The operator model determines whether the current script conversion scenario is "script to storyboard" or "voice\-over script to storyboard" based on the input text content.<br><br>* In the script\-to\-storyboard scenario: you must provide all three asset JSON files for characters, props, and scenes. It is recommended that the three asset JSON files include at least stable ID, name, and visual description. For the reference format, see [Character/prop/scene asset JSON examples](https://docs.byteplus.com/docs/undefined/6a990db4d82b5a04debd736f#a99e5f28). When converting a script to a storyboard, it is recommended to use the LAS script parsing operator to generate the asset JSON table. |
|Input format: Image |Use the `reference_images` parameter to input reference images into the operator. In the voiceover\-to\-storyboard scenario, you may provide reference images as needed.<br><br><br>* Quantity: A maximum of 9 images can be input per task.<br><br>* Aspect ratio (width/height): [0.4, 2.5]<br><br>* Width and height (px): [300,6000] |
|Input path requirements |Use the request parameters `video_url` and `reference_images` to provide input data to the operator. Currently, two methods are supported: public URL and TOS path.<br><br><br>* Public URL: A publicly accessible URL in the format `http/https`.<br><br>   * Public URLs do not support addresses requiring login status or additional header authentication; temporary URLs must remain valid during task execution.<br><br>* TOS path: After uploading the data to be processed to the TOS bucket under the same primary account and region as the current LAS service, you can provide a TOS path in the format `tos://bucket_name/demo`.<br><br>   * The TOS object must exist and have read permissions. |


<span id="ff19f167"></span>
## Output requirements


|Subdivision |Detailed requirements |
|---|---|
|Output data modality |* Text |
|Output path: TOS |Specify the storage path for the operator output results using the request parameter `output_tos_path`. Currently, setting a TOS path is supported.<br><br><br>* TOS path: A TOS Bucket directory with write permissions under the same primary account and region as the LAS service. Format: `tos://bucket/output/`. |


<span id="5329141b"></span>
# Billing information


* Billing standards

   
   |Sub\-items |Billing standards description |
   |---|---|
   |Billing items |The following billing items are included:<br><br><br>* Basic invocation fee: A fixed fee for invoking the operator.<br><br>* Script generation \- image interpretation fee: Billed based on the number of input images.<br><br>* Script generation \- text interpretation fee: Billed based on the amount of input text. |
   |Billing type |Usage\-based billing, invoiced hourly based on actual usage. |
   |Unit price |The unit prices for different billing items vary. See the table below for details. |
   

* Billing details

   
   |Billing item |Unit price |
   |---|---|
   |Basic invocation fee |0.86 USD per call |
   |Script generation \- image interpretation fee |0.04 USD per image |
   |Script generation \- text interpretation fee |0.17 USD per 1,000 characters |
   


<span id="98c6189e"></span>
# Caution and prerequisites


|Details |Caution and prerequisites |
|---|---|
|Costs |Before calling an operator, you need to understand the model invocation costs associated with using the operator. For details, see [Large model billing](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |


<span id="5fd2c977"></span>
# **Rest API invocation**

<span id="92eafb39"></span>
## API usage instructions


* The API for this operator is an asynchronous task interface. You need to submit a task via the `Submit` interface to obtain the `task_id`, then use the `Poll` interface to check the status of the corresponding task (`task_id`) and retrieve the operator processing result.

* Caution: After the task is submitted, the `task_id` is valid for 3 days. After 3 days, the operator processing result cannot be retrieved using this `task_id`.


<span id="f4ac1f63"></span>
## Submit

<span id="c27d5dda"></span>
### Interface description

Submit an asynchronous storyboard script task. Currently, two modes are supported: "Script + character/prop/scene asset JSON to storyboard" and "voice\-over script to storyboard".

<span id="67a0d72d"></span>
### Request parameters

```mixin-react
const properties = ({
  "columns": [
    {
      "title": "Name",
      "dataIndex": "column_0",
      "key": "column_0",
      "width": 300
    },
    {
      "title": "Type",
      "dataIndex": "column_1",
      "key": "column_1",
      "width": 150
    },
    {
      "title": "Required",
      "dataIndex": "column_2",
      "key": "column_2",
      "width": 80
    },
    {
      "title": "Example value",
      "dataIndex": "column_3",
      "key": "column_3",
      "width": 150
    },
    {
      "title": "Description",
      "dataIndex": "column_4",
      "key": "column_4"
    }
  ],
  "data": [
    {
      "key": "1",
      "column_0": "operator_id",
      "column_1": "string",
      "column_2": "Yes",
      "column_3": "las_storyboard_rewrite",
      "column_4": "Operator ID."
    },
    {
      "key": "2",
      "column_0": "operator_version",
      "column_1": "string",
      "column_2": "Yes",
      "column_3": "v1",
      "column_4": <div> Operator version. Currently, only <code> v1</code> is supported. </div>
    },
    {
      "key": "3",
      "column_0": "data",
      "column_1": "StoryboardRewriteReqParams",
      "column_2": "Yes",
      "column_3": "",
      "column_4": "Parameters for text-based storyboard generation.",
      "children": [
        {
          "key": "3-1",
          "column_0": "input_url",
          "column_1": "string",
          "column_2": "Conditionally required",
          "column_3": "None",
          "column_4": <div>Screenplay or voiceover file URL. Provide either this field or <code>source_text</code>. Supports <code>http/https</code>, <code>tos://</code>.</div>
        },
        {
          "key": "3-2",
          "column_0": "source_text",
          "column_1": "string",
          "column_2": "Conditionally required",
          "column_3": "None",
          "column_4": <div> Inline script or voiceover copy. Provide either <code> input_url</code> or this parameter. </div>
        },
        {
          "key": "3-3",
          "column_0": "user_intent",
          "column_1": "string",
          "column_2": "Required",
          "column_3": "None",
          "column_4": "Description of the operator task intent. It is recommended to always enter: \"Please convert to storyboard script\"."
        },
        {
          "key": "3-4",
          "column_0": "characters_registry_url",
          "column_1": "string",
          "column_2": "Conditionally required",
          "column_3": "None",
          "column_4": "Character asset JSON address, required when converting script to storyboard."
        },
        {
          "key": "3-5",
          "column_0": "prop_registry_url",
          "column_1": "string",
          "column_2": "Conditionally required",
          "column_3": "None",
          "column_4": "Prop asset JSON address, required when converting script to storyboard."
        },
        {
          "key": "3-6",
          "column_0": "scene_registry_url",
          "column_1": "string",
          "column_2": "Conditionally required",
          "column_3": "None",
          "column_4": "Scene asset JSON address, required when converting script to storyboard."
        },
        {
          "key": "3-7",
          "column_0": "reference_images",
          "column_1": "array",
          "column_2": "No",
          "column_3": "None",
          "column_4": "List of reference images, required when converting voiceover copy to storyboard."
        },
        {
          "key": "3-8",
          "column_0": "min_shot_duration",
          "column_1": "integer",
          "column_2": "No",
          "column_3": "4",
          "column_4": <div> Minimum duration for a single shot, range <code> 4–30</code> seconds. </div>
        },
        {
          "key": "3-9",
          "column_0": "max_shot_duration",
          "column_1": "integer",
          "column_2": "No",
          "column_3": "15",
          "column_4": <div> Maximum duration for a single shot, range <code> 4–30</code> seconds, and must not be less than <code> min_shot_duration</code>. </div>
        },
        {
          "key": "3-10",
          "column_0": "output_tos_path",
          "column_1": "string",
          "column_2": "No",
          "column_3": "Allocated at runtime",
          "column_4": <div>Output directory. Supports <code>tos://</code> and must be in the same region as the API key.</div>
        }
      ]
    }
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```


<span id="6ba1a2a8"></span>
### Response parameters

```mixin-react
const properties = ({
  "columns": [
    {
"title": "Name",
      "dataIndex": "column_0",
      "key": "column_0",
      "width": 300
    },
    {
"title": "Type",
      "dataIndex": "column_1",
      "key": "column_1",
      "width": 150
    },
    {
"title": "Example value",
      "dataIndex": "column_2",
      "key": "column_2",
      "width": 150
    },
    {
"title": "Description",
      "dataIndex": "column_3",
      "key": "column_3"
    }
  ],
  "data": [
    {
      "key": "1",
      "column_0": "metadata",
      "column_1": "metadata",
      "column_2": "",
"column_3": "Request metadata.",
      "children": [
        {
          "key": "1-1",
          "column_0": "task_id",
          "column_1": "string",
          "column_2": "task-xxx",
"column_3": "Asynchronous task ID, used to query task status and results."
        },
        {
          "key": "1-2",
          "column_0": "task_status",
          "column_1": "string",
          "column_2": "PENDING",
"column_3": "Task status: PENDING, RUNNING, COMPLETED, FAILED, TIMEOUT."
        },
        {
          "key": "1-3",
          "column_0": "business_code",
          "column_1": "string",
          "column_2": "0",
"column_3": "Business code."
        },
        {
          "key": "1-4",
          "column_0": "error_msg",
          "column_1": "string",
          "column_2": "",
"column_3": "Exception details."
        }
      ]
    }
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```


<span id="15446fa3"></span>
### Examples

<span id="d665a233"></span>
#### Request example

Example 1: Script\-to\-storyboard conversion

```Bash
export OUTPUT_TOS_PATH="tos://bucket/output/storyboard_rewrite"

curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
  "operator_id": "las_storyboard_rewrite",
  "operator_version": "v1",
  "data": {
    "input_url": "tos://bucket/input/episode_01.md",
    "characters_registry_url": "tos://bucket/input/characters_registry.json",
    "prop_registry_url": "tos://bucket/input/prop_registry.json",
    "scene_registry_url": "tos://bucket/input/scene_registry.json",
    "min_shot_duration": 4,
    "max_shot_duration": 15,
    "output_tos_path": "'$OUTPUT_TOS_PATH'"
  }
}'
```


Example 2: Voice\-over script\-to\-storyboard conversion

```Bash
export OUTPUT_TOS_PATH="tos://bucket/output/storyboard_rewrite"

curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
  "operator_id": "las_storyboard_rewrite",
  "operator_version": "v1",
  "data": {
    "workflow_mode": "voiceover",
    "source_text": "这款双层沥水篮采用细密网孔，淘洗小米不易漏出，内外两层还能拆开单独使用。",
    "reference_images": [
      "tos://bucket/input/product_01.png"
    ],
    "min_shot_duration": 4,
    "max_shot_duration": 15,
    "output_tos_path": "'$OUTPUT_TOS_PATH'"
  }
}'
```


<span id="badf00a5"></span>
#### Response example

```Bash
{
  "metadata": {
    "task_id": "task-20260814150000-abc123",
    "task_status": "PENDING",
    "business_code": "0",
    "error_msg": ""
  }
}
```


<span id="4bd19a04"></span>
### Error code


|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |invalid parameter |The workflow, text, asset table, shot count, or shot duration parameters are invalid. |
|400 |Tos.AccessFailed |TOS access failed |Failed to download text, asset JSON, reference images, or upload results. |
|401 |Authorization.Missing |Missing Authorization |Authorization is missing. |
|401 |ApiKey.InValid |The api key is invalid |The API Key is invalid. |
|500 |Internal.ServerError |Internal server error |Internal server error, including model generation or result validation not completed. |


<span id="0afa992e"></span>
## Poll

<span id="36c9fb0e"></span>
### Interface description

Query the status and result of a LAS Storyboard Rewrite task.

<span id="618a53a9"></span>
### Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|operator_id |string |Yes |las_storyboard_rewrite |Operator ID. |
|operator_version |string |Yes |v1 |Operator version. |
|task_id |string |Yes |task\-xxx |Asynchronous task ID returned by Submit. |


<span id="7e74b120"></span>
### Response parameters

```mixin-react
const properties = ({
  "columns": [
    {
"title": "Name",
      "dataIndex": "column_0",
      "key": "column_0",
      "width": 300
    },
    {
"title": "Type",
      "dataIndex": "column_1",
      "key": "column_1",
      "width": 150
    },
    {
"title": "Example value",
      "dataIndex": "column_2",
      "key": "column_2",
      "width": 150
    },
    {
"title": "Description",
      "dataIndex": "column_3",
      "key": "column_3"
    }
  ],
  "data": [
    {
      "key": "1",
      "column_0": "metadata",
      "column_1": "metadata",
      "column_2": "",
"column_3": "Task metadata.",
      "children": [
        {
          "key": "1-1",
          "column_0": "task_id",
          "column_1": "string",
          "column_2": "task-xxx",
"column_3": "Asynchronous task ID."
        },
        {
          "key": "1-2",
          "column_0": "task_status",
          "column_1": "string",
          "column_2": "COMPLETED",
"column_3": "Task status: PENDING, RUNNING, COMPLETED, FAILED, TIMEOUT."
        },
        {
          "key": "1-3",
          "column_0": "submit_time",
          "column_1": "string",
          "column_2": "2026-08-14T15:00:00+08:00",
"column_3": "Task submission time, ISO 8601 format."
        },
        {
          "key": "1-4",
          "column_0": "end_time",
          "column_1": "string",
          "column_2": "2026-08-14T15:04:00+08:00",
"column_3": "Task end time, ISO 8601 format."
        },
        {
          "key": "1-5",
          "column_0": "business_code",
          "column_1": "string",
          "column_2": "0",
"column_3": "Business code."
        },
        {
          "key": "1-6",
          "column_0": "error_msg",
          "column_1": "string",
          "column_2": "",
"column_3": "Exception details."
        }
      ]
    },
    {
      "key": "2",
      "column_0": "data",
      "column_1": "StoryboardRewriteResponse",
      "column_2": "",
"column_3": "Data returned when the task succeeds.",
      "children": [
        {
          "key": "2-1",
          "column_0": "result_url",
          "column_1": "string",
          "column_2": "tos://bucket/output/v000/storyboard_bundle_manifest.json",
"column_3": "Standard storyboard bundle manifest address."
        }
      ]
    }
  ]
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```


`result_url` points to `storyboard_bundle_manifest.json`. The manifest will be associated with the following result files:


|File |Content |
|---|---|
|shot_registry.json |Shot list, shot duration, voice\-over, structured scene description, and video generation prompts. |
|characters_registry.json |Character assets and their visual settings. |
|prop_registry.json |Prop or product assets and their visual settings. |
|scene_registry.json |Scene assets and their visual settings. |
|change_report.json |Generated summary, verification status, pending assets, and generation diagnostics. |


<span id="30d6d3ae"></span>
# Examples

**Request examples**

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
  "operator_id": "las_storyboard_rewrite",
  "operator_version": "v1",
  "task_id": "task-20260814150000-abc123"
}'
```


**Response examples**

```JSON
{
  "metadata": {
    "task_id": "task-20260814150000-abc123",
    "task_status": "COMPLETED",
    "submit_time": "2026-08-14T15:00:00+08:00",
    "end_time": "2026-08-14T15:04:00+08:00",
    "business_code": "0",
    "error_msg": ""
  },
  "data": {
    "result_url": "tos://bucket/output/v000/storyboard_bundle_manifest.json"
  }
}
```


<span id="51cf1494"></span>
### Error code


|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |TaskId.Invalid |The task id is invalid |The task ID is invalid or the task does not exist. |
|401 |Authorization.Missing |Missing Authorization |Authorization is missing. |
|401 |ApiKey.InValid |The api key is invalid |The API Key is invalid. |
|500 |Internal.ServerError |Internal server error |Internal server error. |


<span id="6ff751b7"></span>
# Reference

<span id="a7d8a80b"></span>
## Character/prop/scene asset JSON examples

When converting a script to a storyboard, all three asset types—character, prop, and scene—must be provided. Each asset type can use either a TOS URL or an HTTP URL; it is not required to use the same delivery method for all three types.

It is recommended that each of the three JSON files include at least stable ID, name, and visual description fields (refer to the example below). When converting a script to a storyboard, it is recommended to use the LAS script parsing operator to generate the asset JSON table.


* Character asset JSON examples

   ```JSON
   {
     "characters": [
       {
         "character_id": "char_001",
         "name": "林晓",
         "description": "年轻的产品体验者",
         "visual_features": "黑色短发，浅色家居服"
       }
     ]
   }
   ```
   

* Prop asset JSON examples

   ```JSON
   {
     "props": [
       {
         "prop_id": "prop_001",
         "name": "双层沥水篮",
         "description": "用于清洗和沥水的双层厨具",
         "visual_features": "外层盆与细密漏网可拆分"
       }
     ]
   }
   ```
   

* Scene asset JSON examples

   ```JSON
   {
     "scenes": [
       {
         "scene_id": "scene_001",
         "name": "家庭厨房水槽",
         "description": "明亮整洁的家用厨房操作区",
         "visual_features": "浅色台面，不锈钢水槽"
       }
     ]
   }
   ```
