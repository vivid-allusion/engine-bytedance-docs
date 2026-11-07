---
title: "(Required) Step 3 Video Generation"
product: "Vision AI"
product_code: "byteplus-vision"
source: "https://docs.byteplus.com/en/docs/byteplus-vision/omnihuman-video_generation"
---

# Service Description

OmniHuman 1.5 generates video effects matching the input image based on a single image, text prompt, and audio file uploaded by the user.

The emotions and movements of the human figure have a strong correlation with the audio. It also supports adjusting the frame, movements, and camera movement via prompts. Additionally, OmniHuman 1.5 provides excellent support for images of animations, pets, and similar subjects, allowing users to specify the speaker/subject. It can be widely applied in scenarios such as content expression, singing, and performances.

# Restrictions

|Name |Details |
|---|---|
|Image |* Format: Common formats such as JPG (JPEG), PNG, JFIF; **JPG is recommended as the preferred format**<br><br>* Size: Less than 5 MB, resolution less than 4096\*4096; the clearer the input image, the better the generation effect.<br><br>* Additional Recommendation: If a speaker needs to be specified, **subject detection** must be performed first; if not, subject detection can be skipped. |
|Audio |* Duration: The duration must be less than 60 seconds. If the audio exceeds 60 seconds, an error will be generated and the generation will fail; excessive duration may lead to degraded effect) |
|Prompt (Optional) |* Supported Languages: Only Chinese, English, Japanese, Korean, Spanish (Mexican), Indonesian<br><br>* Note: Optional, used for precise control of the scene, movements, camera movements, etc. |

# Video Generation

## Submit tasks

### **Request parameters**

 **(1) Request address**

|**Name** |**Content** |
|---|---|
|Interface address |[https://cv.byteplusapi.com](https://cv.byteplusapi.com) |
|Request method |POST  |
|Content\-Type |application/json |

 **(2) Query parameters**

> **Query** spliced after the URL, example: https://cv.byteplusapi.com/?Action=CVSubmitTask&Version=2024\-06\-06

|**Parameter** |**Optional/Required** |**Type** |**Explanation** |
|---|---|---|---|
|Action |Required |String  |Fixed value: CVSubmitTask |
|Version |Required |String |Fixed value: 2024\-06\-06 |

 **(3) Header request parameters**

> **The fixed values for this service are: **Service=cv**, **Region=****ap\-singapore\-1****

It is primarily used for authentication. For details, please refer to the "[Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters) \- Authentication Parameters \- in header"

|**Parameter** |**Optional/Required** |**Type** |**Explanation** |
|---|---|---|---|
|Authorization |Required |String |Format: HMAC\-SHA256 Credential={AccessKeyId}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}. |

 **(4) Body parameters**

Service request parameter

|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|req_key |string |Yes |Service identifier: **realman_avatar_picture_omni15_cv**<br><br>fixed |
|image_url |string |Required |URL of the portrait image |
|mask_url |string |Optional |List of mask image URLs to specify a specific subject in the image to speak. Separate multiple mask image URLs with semicolons (;) if there are any.<br><br>Obtain the subject’s mask image via Step 2: Subject Detection and pass it in using **string** type.<br><br>Step 2 doc:  https://docs.byteplus.com/en/docs/byteplus\-vision/omnihuman\-subject_detection |
|audio_url |string |Required |URL of the audio file |
|seed |int |Optional |Random seed (used as the basis for determining the initial diffusion state). Default value: \-1 (random).<br><br>If the random seed is the same positive integer and other parameters are consistent, the generated content will have an extremely high probability of being identical in effect. |
|prompt |string |Optional |Prompt, only supports Chinese, English, Japanese, Korean, Mexican Spanish, and Indonesian |
|pe_fast_mode |bool |Optional |When enabled, it will speed up generation by sacrificing some effects.<br><br>Default Value: false (fast mode is disabled by default) |
|output_resolution |int |Optional |Resolution of the output video<br><br>Allowed values for output video resolution: 720 or 1080<br><br>Default: 1080 |
|callback_url |string |Optional |Callback notification address for the results of the current generation task. When the status of the task changes to terminal state, service will send a POST request to this address. The content structure of the callback request is consistent with the response body of the Query Task, with the addition of an extra task_id field.<br><br>The task status returned in the callback:<br><br>done: Processing completed (success or failure can be judged by the outer code & message) <br><br>canceled: Task cancelled.<br><br>If the callback fails, retry the callback three times at 1\-second intervals, with a 15\-second timeout for each attempt. |
|callback_auth_info |string |Optional |Reserved fields for authentication purposes, intended for authentication on callback interfaces. |

### Response parameter

 **(1) General response parameters**

Please refer to [Common Responses and Error Codes](https://docs.byteplus.com/en/docs/byteplus-vision/docs-common-responses-and-error-codes)

 **(2) Business response parameters**

Data field description

|**Field** |**Type** |**Explanation** |
|---|---|---|
|task_id  |string  |Task ID for querying results |

### Request & Response Full Example

**Request example**

```JSON
{
    "req_key": "realman_avatar_picture_omni15_cv",
    "image_url": "https://xxxxx.jpg",
    // "mask_url": "https://xxxxx;...",
    "audio_url": "https://xxxxx",
    // "output_resolution": 720,
    //"callback_url": "https://xxxxx",  //string, callback POST address
    //"callback_auth_info": "xxxxx"    //string, Reserved fields for authentication purposes, intended for authentication on callback interfaces.
}
```

**Response example**

```JSON
{
    "code": 10000,    //Status code handling: Prioritize verifying code equals 10000
    "data": {
        "task_id": "7392616336519610409"
    },
    "message": "Success",
    "request_id": "20240720103939AF0029465CF6A74E51EC",    //Core information for error diagnosis and resolution
    "status": 10000,      //Attention not required, please ignore
    "time_elapsed": "104.852309ms"    //End-to-end link elapsed time
}
```

 **Error response example**

```JSON
{    
    "code": 50215,     //Status code handling: when code != 10000, please ignore “data”
    "data": null,     //Attention not required when code != 10000
    "message": "Input invalid for this service.",     //Error message
    "request_id": "20251128181411FCC2253709DF5006AD06",     //Core information for error diagnosis and resolution
    "status": 50215,     //Attention not required, please ignore
    "time_elapsed": "7.130776ms"    //End-to-end link elapsed time
}
```

**Callback example**

```JSON
{
    "callback_auth_info":"xxxxx",    //Reserved fields for authentication purposes, intended for authentication on callback interfaces.
    "code":10000,     //Status code handling: Prioritize verifying code equals 10000, followed by data.status. Failure to do so may result in parsing panic
    "data":{
        "resp_data":"{\"video_url\":\"https://xxxxx\"}",
        "status":"done"
    },
    "message":"Success",
    "req_key":"realman_avatar_picture_omni15_cv",
    "request_id":"20251223161349C28A0717806C4B4D53A1",    //Core information for error diagnosis and resolution
    "status":10000,            //Attention not required, please ignore
    "task_id":"9378742110847173614",    //Task id
    "time_elapsed":"441.507µs"     
}                   
```

## Query task

### **Request parameters**

 **(1) Request address**

|**Name** |**Content** |
|---|---|
|Interface address |[https://cv.byteplusapi.com](https://cv.byteplusapi.com) |
|Request method |POST  |
|Content\-Type |application/json |

**2) Query parameters**

> **Query** spliced after the URL, example: https://cv.byteplusapi.com/?Action=CVGetResult&Version=2024\-06\-06

|**Parameter** |**Optional/Required** |**Type** |**Explanation** |
|---|---|---|---|
|Action |Required |String  |Fixed value: CVGetResult |
|Version |Required |String |Fixed value: 2024\-06\-06 |

 **(3) Header request parameters**

> **The fixed values for this service are: **Service=cv**, **Region=****ap\-singapore\-1****

It is primarily used for authentication. For details, please refer to the "[Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters) \- Authentication Parameters \- in header"

|**Parameter** |**Optional/Required** |**Type** |**Explanation** |
|---|---|---|---|
|Authorization |Required |String |Format: HMAC\-SHA256 Credential={AccessKeyId}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}. |

 **(4) Body parameters**

|**Parameter** |**Optional/Required** |**Type** |**Explanation** |
|---|---|---|---|
|req_key  |Required |String  |Service identifier: **realman_avatar_picture_omni15_cv** |
|task_id  |Required |String  |Task ID, the value of this field is the return of the **submission task interface** |

### Response parameter

 **(1) General ** Response ** parameters**

Please refer to [Common Responses and Error Codes](https://docs.byteplus.com/en/docs/byteplus-vision/docs-common-responses-and-error-codes)

 **(2) Business ** Response ** parameters**

Business Response parameters:

> Business Response Parameters: Focus on the following fields in data; other fields are public returns (can be ignored or not parsed).

|Parameter Name |Description |remark |
|---|---|---|
|resp_data.video_url |Video link (valid for 1 hour) |Example:<br><br>"{\"progress\": 100, \"received_at\": 1756375407, \"processed_at\": 1756375407, \"finished_at\": 1756375408, \"gpu_type\": \"unknown\", \"binary_data_url_list\": [], \"binary_data_info_list\": [], \"vid\": \"v147efg5000cd2o0olfog65rstldjjag\", \"video_url\": \"https://xxxxx\", \"comfyui_cost\": 0.2478}" |
|status |Task execution status |status:<br><br>in_queue: Task submitted<br><br>generating: Task consumed and being processed<br><br>done: Processing completed (success or failure can be judged by the outer code & message)<br><br>not_found: Task not found (possible reasons: the task does not exist or has expired (12 hours))<br><br>expired: Task expired, please try to resubmit the task request<br><br>canceled: Task cancelled. |

### Request & Response Full Example

**Request example**

```JSON
{
    "req_key": "realman_avatar_picture_omni15_cv",
    "task_id": "<task_id returned by the task submission interface>"
}
```

**Response example**

```JSON
{
    "code": 10000,    //Status code handling: Prioritize verifying code equals 10000, followed by data.status. Failure to do so may result in parsing panic
    "data":{
        "resp_data":"{\"video_url\":\"https://xxxxx\"}",
        "status":"done"
    },
    "message": "Success",
    "request_id": "20250829122915429F7AC72EAA182E47E3",    //Core information for error diagnosis and resolution
    "status": 10000,      //Attention not required, please ignore
    "time_elapsed": "14.704612ms"
}
```

**Error response example**

```JSON
{
    "code": 50400,    //Status code handling: when code != 10000, please ignore “data”
    "data": null,    //Attention not required when code != 10000, please ignore
    "message": "Access Denied: Access Denied",     //Error message
    "request_id": "20251128170557851991094A144E04C521",    //Core information for error diagnosis and resolution
    "status": 50400,     //Attention not required, please ignore
    "time_elapsed": "494.205µs"    //End-to-end link elapsed time
}
```

## Cancel task

### **Request parameters**

 **(1) Request address**

|**Name** |**Content** |
|---|---|
|Interface address |[https://cv.byteplusapi.com](https://cv.byteplusapi.com) |
|Request method |POST  |
|Content\-Type |application/json |

 **(2) Query parameters**

> **Query** spliced after the URL, example: https://cv.byteplusapi.com/?Action=CVCancelTask&Version=2024\-06\-06

|**Parameter** |**Optional/Required** |**Type** |**Explanation** |
|---|---|---|---|
|Action |Required |String  |Fixed value: CVCancelTask |
|Version |Required |String |Fixed value: 2024\-06\-06 |

 **(3) Header request parameters**

> **The fixed values for this service are: **Service=cv**, **Region=****ap\-singapore\-1****

It is primarily used for authentication. For details, please refer to the "[Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters) \- Authentication Parameters \- in header"

|**Parameter** |**Optional/Required** |**Type** |**Explanation** |
|---|---|---|---|
|Authorization |Required |String |Format: HMAC\-SHA256 Credential={AccessKeyId}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}. |

 **(4) Body parameters**

|**Parameter** |**Optional/Required** |**Type** |**Explanation** |
|---|---|---|---|
|req_key  |Required |String  |Service identifier: **realman_avatar_picture_omni15_cv** |
|task_id  |Required |String  |Task ID, the value of this field is the return of the **submission task interface. ** <br><br>**Only** tasks with statuses of "in_queue" and "generating" can be cancelled. |

### Response parameter

 **(1) General ** Response ** parameters**

Please refer to [Common Responses and Error Codes](https://docs.byteplus.com/en/docs/byteplus-vision/docs-common-responses-and-error-codes)

 **(2) Business ** Response ** parameters**

Business Response parameters:

|Parameter Name |Description |remark |
|---|---|---|
|code |Return code |Return code 10000 indicates success. All other codes are error codes. |
|message |Detailed message |When the return code is not 10000, it will provide detailed error message. |

### Request & Response Full Example

**Request example**

```JSON
{
    "req_key": "realman_avatar_picture_omni15_cv",
    "task_id": "<task_id returned by the task submission interface>"
}
```

**Response example**

```JSON
{
    "code": 10000,        //Status code handling: Prioritize verifying code equals 10000, followed by data.status. Failure to do so may result in parsing panic
    "data": {
        "req_key": "realman_avatar_picture_omni15_cv",
        "task_id": "5539565225053838550"                //task id
    },
    "message": "Success",
    "request_id": "202512261639514FED3E1B836881892B0A",    //Core information for error diagnosis and resolution
    "status": 10000,        //Attention not required, please ignore
    "time_elapsed": "176.743021ms"      //End-to-end link elapsed time
}
```

**Error response example**

```JSON
{
    "code":50217,    //Status code handling: when code != 10000, please ignore “data”
    "data":null,    //Attention not required when code != 10000, please ignore
    "message":"Cancel not allow: task already been executed",    //Error message
    "request_id":"202512302034559DA308500B39AEAEB13C",    //Core information for error diagnosis and resolution
    "status":50217,    //Attention not required, please ignore
    "time_elapsed":"4.805987ms"    //End-to-end link elapsed time
}
```

## Error Codes

### **Common Error Codes**

Please refer to [Common Responses and Error Codes](https://docs.byteplus.com/en/docs/byteplus-vision/docs-common-responses-and-error-codes)

### Business Error Codes

|Http Code |Error Code |Error Message |Description |Retry |
|---|---|---|---|---|
|200 |10000 |No |Success |Not needed |
|429 |50429 |Request Has Reached API Limit, Please Try Later |QPS limit exceeded |**Retryable** |
|429 |50430 |Request Has Reached API Concurrent Limit, Please Try Later |Concurrency limit exceeded |**Retryable** |
|500 |50500 |Internal Error |Internal error |**Retryable** |
|500 |50501 |Internal RPC Error |Internal algorithmic error |**Retryable** |
|500 |50510 |Algovproxy Risk Error |Content Pre\-filter failed |Not needed |

## Integration Instructions

### SDK Usage Instructions

Please refer to [SDK Usage Instructions](https://docs.byteplus.com/en/docs/byteplus-vision/SDK-Usage-instructions)

### HTTP Access Instructions

Please refer to [HTTP Request Sample](https://docs.byteplus.com/en/docs/byteplus-vision/http_request_sample)

### API Key Usage Instructions

Please refer to [API Key Usage Instructions](https://docs.byteplus.com/en/docs/byteplus-vision/api-key-usage-instructions)
