---
title: "UpdateImageInfos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-updateimageinfos"
---

Updates the title, description, tags, or category of an image asset.

## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=UpdateImageInfos&Version=2023\-07\-01

HTTP method: GET or POST

## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateImageInfos` |The API action. For this operation, set the value to `UpdateImageInfos`. |
|Version |String |Yes |`2023-07-01` |The API version. For this operation, set the value to `2023-07-01`. |
|Pid |String |Yes |`i18f06gm0018db8at0itgd6bem70tiug` |The image asset ID (Pid). |
|Tags |String |No |`ceshitdff` |The image tags. Separate multiple tags with commas. |
|ClassificationId |Long |No |`1791373087` |The image category ID. |
|Description |String |No |`修改12` |The image description. |
|SpaceName |String |No |`test-ll-vod-space` |The space name. You can call [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) to obtain the space names under your account. |
|Title |String |No |`ceshi.jpeg` |The image title. |

## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#response) in the response.

## Samples

### Sample request

```http
POST /?Action=UpdateImageInfos&Version=2023-07-01 HTTP/1.1
Host: vod.byteplusapi.com
Content-Type: application/json
```

```json
{
    "Pid": "i18f06gm0018db8at0itgd6bem70tiug",
    "SpaceName": "test-ll-vod-space",
    "Title": "ceshi.jpeg",
    "Tags": "ceshitdff",
    "Description": "修改12",
    "ClassificationId": 1791373087
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20261029**********************",
        "Action": "UpdateImageInfos",
        "Version": "2023-07-01",
        "Service": "vod",
        "Region": "ap-southeast-1"
    }
}
```

## Error codes

For common error codes, see [Common error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
