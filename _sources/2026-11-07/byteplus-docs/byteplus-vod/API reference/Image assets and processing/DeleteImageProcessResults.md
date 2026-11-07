---
title: "DeleteImageProcessResults"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-deleteimageprocessresults"
---

Deletes specified processed files of an image asset. The original image is retained. Deletion is asynchronous.

## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DeleteImageProcessResults&Version=2023\-07\-01

HTTP method: GET or POST

## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DeleteImageProcessResults` |The API action. For this operation, set the value to `DeleteImageProcessResults`. |
|Version |String |Yes |`2023-07-01` |The API version. For this operation, set the value to `2023-07-01`. |
|SpaceName |String |Yes |`mya-autotest-qa` |The space name. You can call [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) to obtain the space names under your account. |
|Pid |String |Yes |`i256c3gm0018db8vc1itgd6bcq42r0e0` |The image asset ID (Pid). |
|FileIds |String |Yes |`86977c91e3321a0dcad45756ab49d73d` |The IDs of the processed image files to delete. Obtain the file IDs from `ProcessedImageInfos` in [GetImageInfos](https://docs.byteplus.com/docs/byteplus-vod/reference-getimageinfos). |

## Response parameters

For API\-specific response parameters, see the following tables. For common response parameters, see [Response](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#response).

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|JobId |String |`example-deletion-job-id` |The asynchronous deletion task ID. |
|NotExistFileIds |Array of String |`[]` |The file IDs that do not exist. |

## Samples

### Sample request

```http
POST /?Action=DeleteImageProcessResults&Version=2023-07-01 HTTP/1.1
Host: vod.byteplusapi.com
Content-Type: application/json
```

```json
{
    "SpaceName": "mya-autotest-qa",
    "Pid": "i256c3gm0018db8vc1itgd6bcq42r0e0",
    "FileIds": "86977c91e3321a0dcad45756ab49d73d"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20261029**********************",
        "Action": "DeleteImageProcessResults",
        "Version": "2023-07-01",
        "Service": "vod",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "JobId": "example-deletion-job-id",
        "NotExistFileIds": []
    }
}
```

## Error codes

For common error codes, see [Common error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
