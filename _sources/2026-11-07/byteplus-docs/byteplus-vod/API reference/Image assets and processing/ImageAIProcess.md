---
title: "ImageAIProcess"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-imageaiprocess"
---

Submits an AI super\-resolution task for an image asset.

The response indicates that the task was submitted. To obtain the final result, call [GetImageProcessTasks](https://docs.byteplus.com/docs/byteplus-vod/reference-getimageprocesstasks) or subscribe to [ImageProcessComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-imageprocesscomplete).

For input size, dimension, and output limits, see [Image enhancement and processing](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement#limits-and-configuration).

## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=ImageAIProcess&Version=2023\-07\-01

HTTP method: POST

## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

### Query parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ImageAIProcess` |The API action. For this operation, set the value to `ImageAIProcess`. |
|Version |String |Yes |`2023-07-01` |The API version. For this operation, set the value to `2023-07-01`. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Pid |String |Yes |`i186a8gm0018dbhefdqtgd69okvmf9pg` |The image asset ID (Pid). |
|ProcessType |String |Yes |`AISuperResolution` |The AI processing type. Set this value to `AISuperResolution`. |
|WorkflowParameter |String |Yes |`{"Input":{},"GenDREnhanceParam":{"Multiple":2.7}}` |The AI processing parameters, serialized as a JSON string. See [WorkflowParameter](https://docs.byteplus.com/en/docs/25/124098#workflowparameter). |
|SpaceName |String |No |`meter-space` |The space name. You can call [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) to obtain the space names under your account. |
|CallbackArgs |String |No |`""` |The custom information passed through to the completion callback. |

### WorkflowParameter

Serialize the following object as a JSON string when setting `WorkflowParameter`. `GenDREnhanceParam.Multiple` specifies the super\-resolution scale factor. The supported range is 1.1 to 30, subject to the output dimension limit.

```json
{
    "Input": {},
    "GenDREnhanceParam": {
        "Multiple": 2.7
    }
}
```

## Response parameters

For API\-specific response parameters, see the following tables. For common response parameters, see [Response](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#response).

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Pid |String |`i186a8gm0018dbhefdqtgd69okvmf9pg` |The image asset ID (Pid). |
|Status |String |`pending` |The submission status. A successfully submitted task returns `pending`. |
|TaskId |String |`d44f72f76b3372a3bf5d6206801f9bfc` |The image processing task ID. |
|ProcessType |String |`AISuperResolution` |The normalized processing type: `Basic` or `AISuperResolution`. |

## Samples

### Sample request

```http
POST /?Action=ImageAIProcess&Version=2023-07-01 HTTP/1.1
Host: vod.byteplusapi.com
Content-Type: application/json
```

```json
{
    "Pid": "i186a8gm0018dbhefdqtgd69okvmf9pg",
    "SpaceName": "meter-space",
    "ProcessType": "AISuperResolution",
    "WorkflowParameter": "{\"Input\":{},\"GenDREnhanceParam\":{\"Multiple\":2.7}}"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20261029**********************",
        "Action": "ImageAIProcess",
        "Version": "2023-07-01",
        "Service": "vod",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Pid": "i186a8gm0018dbhefdqtgd69okvmf9pg",
        "ProcessType": "AISuperResolution",
        "TaskId": "d44f72f76b3372a3bf5d6206801f9bfc",
        "Status": "pending"
    }
}
```

## Error codes

For common error codes, see [Common error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
