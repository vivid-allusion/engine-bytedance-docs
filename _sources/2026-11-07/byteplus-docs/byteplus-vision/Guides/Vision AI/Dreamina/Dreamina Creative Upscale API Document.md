---
title: "Dreamina Creative Upscale API Document"
product: "Vision AI"
product_code: "byteplus-vision"
source: "https://docs.byteplus.com/en/docs/byteplus-vision/dreamina-ultra-hd"
---

# Service Description

Dreamina Smart Creative Upscale identical image editing feature:

Built on the Seedream base model, it targets AIGC\-generated scenarios and low\-quality images. While preserving global structure and semantic consistency, it moderately relaxes rigid consistency constraints to generate richer details and comprehensively enhance image texture. Currently, it supports upscaling images to 2K/4K resolution.

# Restrictions

|Name |Details |
|---|---|
|Input Image |* Format: Only JPEG and PNG are supported; JPEG is recommended.<br><br>* Size: Maximum 4.7MB<br><br>* Resolution: Maximum 4096 × 4096 pixels.<br><br>* The aspect ratio shall be maintained between 1/3 and 3. |

## Submit task

### **Request parameters**

 **(1) Request address**

|Name |Content |
|---|---|
|Interface address |[https://cv.byteplusapi.com](https://cv.byteplusapi.com) |
|Request method |POST |
|Content\-Type |application/json |

 **(2) Query parameters**

> **Query** spliced after the URL, example: https://cv.byteplusapi.com/?Action=CVSync2AsyncSubmitTask&Version=2024\-06\-06

|**Parameter** |**Optional/Required** |**Type** |**Explanation** |
|---|---|---|---|
|Action |Required |String  |Fixed value: **CVSync2AsyncSubmitTask** |
|Version |Required |String |Fixed value: **2024\-06\-06** |

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
|req_key |Required |String |Service identifier: **i2i_seed3_tilesr_cvtob_bp**<br><br>fixed |
|binary_data_base64 |Required (Choose one of the two)<br><br> |array of string |Image file Base64 encoding: one image required |
|image_urls |||Image file URL: one image required |
|resolution |Optional |String |Image resolution, optional values:<br><br>Default value: "2k"<br><br>Available options: ["2k", "4k"] |
|scale |Optional |Int |Degree of Detail Generation<br><br>Default value: 50<br><br>Value range: [0, 100] |
|callback_url |Optional |String |Callback notification address for the results of the current generation task. When the status of the task changes to done, service will send a POST request to this address. The content structure of the callback request is consistent with the response body of the Query Task, with the addition of an extra task_id field.<br><br>The task status returned in the callback:<br><br>done: Processing completed (success or failure can be judged by the outer code & message) <br><br>canceled: Task canceled<br><br>If the callback fails, retry the callback three times at 1\-second intervals, with a 15\-second timeout for each attempt. |
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
    "req_key": "i2i_seed3_tilesr_cvtob_bp",
    "image_urls": [
        "https://xxxx"
    ],
    "resolution": "2k"
}
```

**Response example**

```JSON
{
    "code": 10000,    //Status code handling: Prioritize verifying code equals 10000
    "data": {
        "task_id": "3941025814847436723"    //Core information for error diagnosis and resolution
    },
    "message": "Success",
    "request_id": "202511261807114C4542705F784354C6D7",
    "status": 10000,      //Attention not required, please ignore
    "time_elapsed": "2.207617745s"    //End-to-end link elapsed time
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

## Query task

### **Request parameters**

 **(1) Request address**

|**Name** |**Content** |
|---|---|
|Interface address |[https://cv.byteplusapi.com](https://cv.byteplusapi.com) |
|Request method |POST  |
|Content\-Type |application/json |

 **(2) Query parameters**

> **Query** spliced after the URL, example: https://cv.byteplusapi.com/?Action=CVSync2AsyncGetResult&Version=2024\-06\-06

|**Parameter** |**Optional/Required** |**Type** |**Explanation** |
|---|---|---|---|
|Action |Required |String  |Fixed value: **CVSync2AsyncGetResult** |
|Version |Required |String |Fixed value: **2024\-06\-06** |

 **(3) Header request parameters**

> **The fixed values for this service are: **Service=cv**, **Region=****ap\-singapore\-1****

It is primarily used for authentication. For details, please refer to the "[Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters) \- Authentication Parameters \- in header"

|**Parameter** |**Optional/Required** |**Type** |**Explanation** |
|---|---|---|---|
|Authorization |Required |String |Format: HMAC\-SHA256 Credential={AccessKeyId}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}. |

 **(4) Body parameters**

|**Parameter** |**Optional/Required** |**Type** |**Explanation** |
|---|---|---|---|
|req_key  |Required |String  |Service identifier: **i2i_seed3_tilesr_cvtob_bp** |
|task_id  |Required |String  |Task ID, the value of this field is the return of the **submission task interface** |

### **Response parameter**

 **(1) General Response parameters**

Please refer to [Common Responses and Error Codes](https://docs.byteplus.com/en/docs/byteplus-vision/docs-common-responses-and-error-codes)

 **(2) Business Response parameters**

Business Response parameters:

> Business Response Parameters: Focus on the following fields in data; other fields are public returns (can be ignored or not parsed).

|Parameter Name |Type |Description |
|---|---|---|
|image_urls |array of string |Returns an array of image URLs, with the output images in PNG format. |
|status |String |Task execution status:<br><br>in_queue: Task submitted<br><br>generating: Task consumed and being processed<br><br>done: Processing completed (success or failure can be judged by the outer code & message)<br><br>not_found: Task not found (possible reasons: the task does not exist or has expired (12 hours))<br><br>expired: Task expired, please try to resubmit the task request<br><br>canceled: Task canceled |

### **Request & Response Full Example**

**Request example**

```JSON
{
    "req_key": "i2i_seed3_tilesr_cvtob_bp",
    "task_id": "<task_id returned by the task submission interface>"
}
```

**Response example**

```JSON
{
    "code": 10000, //Status code handling: Prioritize verifying code equals 10000, followed by data.status. Failure to do so may result in parsing panic
    "data": {
        "image_urls": [
            "https://xxxx"
        ],
        "status":"done"
    },
    "message": "Success",
    "status": 10000,  //Attention not required, please ignore
    "request_id": "2025061718460554C9B78D23B0BAB45B2A",  //Core information for error diagnosis and resolution
    "time_elapsed": "508.312154ms"    //End-to-end link elapsed time
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
|req_key  |Required |String  |Service identifier: **i2i_seed3_tilesr_cvtob_bp** |
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
    "req_key": "i2i_seed3_tilesr_cvtob_bp",
    "task_id": "<task_id returned by the task submission interface>"
}
```

**Response example**

```JSON
{
    "code": 10000,        //Status code handling: Prioritize verifying code equals 10000, followed by data.status. Failure to do so may result in parsing panic
    "data": {
        "req_key": "i2i_seed3_tilesr_cvtob_bp",
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
