---
title: "Dreamina 4.6 API Document"
product: "Vision AI"
product_code: "byteplus-vision"
source: "https://docs.byteplus.com/en/docs/byteplus-vision/dreamina_4_6"
---

# Service Description

Dreamina 4.6 \- in\-house image generation capabilities originated from the same underlying technology as Dreamina.

Built upon the Seedream 4.0 foundational model, this image generation variant is optimized for mainstream photo editing scenarios, delivering enhanced results across portrait photography, graphic design, and artistic image stylization.

# Restrictions

|Name |Details |
|---|---|
|Input Image |* Format: Only JPEG and PNG are supported; JPEG is recommended.<br><br>* Size: Maximum 15MB, with up to 14 input images allowed.<br><br>* Resolution: Maximum 4096 × 4096 pixels. |
|Output Image |* For detailed width and height rules of output images, refer to the parameter descriptions in width and height below.<br><br>* Output images will be returned as a list. The maximum number of output images = 15 − number of input images; it is recommended to output no more than 9 images. |
|Additional Notes |* Higher resolution and larger quantities of input/output images will result in more noticeable latency increases.<br><br>* A single call may return multiple images, and billing is based on the number of output images. By default, the number of output images is determined by the model’s understanding of the prompt intent.<br><br>* If latency and cost are sensitive, it is recommended to use the force_single parameter to enforce the output of only 1 image. |

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
|req_key |Required |String |Service identifier: **jimeng_seedream46_cvtob**<br><br>fixed |
|image_urls |Optional |Array of String<br><br> |URLs of input images. Supports 0 to 14 images.<br><br><br>* Larger quantities and larger image sizes will significantly increase the service processing time.<br><br>* It is recommended to limit input images to 6 or fewer; excessive images may degrade output quality. |
|prompt |Required |String |Text prompt for image generation. Supports both Chinese and English input. Recommendations:<br><br><br>* Maximum length: 800 characters. Overly long prompts may cause abnormal generation or failure.<br><br>* Supports directly specifying the output aspect ratio in the prompt; the model will intelligently determine the width/height ratio based on the "size" field. The default output is a 2K resolution image with an aspect ratio ≤ 3.<br><br>* Except for "", special symbols such as $ are not recommended. |
|size |Optional<br><br> <br><br>**Text\-to\-image scenario**:<br><br><br>* Either size or width+height must be provided. If neither is provided, the default area is 4,194,304 (2048×2048), generating a 2K resolution image with a model\-determined aspect ratio.<br><br>* If both size and width+height are provided, <br><br><br>width+height takes precedence.<br><br><br>* If only the area is provided, the model will intelligently determine the aspect ratio of the generated image based on the user's prompt intent.<br><br><br>**Image\-to\-image scenario**:<br><br><br>* The model will intelligently determine the output aspect ratio based on the prompt and the reference image dimensions. |Int<br><br> |Area of the generated image.<br><br><br>* Default value: 4,194,304 (2048×2048), generating a 2K resolution image.<br><br>* Valid range: [1024×1024, 4096×4096], supporting 1K to 4K resolution images. |
|width ||Int |Width and height of the generated image; this field is not passed by default.<br><br><br>* The product of width and height must be within the range [1024×1024, 4096×4096], and the aspect ratio must be between [min_ratio, max_ratio].<br><br>* Both width and height must be provided together to take effect.<br><br><br>Recommended optional width/height combinations:<br><br><br>* 1K<br><br>   * 1024x1024 （1:1）<br><br>* 2K<br><br>   * 2048x2048 （1:1）<br><br>   * 2304x1728（4:3）<br><br>   * 2496x1664 （3:2）<br><br>   * 2560x1440 （16:9）<br><br>   * 3024x1296 （21:9）<br><br>* 4K<br><br>   * 4096x4096 （1:1）<br><br>   * 4736x3552（4:3）<br><br>   * 5024x3360 （3:2）<br><br>   * 5472x2072 （16:9）<br><br>   * 6272x2688 （21:9） |
|height ||Int ||
|scale |Optional |Int |The degree of influence from the text prompt. A larger value means the text prompt has stronger influence, while the input images have weaker influence.<br><br><br>* Default value: 50<br><br>* Valid range: [1, 100] |
|force_single |Optional |Bool |Whether to force the generation of a single image.<br><br>Default：false<br><br>**Note**:<br><br><br>* More images in a group will result in longer processing time, and the latency will increase significantly with the number of images.<br><br>* For stable group image output, it is recommended to limit the number of images in the prompt to **9 or fewer**.<br><br>* When generating group images, it is advised to explicitly specify the image resolution in the prompt or pass specific width/height values, to avoid API errors caused by inconsistent resolutions across generated images. |
|min_ratio |Optional |Float |The aspect ratio (width/height) of the generated image must be ≥ min_ratio. If the automatically selected ratio is smaller than min_ratio, min_ratio will be used instead.<br><br><br>* Default value: 1/3<br><br>* Valid range: [1/16, 16) |
|max_ratio |Optional |Float |The aspect ratio (width/height) of the generated image must be ≤ max_ratio. If the automatically selected ratio is larger than max_ratio, max_ratio will be used instead.<br><br><br>* Default value: 3<br><br>* Valid range: (1/16, 16] |
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
    "req_key": "jimeng_seedream46_cvtob",
    "image_urls": [
        "https://xxxx",
        // ...
    ],
    "prompt": "generate a person with a red hair and a blue shirt"
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
|req_key  |Required |String  |Service identifier: **jimeng_seedream46_cvtob** |
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
    "req_key": "jimeng_seedream46_cvtob",
    "task_id": "<task_id returned by the task submission interface>"
}
```

**Response example**

```JSON
{
    "code": 10000, //Status code handling: Prioritize verifying code equals 10000, followed by data.status. Failure to do so may result in parsing panic
    "data": {
        "image_urls": [
            "https://xxxx",
            // ...
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
|req_key  |Required |String  |Service identifier: **jimeng_seedream46_cvtob** |
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
    "req_key": "jimeng_seedream46_cvtob",
    "task_id": "<task_id returned by the task submission interface>"
}
```

**Response example**

```JSON
{
    "code": 10000,        //Status code handling: Prioritize verifying code equals 10000, followed by data.status. Failure to do so may result in parsing panic
    "data": {
        "req_key": "jimeng_seedream46_cvtob",
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
