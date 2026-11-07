---
title: "Create Flash Avatar"
product: "Vision AI"
product_code: "byteplus-vision"
source: "https://docs.byteplus.com/en/docs/byteplus-vision/Create-Flash-Avatar"
---

# Service Description

Generate a Flash Avatar using the training video.The video used must comply with the requirements specified in the [video shooting guidelines](https://docs.byteplus.com/en/docs/byteplus-vision/ShootingGuideonFlashAvatar).

The generated Flash Avatar can be used for [generating Flash Avatar videos](https://docs.byteplus.com/en/docs/byteplus-vision/generate-flash-avatar-video).

# Restrictions

|Name |Details |
|---|---|
|Video |* Format: .mp4 or .mov<br><br>* Size: Less than 500 MB.<br><br>* Duration: More than 3 seconds.  A 10\-15 second video is recommended. <br><br>* Resolution: At least 720p. 1080p is recommended.<br><br>* Frame rate: 25fps recommended.<br><br>* Bit rate: Greater than 20Mbps |

# Create Flash Avatar

## Submit task

### **Request parameters**

 **(1) Request address**

|Name |Content |
|---|---|
|Interface address |[https://cv.byteplusapi.com](https://cv.byteplusapi.com) |
|Request method |POST |
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

|**Name** |**Optional/Required** |**Type** |**Description** |
|---|---|---|---|
|req_key |Required |String |Service identifier: **realman_lipsync_training_tob**<br><br>fixed |
|video_url |Required |String |URL of the training video. The video used must comply with the requirements specified in the video shooting guidelines.  |
|alpha_url |Optional |String |Alpha Channel URL of the training video. This parameter is required if an Alpha Channel Video needs to be generated when generating Flash Avatar videos. |
|callback_url |Optional |String |Callback notification address for the results of the current generation task. When the status of the task changes to terminal state, service will send a POST request to this address. The content structure of the callback request is consistent with the response body of the Query Task, with the addition of an extra task_id field.<br><br>The task status returned in the callback:<br><br>done: Processing completed (success or failure can be judged by the outer code & message) <br><br>canceled: Task cancelled<br><br>If the callback fails, retry the callback three times at 1\-second intervals, with a 15\-second timeout for each attempt. |
|callback_auth_info |Optional |String |Reserved fields for authentication purposes, intended for authentication on callback interfaces. |

### **Response parameter**

 **(1) General response parameters**

Please refer to [Common Responses and Error Codes](https://docs.byteplus.com/en/docs/byteplus-vision/docs-common-responses-and-error-codes)

 **(2) Business response parameters**

Data field description

|**Field** |**Type** |**Explanation** |
|---|---|---|
|task_id  |String  |Task ID for querying results |

### **Request & Response Full Example**

**Request example**

```JSON
{
    "req_key": "realman_lipsync_training_tob",
    "video_url": "https://xxxxx",
    //"alpha_url": "https://xxxxx",
    //"callback_url": "https://xxxxx",  //string, callback POST address
    //"callback_auth_info": "xxxxx"    //string, Reserved fields for authentication purposes, intended for authentication on callback interfaces.
}
```

**Response example**

```JSON
{
    "code": 10000,    //Status code handling: Prioritize verifying code equals 10000
    "data": {
        "task_id": "1112273275"
    },
    "message": "Success",
    "request_id": "202511261757035824EF9C694A8E58DAF3",    //Core information for error diagnosis and resolution
    "status": 10000,      //Attention not required, please ignore
    "time_elapsed": "6.791315ms"    //End-to-end link elapsed time
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
    "data": {
        "binary_data_base64": [], 
        "resp_data": "{\"binary_data_info_list\":[],\"binary_data_url_list\":[],\"code\":0,\"face_position\":null,\"finished_at\":1764151081,\"gpu_type\":\"unknown\",\"message\":null,\"msg\":\"success\",\"processed_at\":1764151024,\"progress\":100,\"received_at\":1764151024,\"refuse_code\":[],\"resource_id\":\"xxxxx\",\"status\":null}",
        "status": "done"
    },
    "message":"Success",
    "req_key":"realman_lipsync_training_tob",
    "request_id":"20251223161349C28A0717806C4B4D53A1",    //Core information for error diagnosis and resolution
    "status":10000,            //Attention not required, please ignore
    "task_id":"9378742110847173614",    //Task id
    "time_elapsed":0            
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

 **(2) Query parameters**

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
|req_key  |Required |String  |Service identifier: **realman_lipsync_training_tob** |
|task_id  |Required |String  |Task ID, the value of this field is the return of the **submission task interface** |

### **Response parameter**

 **(1) General Response parameters**

Please refer to [Common Responses and Error Codes](https://docs.byteplus.com/en/docs/byteplus-vision/docs-common-responses-and-error-codes)

 **(2) Business Response parameters**

Business Response parameters:

> Business Response Parameters: Focus on the following fields in data; other fields are public returns (can be ignored or not parsed).

|Parameter Name |Description |Remark |
|---|---|---|
|resp_data.resource_id |Resource ID of the trained Flash Avatar |Unique identifier for the corresponding trained Flash Avatar. |
|status |Task execution status |status:<br><br>in_queue: Task submitted<br><br>generating: Task consumed and being processed<br><br>done: Processing completed (success or failure can be judged by the outer code & message)<br><br>not_found: Task not found (possible reasons: the task does not exist or has expired (12 hours))<br><br>expired: Task expired, please try to resubmit the task request<br><br>canceled: Task cancelled |

### **Request & Response Full Example**

**Request example**

```JSON
{
    "req_key": "realman_lipsync_training_tob",
    "task_id": "<task_id returned by the task submission interface>"
}
```

**Response example**

```JSON
{
    "code": 10000,     //Status code handling: Prioritize verifying code equals 10000, followed by data.status. Failure to do so may result in parsing panic
    "data": {
        "binary_data_base64": [], 
        "resp_data": "{\"binary_data_info_list\":[],\"binary_data_url_list\":[],\"code\":0,\"face_position\":null,\"finished_at\":1764151081,\"gpu_type\":\"unknown\",\"message\":null,\"msg\":\"success\",\"processed_at\":1764151024,\"progress\":100,\"received_at\":1764151024,\"refuse_code\":[],\"resource_id\":\"xxxxx\",\"status\":null}",
        "status": "done"
    },
    "message": "Success", 
    "request_id": "20251126154220485785F99872DD5931C4",     //Core information for error diagnosis and resolution
    "status": 10000,      //Attention not required, please ignore
    "time_elapsed": "15.032651ms"    //End-to-end link elapsed time
}
```

**Error response example**

```JSON
{
    "code": 50400,    //Status code handling: when code != 10000, please ignore “data”
    "data": null,    //Attention not required when code != 10000, please ignore
    "message": "Access Denied: Access Denied",     //Error message
    "request_id": "20251128170557851991094A144E04C521",    //Core information for error diagnosis and resolution
    "status": 50400, //Attention not required, please ignore
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
|req_key  |Required |String  |Service identifier: **realman_lipsync_training_tob** |
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
    "req_key": "realman_lipsync_training_tob",
    "task_id": "<task_id returned by the task submission interface>"
}
```

**Response example**

```JSON
{
    "code": 10000,        //Status code handling: Prioritize verifying code equals 10000, followed by data.status. Failure to do so may result in parsing panic
    "data": {
        "req_key": "realman_lipsync_training_tob",
        "task_id": "14597992595293864900"                //task id
    },
    "message": "Success",
    "request_id": "20251229144801297FBA65ED9BD661BF63",    //Core information for error diagnosis and resolution
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
