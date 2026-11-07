---
title: "ImageProcess"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-imageprocess"
---

Submits a basic image processing task to resize, center\-crop, or center\-pad an image. You can also specify the output format.

The response indicates that the task was submitted. To obtain the final result, call [GetImageProcessTasks](https://docs.byteplus.com/docs/byteplus-vod/reference-getimageprocesstasks) or subscribe to [ImageProcessComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-imageprocesscomplete).

## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=ImageProcess&Version=2023\-07\-01

HTTP method: POST

## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

### Query parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ImageProcess` |The API action. For this operation, set the value to `ImageProcess`. |
|Version |String |Yes |`2023-07-01` |The API version. For this operation, set the value to `2023-07-01`. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Pid |String |Yes |`i189ddgm0018db8ono2tgd6bem70tj1g` |The image asset ID (Pid). |
|ProcessType |String |Yes |`pad` |The processing operation: `rs` for proportional resizing, `cc` for center cropping, or `pad` for center padding. |
|Width |String |No |`432` |The output image width, in pixels. If specified, the value must be a positive integer. Required for `cc` and `pad`. |
|Height |String |No |`345` |The output image height, in pixels. If specified, the value must be a positive integer. Required for `cc` and `pad`. |
|Color |String |No |`543333` |The fill color for `pad`, specified as a six\-digit hexadecimal RGB value, such as `FFFFFF`. Required for `pad`. |
|SpaceName |String |No |`test-ll-space-0522` |The space name. You can call [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) to obtain the space names under your account. |
|CallbackArgs |String |No |`""` |The custom information passed through to the completion callback. |
|OutputFormat |String |No |`avif` |The output format. Valid values: `jpeg`, `jpg`, `png`, `webp`, `awebp`, `gif`, `image`, `avif`, and `avis`. An empty value is equivalent to `image`, which retains the input format. `gif` requires an animated input image. |

> **Resize parameters**

> For proportional resizing with `ProcessType=rs`, specify one of `Width` or `Height`. For example, set `Width` to `"320"` and omit `Height` to resize by width while preserving the aspect ratio. For `cc` and `pad`, both dimensions are required.

## Response parameters

For API\-specific response parameters, see the following tables. For common response parameters, see [Response](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#response).

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Pid |String |`i189ddgm0018db8ono2tgd6bem70tj1g` |The image asset ID (Pid). |
|Status |String |`pending` |The submission status. A successfully submitted task returns `pending`. |
|TaskId |String |`59f579e83b2cd66a6e5a32e35618088d` |The image processing task ID. |
|ProcessType |String |`Basic` |The normalized processing type: `Basic` or `AISuperResolution`. |

## Samples

### Sample request

```http
POST /?Action=ImageProcess&Version=2023-07-01 HTTP/1.1
Host: vod.byteplusapi.com
Content-Type: application/json
```

```json
{
    "Pid": "i189ddgm0018db8ono2tgd6bem70tj1g",
    "ProcessType": "pad",
    "Width": "432",
    "Height": "345",
    "Color": "543333",
    "SpaceName": "test-ll-space-0522",
    "OutputFormat": "avif"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20261029**********************",
        "Action": "ImageProcess",
        "Version": "2023-07-01",
        "Service": "vod",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Pid": "i189ddgm0018db8ono2tgd6bem70tj1g",
        "ProcessType": "Basic",
        "TaskId": "59f579e83b2cd66a6e5a32e35618088d",
        "Status": "pending"
    }
}
```

## Error codes

For common error codes, see [Common error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
