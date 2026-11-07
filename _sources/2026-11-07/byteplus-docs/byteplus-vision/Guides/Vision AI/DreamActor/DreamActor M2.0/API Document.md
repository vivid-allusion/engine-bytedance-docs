---
title: "API Document"
product: "Vision AI"
product_code: "byteplus-vision"
source: "https://docs.byteplus.com/en/docs/byteplus-vision/dreamactor-m2-0-api-document"
---

# Service Description

DreamActor M2.0 is the motion control feature driven by the large model. By inputting a single image and a template video, it can drive the character in the image to replicate the **motion, facial expressions, and lip movements** from the template video, while preserving the subject and background features of the input image consistently.

# Restrictions

|Name |Details |
|---|---|
|Image |* Format: jpeg, jpg or png<br><br>* Size: maximum 4.7 MB<br><br>* Resolution: between 480✖️480 and 1920✖️1080 (anything larger will be proportionally reduced)<br><br><br>Image supports driving for real people, animation, pets, etc.; overly abstract subjects may fail to generate. |
|Video |* Format: mp4, mov or webm<br><br>* Duration: maximum 30 seconds<br><br>* Resolution: between 200✖️200 and 2048✖️1440(2K)<br><br><br>It supports both facial expressions and body movement driving, and can handle full\-body, half\-body, or portrait driving:<br><br>Driving source: Video (supports real people, animation, pets)<br><br>Driving range: Full face + body<br><br>Note: We recommend that the number of people in the selected video template **matches** the number of people in the image for driving. Alternatively, using a **single\-person video** to drive multi\-person images will provide more stable performance. |

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
|req_key |Required |String |Service identifier: **dreamactor_m20_gen_video_cvtob**<br><br>fixed |
|binary_data_base64 |<br>Required<br><br><br><br>(select either one)<br> |array of String |Base64\-encoded image file: 1 image required. |
|image_urls ||array of String |Image file URL: 1 image required. |
|video_url |Required |String |Video URL (public internet access required) |
|cut_result_first_second_switch |Optional |Bool |Whether to crop the first second of the output video (there is a 1\-second transition at the beginning of the output video; this parameter can be used to crop it)<br><br>Default value: true |

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
    "req_key": "dreamactor_m20_gen_video_cvtob",
    // "binary_data_base64": [],
    "image_urls": [
        "https://xxxx"
    ],
    "video_url": "https://xxxx"
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
|req_key  |Required |String  |Service identifier: **dreamactor_m20_gen_video_cvtob** |
|task_id  |Required |String  |Task ID, the value of this field is the return of the **submission task interface** |

### **Response parameter**

 **(1) General Response parameters**

Please refer to [Common Responses and Error Codes](https://docs.byteplus.com/en/docs/byteplus-vision/docs-common-responses-and-error-codes)

 **(2) Business Response parameters**

Business Response parameters:

> Business Response Parameters: Focus on the following fields in data; other fields are public returns (can be ignored or not parsed).

|Parameter Name |Description |Remark |
|---|---|---|
|resp_data.video_url |String |URL of the generated video(valid for 1 hour) |
|aigc_meta_tagged |Bool |Whether the implicit watermark is successfully marked |
|status |String |Task execution status:<br><br>in_queue: Task submitted<br><br>generating: Task consumed and being processed<br><br>done: Processing completed (success or failure can be judged by the outer code & message)<br><br>not_found: Task not found (possible reasons: the task does not exist or has expired (12 hours))<br><br>expired: Task expired, please try to resubmit the task request<br><br>canceled: Task canceled |

### **Request & Response Full Example**

**Request example**

```JSON
{
    "req_key": "dreamactor_m20_gen_video_cvtob",
    "task_id": "<task_id returned by the task submission interface>"
}
```

**Response example**

```JSON
{
    "code": 10000, //Status code handling: Prioritize verifying code equals 10000, followed by data.status. Failure to do so may result in parsing panic
    "data": {
        "resp_data":"{\"Duration\":\"10.12\",\"video_url\":\"http://xxxxx\"}",
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
