---
title: "(Optional) Step 2 Subject Detection"
product: "Vision AI"
product_code: "byteplus-vision"
source: "https://docs.byteplus.com/en/docs/byteplus-vision/omnihuman-subject_detection"
---

# Service Description

Step 2 detects subjects in images and supports returning mask images corresponding to the subjects. **This step can be skipped** if there's no need to specify a subject to speak during video generation.

# Restrictions

|Name |Details |
|---|---|
|Image Requirements |* Format: Common formats such as JPG (JPEG), PNG, JFIF; **JPG is recommended as the preferred format**<br><br>* Size: Less than 5 MB, resolution less than 4096\*4096; the clearer the input image, the better the generation effect.<br><br>* Additional Recommendation: If a speaker needs to be specified, **subject detection** must be performed first; if not, subject detection can be skipped. |

# Subject Detection

## Submit tasks

### **Request parameters**

 **(1) Request address**

|**Name** |**Content** |
|---|---|
|Interface address |[https://cv.byteplusapi.com](https://cv.byteplusapi.com) |
|Request method |POST |
|Content\-Type |application/json |

 **(2) Query parameters**

**Query** spliced after the URL, example: https://cv.byteplusapi.com/?Action=CVSync2AsyncSubmitTask&Version=2024\-06\-06

|**Parameter** |**Optional/Required** |**Type** |**Explanation** |
|---|---|---|---|
|Action |Required |String |Fixed value: CVSync2AsyncSubmitTask |
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
|req_key |string |Yes |Service identifier: **realman_avatar_object_detection_cv**<br><br>fixed |
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
    "req_key": "realman_avatar_object_detection_cv",
    "image_url": "https://xxxxx.jpg",
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
|req_key  |Required |String  |Service identifier: **realman_avatar_object_detection_cv** |
|task_id  |Required |String  |Task ID, the value of this field is the return of the **submission task interface** |

### **Response parameter**

 **(1) General Response parameters**

Please refer to [Common Responses and Error Codes](https://docs.byteplus.com/en/docs/byteplus-vision/docs-common-responses-and-error-codes)

 **(2) Business Response parameters**

Business Response parameters:

> Business Response Parameters: Focus on the following fields in data; other fields are public returns (can be ignored or not parsed).

|Parameter Name |**Type** |Description |remark |
|---|---|---|---|
|resp_data |JSON string |Subject Detection Result<br><br><br>* code: Error Code. 0 indicates success.<br><br>* status: Whether the subject is detected. 0 means no subject is detected, and 1 means the subject is detected.<br><br>* object_detection_result.mask.url (Field to focus on): The order of the URL list and the subjects in the input images are sorted **in descending order of mask area** (from largest to smallest). If you need to preview the mask images, you can download them via the URLs, manually change the file name extension to .png, and save them as .png files before viewing. |Example:<br><br>{'code': 10000, 'data': {'resp_data': '{"code":0,"object_detection_result":{"mask":{"url":[\"https://xxxxx\"]}},"status":1}'}, 'message': 'Success', 'request_id': '202509231217222E094AB54EF8C50A04E3', 'status': 10000, 'time_elapsed': '3.964553804s'} |

### **Request & Response Full Example**

**Request example**

```JSON
{
    "req_key": "realman_avatar_object_detection_cv",
    "task_id": "<task_id returned by the task submission interface>"
}
```

**Response example**

```JSON
{
    "code": 10000,
    "data": {
        "resp_data": "{\"code\":0,\"object_detection_result\":{\"mask\":{\"url\":[\"https://xxxxx\"]}},\"status\":1}"
    },
    "message": "Success",
    "request_id": "202509231217222E094AB54EF8C50A04E3",
    "status": 10000,
    "time_elapsed": "3.964553804s"
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
