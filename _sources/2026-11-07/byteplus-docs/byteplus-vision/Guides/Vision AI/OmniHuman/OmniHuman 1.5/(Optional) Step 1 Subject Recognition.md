---
title: "(Optional) Step 1 Subject Recognition"
product: "Vision AI"
product_code: "byteplus-vision"
source: "https://docs.byteplus.com/en/docs/byteplus-vision/omnihuman-subject_recognition"
---

# Service Description

To determine if an image contains a human or human\-like subject before using it in other services, you can use the Subject Recognition API. This document provides the complete API reference, detailing how to submit an image for asynchronous detection and query for the result. It covers all necessary parameters, request examples, and response specifications to guide your integration.

# Restrictions

|Name |Details |
|---|---|
|Image Requirements |* Format: Common formats such as JPG (JPEG), PNG, JFIF; **JPG is recommended as the preferred format**<br><br>* Size: Less than 5 MB, resolution less than 4096\*4096; the clearer the input image, the better the generation effect.<br><br>* Additional Recommendation: If a speaker needs to be specified, **subject detection** must be performed first; if not, subject detection can be skipped. |

# Subject Recognition

## Submit tasks

### **Request parameters**

 **(1) Request address**

|**Name** |**Content** |
|---|---|
|Interface address |[https://cv.byteplusapi.com](https://cv.byteplusapi.com) |
|Request method |POST |
|Content\-Type |application/json |

 **(2) Query parameters**

**Query** spliced after the URL, example: https://cv.byteplusapi.com/?Action=CVSubmitTask&Version=2024\-06\-06

|**Parameter** |**Optional/Required** |**Type** |**Explanation** |
|---|---|---|---|
|Action |Required |String |Fixed value: CVSubmitTask |
|Version |Required |String |Fixed value: 2024\-06\-06 |

 **(3) Header request parameters**

It is primarily used for authentication. For details, please refer to the "[Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters) \- Authentication Parameters \- in header"

|**Parameter** |**Optional/Required** |**Type** |**Explanation** |
|---|---|---|---|
|Authorization |Required |String |Format: HMAC\-SHA256 Credential={AccessKeyId}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}. |

 **(4) Body parameters**

Service request parameter

|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|req_key |string |Yes |Service identifier: **realman_avatar_picture_create_role_omni_cv**<br><br>fixed |
|image_url |string |Yes |URL link of the portrait image |
|callback_url |string |No |Callback notification address for the results of the current generation task. When the status of the task changes to terminal state, service will send a POST request to this address. The content structure of the callback request is consistent with the response body of the Query Task, with the addition of an extra task_id field.<br><br>The task status returned in the callback:<br><br>done: Processing completed (success or failure can be judged by the outer code & message)<br><br>canceled: Task cancelled<br><br>If the callback fails, retry the callback three times at 1\-second intervals, with a 15\-second timeout for each attempt. |
|callback_auth_info |string |No |Reserved fields for authentication purposes, intended for authentication on callback interfaces. |

### Response parameter

 **(1) General response parameters**

Please refer to [Common Responses and Error Codes](https://docs.byteplus.com/en/docs/byteplus-vision/docs-common-responses-and-error-codes)

 **(2) Business response parameters**

Data field description

|**Field** |**Type** |**Explanation** |
|---|---|---|
|task_id |string |Task ID for querying results |

### Request & Response Full Example

**Request example**

```JSON
{
    "req_key": "realman_avatar_picture_create_role_omni_cv",
    "image_url": "https://xxxxx.jpg",
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
    "data": {
        "binary_data_base64": [], 
        "resp_data": "{\"status\":1}", 
        "status": "done"
    }, 
    "message":"Success",
    "req_key":"realman_avatar_picture_create_role_omni_cv",
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
|Request method |POST |
|Content\-Type |application/json |

 **(2) Query parameters**

**Query** spliced after the URL, example: https://cv.byteplusapi.com/?Action=CVGetResult&Version=2024\-06\-06

|**Parameter** |**Optional/Required** |**Type** |**Explanation** |
|---|---|---|---|
|Action |Required |String |Fixed value: CVGetResult |
|Version |Required |String |Fixed value: 2024\-06\-06 |

 **(3) Header request parameters**

It is primarily used for authentication. For details, please refer to the "[Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters) \- Authentication Parameters \- in header"

|**Parameter** |**Optional/Required** |**Type** |**Explanation** |
|---|---|---|---|
|Authorization |Required |String |Format: HMAC\-SHA256 Credential={AccessKeyId}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}. |

 **(4) Body parameters**

|**Parameter** |**Optional/Required** |**Type** |**Explanation** |
|---|---|---|---|
|req_key |Required |String |Service identifier: **realman_avatar_picture_create_role_omni_cv** |
|task_id |Required |String |Task ID, the value of this field is the return of the **submission task interface** |

### Response parameter

 **(1) General** Response **parameters**

Please refer to [Common Responses and Error Codes](https://docs.byteplus.com/en/docs/byteplus-vision/docs-common-responses-and-error-codes)

 **(2) Business** Response **parameters**

Business Response parameters:

> Business Response Parameters: Focus on the following fields in data; other fields are public returns (can be ignored or not parsed).

|Parameter Name |Description |remark |
|---|---|---|
|resp_data |Image Recognition Result |resp_data is a serialized JSON string. The status parameter within it indicates the recognition result, with possible values:<br><br><br>* 0: Does not contain humans, human\-like subjects, anthropomorphic subjects, or similar entities.<br><br>* 1: Contains humans, human\-like subjects, anthropomorphic subjects, or similar entities.<br><br><br>Example:<br><br>"{'code': 10000, 'data': {'binary_data_base64': [], 'resp_data': '{"status":1}', 'status': 'done'}, 'message': 'Success', 'request_id': '2025xxxxxxxxx', 'status': 10000, 'time_elapsed': '6.292875ms'}" |
|status |Task execution status |status:<br><br>in_queue: Task submitted<br><br>generating: Task consumed and being processed<br><br>done: Processing completed (success or failure can be judged by the outer code & message)<br><br>not_found: Task not found (possible reasons: the task does not exist or has expired (12 hours))<br><br>expired: Task expired, please try to resubmit the task request<br><br>canceled: Task cancelled |

### Request & Response Full Example

**Request example**

```JSON
{
    "req_key": "realman_avatar_picture_create_role_omni_cv",
    "task_id": "<task_id returned by the task submission interface>"
}
```

**Response example**

```JSON
{
    "code": 10000,     //Status code handling: Prioritize verifying code equals 10000, followed by data.status. Failure to do so may result in parsing panic
    "data": {
        "binary_data_base64": [], 
        "resp_data": "{\"status\":1}", 
        "status": "done"
        }, 
     "message": "Success", 
     "request_id": "202511281848165B04AC671560AC03C130", //Core information for error diagnosis and resolution
     "status": 10000,      //Attention not required, please ignore
     "time_elapsed": "6.292875ms"
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
