---
title: "DeleteImages"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-deleteimages"
---

Deletes image assets, including their original files and all processed files. Deletion is asynchronous.

Use the returned `JobId` to associate the request with the [ImageDeleteComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-imagedeletecomplete) notification.

## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DeleteImages&Version=2023\-07\-01

HTTP method: GET or POST

## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DeleteImages` |The API action. For this operation, set the value to `DeleteImages`. |
|Version |String |Yes |`2023-07-01` |The API version. For this operation, set the value to `2023-07-01`. |
|Pids |String |Yes |`i256c3gm0018db8vc1itgd6bcq42r0e0` |The image asset IDs. Separate multiple IDs with commas. |
|CallbackArgs |String |No |`""` |The custom information passed through to the completion callback. |
|SpaceName |String |No |`mya-autotest-qa` |The space name. You can call [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) to obtain the space names under your account. |

## Response parameters

For API\-specific response parameters, see the following tables. For common response parameters, see [Response](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#response).

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|JobId |String |`a586ea18d0cd4f9ba41edb9a67e3fd92` |The asynchronous deletion task ID. |
|NotExistPids |Array of String |`[]` |The image asset IDs that do not exist. |

## Samples

### Sample request

```http
POST /?Action=DeleteImages&Version=2023-07-01 HTTP/1.1
Host: vod.byteplusapi.com
Content-Type: application/json
```

```json
{
    "Pids": "i256c3gm0018db8vc1itgd6bcq42r0e0",
    "SpaceName": "mya-autotest-qa"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20261029**********************",
        "Action": "DeleteImages",
        "Version": "2023-07-01",
        "Service": "vod",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "JobId": "a586ea18d0cd4f9ba41edb9a67e3fd92",
        "NotExistPids": []
    }
}
```

## Error codes

For common error codes, see [Common error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
