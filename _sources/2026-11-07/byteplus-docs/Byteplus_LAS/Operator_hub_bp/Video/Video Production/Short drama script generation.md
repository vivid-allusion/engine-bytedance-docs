---
title: "Short drama script generation"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Short_drama_script_generation"
---

The short drama/movie script generation operator (`las_short_drama_script_gen`) is an automated tool for reverse script extraction, designed for serialized or ultra\-long video content, including short dramas, long videos, and movies. Powered by a visual multimodal large model (VLM), the operator can automatically extract all characters from the entire drama or film, analyze character relationships, and generate high\-quality textual scripts and character lists in reverse, including detailed scenes, actions, expressions, and dialogues based on visuals and lines. This facilitates secondary creation, translation for overseas markets, and copyright protection for video content.

<span id="operator-introduction"></span>
# Operator introduction

> Operator ID: las_short_drama_script_gen


<span id="applicable-scenarios"></span>
## Applicable scenarios

&nbsp;


|Scenario |Description |
|---|---|
|Short drama overseas distribution and localization translation |Automatically generate multi\-dimensional text drafts for the original footage, reducing manual script extraction costs. |
|Secondary creation of film and television content |Provides detailed plot text and character traits, facilitating the creation of derivative works. |
|Copyright protection and infringement comparison |High\-fidelity text conversion of video content, providing a fixed chain of evidence. |


<span id="core-capabilities"></span>
## Core capabilities


* **Character consistency recognition**: Overcomes the limitations of isolated understanding of single episodes or segments, enabling stable tracking of core characters in long serials or ultra\-long movies. Ensures high consistency of character identity and settings across episodes when facing costume changes, side profiles, or complex scene transitions, ultimately constructing a complete global character list.

* **High\-fidelity script reverse restoration**: Integrates video visuals and dialogue lines to generate professional\-level storyboard scripts in reverse (with precise timestamps in movie mode). Accurately restores scene layout, character emotions, body movements, and key dialogues, providing high\-quality textual drafts ready for secondary development or translation review.

* **Dual\-mode adaptive architecture**:

   * **Short drama mode**: Supports batch input of multiple short drama episodes, processes strictly in input order, and maintains continuity and character consistency in serialized plots.

   * **Movie mode**: For single movies or long recordings lasting several hours, automatically initiates adaptive processing strategies for long videos to effectively mitigate detail loss caused by limitations of long contexts in large models.

* **Flexible output format customization**: Provides an interface for custom instructions (Prompts). You can freely adjust the generation style of individual episode scripts according to specific business requirements (such as focusing on psychological descriptions, specific storyboard layout formats, or particular text markup), to meet the direct integration needs of various downstream businesses.

* **Convenient result delivery**: Supports directly and securely writing the generated character list and complete script to your specified cloud storage (TOS).


<span id="effect-demonstration"></span>
## Effect demonstration


---



<div style="text-align: center">
<strong>[Input video]</strong></div>



<columns>
<columnsItem zoneid="hEaG90aATJ">

* Input video: EP01

   <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e472c17b08f4eb999cedc9ebdf331f3~tplv-goo7wpa0wc-image.image" controls></video>
   

* Input video: EP02

   <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c819aefc50a41f589d23eba5f61f2ad~tplv-goo7wpa0wc-image.image" controls></video>
   

</columnsItem>
<columnsItem zoneid="sDKuEnyg9X">

* Output: Generate complete scripts and individual episode scripts

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39caa87428964301b4854d7472be63d6~tplv-goo7wpa0wc-topic.webp) </span>

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3358dca1a2544fd5afc50888df40c7a7~tplv-goo7wpa0wc-raw.image" name="ep_001.md">ep_001.md</Attachment>
   

&nbsp;

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01afd727be7b49c299ccfb94ddc6829f~tplv-goo7wpa0wc-raw.image" name="ep_002.md">ep_002.md</Attachment>
   

&nbsp;

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1bb0a435d25743acb97111b16a35b0f1~tplv-goo7wpa0wc-raw.image" name="full_script.md">full_script.md</Attachment>
   

</columnsItem>
</columns>


<div style="text-align: right">
——The above is a sample output. The operator is continuously iterated and optimized. The actual structure and fields of the output depend on the operator's actual output when called.</div>



---



<span id="supported-regions"></span>
## Supported regions


* Asia Pacific(Johor)：ap\-southeast\-1


<span id="operator-performance"></span>
## Operator performance

&nbsp;


|Item breakdown |Performance impact |
|---|---|
|Maximum RPM |600 |
|Maximum concurrency |10 |
|Time consumption |Directly proportional to video duration. |


<span id="input-and-output-requirements"></span>
# Input and output requirements

<span id="input-requirements"></span>
## Input requirements

&nbsp;


|Breakdown |Detailed requirements |
|---|---|
|Supported input data modalities |Video |
|Input format: Video |* Format: `mp4`, `mov`, `avi`, `mkv`, `flv`, `webm`<br><br>* Size: Minimum 1 second, maximum 5 hours; up to 10 GB. |
|Input path requirements |Provide input data to the operator via the request parameter `video_urls`. Currently, two methods are supported: public URL and TOS path.<br><br><br>* Public URL: A publicly accessible URL in the format `http/https`.<br><br>   * Public URLs that require login status or additional Header authentication are not supported; temporary URLs must be valid during task execution.<br><br>* TOS path: After uploading the data to be processed to a TOS Bucket under the same primary account and region as the current LAS service, you can provide the TOS path in the format `tos://bucket_name/demo`.<br><br>   * The TOS object must exist and have read permissions. |


<span id="output-requirements"></span>
## Output requirements

&nbsp;


|Breakdown |Detailed requirements |
|---|---|
|Output data modality |Text (script Markdown file) |
|Output path: TOS |Specify the storage path for the operator's output results via the request parameter `output_tos_path`. Currently, only TOS paths are supported.<br><br>TOS path: A TOS Bucket directory under the same primary account and region as the LAS service, with write permissions, in the format: `tos://bucket/output/`. |


<span id="billing-instructions"></span>
# Billing instructions


* Billing standards

&nbsp;

   
   |Sub\-items |Billing standards description |
   |---|---|
   |Billing item |Usage is calculated and billed based on **the duration of the input video**. |
   |Billing type |Usage\-based billing, unit: `USD/minute`, invoiced every hour based on actual usage. Billing precision: rounded to the nearest value |
   |Unit price |0.21 USD/minute |
   

* Billing details

   Billing formula: `Total cost = unit price * usage`


<span id="caution-and-prerequisites"></span>
# Caution and prerequisites

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
## submit

<span id="interface-description"></span>
### Interface description

Submit the las_short_drama_gen operator to perform short drama/movie script generation tasks.

<span id="request-parameters"></span>
### Request parameters



**operator_id** <span data-label="purple">string</span> <span data-api-tag="require|ZDssO5">必选</span> `Example value: las_short_drama_script_gen`

The operator ID is las_short_drama_script_gen.



**operator_version** <span data-label="purple">string</span> <span data-api-tag="require|C852sy">必选</span> `Example value: v1`

Currently only v1 is supported.



**data** <span data-label="purple">ShortDramaScriptGenReqParams</span> <span data-api-tag="require|4jBzQi">必选</span>

Operator parameters.


**video_urls** <span data-label="purple">list of string</span> <span data-api-tag="require|1qNTxL">必选</span> `Example value: [tos://xxx/video.mp4]`

List of short drama (movie) video URLs. The backend automatically detects short drama and movie modes. Caution: The operator will strictly determine the episode number according to the physical index order of the list (that is, the first URL is considered episode 1, and so on). Please ensure the list is correctly ordered by episode before submitting. Supports Volcano TOS (tos://bucket/key).



**output_tos_path** <span data-label="purple">string</span> <span data-api-tag="require|Cj8198">必选</span> `Example value: tos://testbucket/path/`

TOS path for saving results. Supports Volcano TOS (tos://bucket/key).



**custom_script_prompt** <span data-label="purple">string</span>

Custom script generation prompt.




&nbsp;

<span id="response-parameters"></span>
### Response parameters


**metadata** <span data-label="purple">metadata</span>

Request metadata.


**task_id** <span data-label="purple">string</span> `Example value: task-xxx`

Task ID in asynchronous mode, used for job status queries.



**task_status** <span data-label="purple">string</span> `Example value: PENDING`

Task status in asynchronous mode.


* PENDING, request received

* RUNNING, in progress

* COMPLETED, finished

* FAILED, failed

* TIMEOUT, timed out



**business_code** <span data-label="purple">string</span> `Example value: 0`

Business code.



**error_msg** <span data-label="purple">string</span>

If an exception occurs, detailed exception information will be returned.



&nbsp;

<span id="example"></span>
### Example

<span id="request-example"></span>
#### Request example

```Bash
# Set INPUT_PATH to the TOS path of the video file saved under this account
export INPUT_PATH="tos://xxxx/sample.mp4"
# Set OUTPUT_PATH_TEMPLATE to a writable TOS path under this account
export OUTPUT_PATH_TEMPLATE="tos://xxxx/output/"
# Initiate an operator service request
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_short_drama_script_gen",
    "operator_version": "v1",
    "data": {
        "video_urls": ["$INPUT_PATH"],
        "output_tos_path": "$OUTPUT_PATH_TEMPLATE"
    }
}'
```


<span id="response-example"></span>
#### Response example

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


|HttpCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |The parameter is invalid.. |Invalid parameter |
|401 |Authorization.Missing |Missing Authorization. |Authorization missing |
|401 |ApiKey.InValid |The api key is invalid. |Invalid API |


<span id="poll"></span>
## Poll

<span id="interface-description-1"></span>
### Interface description

Query the execution status and result of the short drama/movie script generation task.

<span id="request-parameters-1"></span>
### Request parameters



**operator_id** <span data-label="purple">string</span> <span data-api-tag="require|yDxEpK">必选</span> `Example value: las_short_drama_script_gen`

Operator ID



**operator_version** <span data-label="purple">string</span> <span data-api-tag="require|xKN3Xz">必选</span> `Example value: v1`

Operator version



**task_id** <span data-label="purple">string</span> <span data-api-tag="require|3BLfkN">必选</span> `Example value: task-xxx`

Task ID



&nbsp;

<span id="response-parameters-1"></span>
### Response parameters



**metadata** <span data-label="purple">metadata</span>

Metadata of the request.


**task_status** <span data-label="purple">string</span> `Example value: COMPLETED`

Task status.


* ACCEPTED, request received

* RUNNING, running

* COMPLETED, completed

* FAILED, failed



**submit_time** <span data-label="purple">string</span> `Example value: 2026-07-21T16:04:06+08:00`

Task submission time, formatted as an ISO 8601 timestamp.



**end_time** <span data-label="purple">string</span> `Example value: 2026-07-21T16:04:06+08:00`

Task end time, formatted as an ISO 8601 timestamp.



**business_code** <span data-label="purple">string</span> `Example value: 0`

Business code.



**error_msg** <span data-label="purple">string</span> `Example value: The api key is invalid.`

If an exception occurs, detailed exception information will be returned.



**task_id** <span data-label="purple">string</span> `Example value: task-xxx`

Task ID in asynchronous mode.




**data** <span data-label="purple">ShortDramaGenResponse</span>

Returned data.


**final_table_path** <span data-label="purple">string</span> `Example value: tos://bucket/key`

Final role table path.



**scripts_path** <span data-label="purple">string</span> `Example value: tos://bucket/key`

Script folder path.



**input_episode_count** <span data-label="purple">integer</span> `Example value: 2`

Total number of input episodes.



**generated_script_count** <span data-label="purple">integer</span> `Example value: 2`

Number of scripts generated successfully.



**total_video_duration_minutes** <span data-label="purple">float</span> `Example value: 16.6`

Total duration of videos processed successfully (minutes).



**failed_video_urls** <span data-label="purple">list of string</span> `Example value: ["tos://bucket/key"]`

List of video URLs that failed to process.



**failed_videos** <span data-label="purple">list of FailedVideoInfo</span> `Example value: [{"video_url":"tos://bucket/key.mp4","episode_index":1,"reason":"Unsupported video format"}]`

List of details for videos that failed to process, including the failed video URL, episode index, and reason for failure.


**video_url** <span data-label="purple">string</span> `Example value: tos://bucket/key.mp4`

URL of the video that failed to process.



**episode_index** <span data-label="purple">integer</span> `Example value: 1`

Episode index corresponding to the failed video, starting from 1.



**reason** <span data-label="purple">string</span> `Example value: Unsupported video format`

Reason for failure.




**status** <span data-label="purple">string</span> `Example value: success`

Short drama generation status. Usually returned when metadata.task_status=COMPLETED. Enum values: success, failed, partial_success. partial_success means the task is overall completed but some videos failed to process; in this case, failed_video_urls is not empty and generated_script_count is less than input_episode_count. failed means all videos failed to generate.




&nbsp;

<span id="example-1"></span>
### Example

<span id="request-example-1"></span>
#### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_short_drama_script_gen",
    "operator_version": "v1",
    "task_id": "task-20251125163544-abc123"
}'
```


<span id="response-example-1"></span>
#### Response example

```JSON
{
  "metadata": {
    "task_id": "06ecbd66031e7006022d",
    "task_status": "COMPLETED",
    "submit_time": "2026-07-21T16:04:06+08:00",
    "end_time": "2026-07-21T16:04:06+08:00",
    "business_code": "0",
    "error_msg": "Task processed successfully"
  },
  "data": {
    "final_table_path": "tos://xxx/final_character_table.json",
    "scripts_path": "tos://xxx/scripts",
    "input_episode_count": 12,
    "generated_script_count": 9,
    "total_video_duration_minutes": 27.8,
    "failed_video_urls": [],
    "failed_videos": [],
    "status": "partial_success"
  }
}
```


<span id="error-code-1"></span>
### Error code

&nbsp;


|HttpCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Missing |Missing required parameter. |Required parameter missing in request body |
|400 |Parameter.Invalid |Invalid parameter. |Invalid parameter |
|400 |Url.Invalid |Invalid URL. |Video URL is inaccessible or does not exist |
|400 |Video.Invalid |Invalid video file. |Video format not supported or file is corrupted |
|400 |Video.DownloadFailed |Video download failed. |Download exception or access failure |
|400 |Image.TooLarge |Video file too large. |Video file size exceeds the system's single processing limit |
|400 |Video.DurationExceeded |Video duration exceeded. |Total video duration exceeds the maximum limit |
|400 |Video.DurationTooShort |Video duration too short. |Video duration is insufficient for plot restoration |
|400 |Video.FrameExtractionFailed |Frame extraction failed. |Frame extraction failed |
|400 |Connection.TooMany |Exceed max connections. |Concurrency too high, rate limiting triggered |
|400 |Video.VLMFailed |VLM call failed. |Model request failed |
|401 |Authorization.Missing |Missing Authorization. |Authorization missing |
|401 |ApiKey.InValid |The api key is invalid. |Invalid API |
|400 |Task.NotFound |Task not found. |Task does not exist |
|500 |Internal.ServerError |Internal server error. |Internal service error |
