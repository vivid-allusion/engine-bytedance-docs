---
title: "GetImageProcessTasks"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-getimageprocesstasks"
---

Lists processing tasks for an image asset. You can filter the results by task ID or task status.

## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=GetImageProcessTasks&Version=2023\-07\-01

HTTP method: POST

## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

### Query parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetImageProcessTasks` |The API action. For this operation, set the value to `GetImageProcessTasks`. |
|Version |String |Yes |`2023-07-01` |The API version. For this operation, set the value to `2023-07-01`. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|SpaceName |String |Yes |`meter-space` |The space name. You can call [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) to obtain the space names under your account. |
|Pid |String |Yes |`i186a8gm0018dbhefdqtgd69okvmf9pg` |The image asset ID (Pid). |
|TaskId |String |No |`d44f72f76b3372a3bf5d6206801f9bfc` |The image processing task ID. When specified, an exact match is required. |
|Status |String |No |`success` |The task status: `pending`, `processing`, `success`, or `failed`. |
|Offset |Long |No |`0` |The data offset. Default: 0. Must be greater than or equal to 0. |
|Limit |Long |No |`20` |The maximum number of tasks to return. Default: 20. Maximum: 100. |

## Response parameters

For API\-specific response parameters, see the following tables. For common response parameters, see [Response](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#response).

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TaskSet |Array of [VodImageProcessTask](https://docs.byteplus.com/en/docs/25/124100#vodimageprocesstask) |`-` |The tasks, sorted by `CreateTime` in descending order, then by `TaskId` in descending order. |
|TotalCount |Long |`1` |The total number of results that match the filters. |

### VodImageProcessTask

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Pid |String |`i186a8gm0018dbhefdqtgd69okvmf9pg` |The image asset ID (Pid). |
|Output |Object of [VodImageProcessTaskOutput](https://docs.byteplus.com/en/docs/25/124100#vodimageprocesstaskoutput) |`-` |The output file information. Image URLs are not returned by this operation. Call [GetImageInfos](https://docs.byteplus.com/docs/byteplus-vod/reference-getimageinfos) to obtain the image URLs. |
|Status |String |`success` |The task status: `pending`, `processing`, `success`, or `failed`. |
|TaskId |String |`d44f72f76b3372a3bf5d6206801f9bfc` |The image processing task ID. |
|ErrorCode |String |`-` |The error code, returned only when `Status` is `failed`. |
|CreateTime |Long |`1792061082` |The creation time, as a Unix timestamp in seconds. |
|UpdateTime |Long |`1792064087` |The last update time, as a Unix timestamp in seconds. |
|ProcessType |String |`AISuperResolution` |The normalized processing type: `Basic` or `AISuperResolution`. |
|ErrorMessage |String |`-` |The error message, returned only when `Status` is `failed`. |
|ProcessParameter |String |`{"GenDREnhanceParam":{"Multiple":2.7},"Input":{}}` |The normalized image processing parameters, serialized as a JSON string. |

### VodImageProcessTaskOutput

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Md5 |String |`e9461142c88731da6f40ab8e6bf4e882` |The MD5 hash of the image file. |
|Size |Long |`340698` |The image file size, in bytes. |
|Width |Long |`2027` |The image width, in pixels. |
|FileId |String |`d93c1337cced42139d05e3a572d0c34c` |The image file ID. |
|Format |String |`jpeg` |The image format, such as `jpeg`, `png`, or `webp`. |
|Height |Long |`1350` |The image height, in pixels. |
|Duration |Double |`0` |The duration of the animated image, in seconds. For a static image, the value is 0. |
|FrameCnt |Long |`1` |The number of frames. For a static image, the value is 1. |
|StoreUri |String |`tos-vod-bp-mya-v-b4aefc584297584a/<output-file-name>` |The storage URI of the image file. |
|CreateTime |Long |`1792061082` |The creation time, as a Unix timestamp in seconds. |
|UpdateTime |Long |`1792064087` |The last update time, as a Unix timestamp in seconds. |
|StorageClass |String |`STANDARD` |The storage class of the image file, such as `STANDARD`. |

## Samples

### Sample request

```http
POST /?Action=GetImageProcessTasks&Version=2023-07-01 HTTP/1.1
Host: vod.byteplusapi.com
Content-Type: application/json
```

```json
{
    "SpaceName": "meter-space",
    "Pid": "i186a8gm0018dbhefdqtgd69okvmf9pg",
    "TaskId": "d44f72f76b3372a3bf5d6206801f9bfc",
    "Offset": 0,
    "Limit": 20
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20261029**********************",
        "Action": "GetImageProcessTasks",
        "Version": "2023-07-01",
        "Service": "vod",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "TotalCount": 1,
        "TaskSet": [
            {
                "Pid": "i186a8gm0018dbhefdqtgd69okvmf9pg",
                "Status": "pending",
                "TaskId": "d44f72f76b3372a3bf5d6206801f9bfc",
                "ProcessType": "AISuperResolution",
                "ProcessParameter": "{\"GenDREnhanceParam\":{\"Multiple\":2.7},\"Input\":{}}"
            }
        ]
    }
}
```

## Error codes

For common error codes, see [Common error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
