---
title: "GetImageInfos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-getimageinfos"
---

Gets the details of one or more image assets, including their original files and processed files.

## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=GetImageInfos&Version=2023\-07\-01

HTTP method: GET or POST

## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetImageInfos` |The API action. For this operation, set the value to `GetImageInfos`. |
|Version |String |Yes |`2023-07-01` |The API version. For this operation, set the value to `2023-07-01`. |
|Pids |String |Yes |`i18f06gm0018db8at0itgd6bem70tiug` |The image asset IDs. Separate multiple IDs with commas. |
|ForceExpire |String |No |`3600` |The validity period of the image URLs, in seconds. Valid range: 60 to 315360000. If omitted, the expiration setting of the domain is used. |
|PlayConfig |String |No |`{"PlayDomain":"image.example.com"}` |The playback configuration, specified as a JSON string. Set `PlayDomain` to the image playback domain to use. |
|Ssl |String |No |`1` |Whether to return HTTPS image URLs. Valid values: `1` for HTTPS and `0` for HTTP. Default: `0`. |
|SpaceName |String |No |`test-ll-vod-space` |The space name. You can call [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) to obtain the space names under your account. |

## Response parameters

For API\-specific response parameters, see the following tables. For common response parameters, see [Response](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#response).

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|NotExistPids |Array of String |`[]` |The image asset IDs that do not exist. |
|ImageInfoList |Array of [VodImageDetailInfo](https://docs.byteplus.com/en/docs/25/124094#vodimagedetailinfo) |`-` |The image details grouped by Pid. |

### VodImageDetailInfo

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Pid |String |`i18f06gm0018db8at0itgd6bem70tiug` |The image asset ID (Pid). |
|Tags |Array of String |`["ceshitdff"]` |The image tag list. |
|Title |String |`ceshi.jpeg` |The image title. |
|Category |String |`dynamic_img` |The image type: `image` for a static image (one frame and a duration of 0), or `dynamic_img` for an animated image. |
|SpaceName |String |`test-ll-vod-space` |The space name. You can call [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) to obtain the space names under your account. |
|CreateTime |String |`1792061082` |The creation time, as a Unix timestamp in seconds. |
|UpdateTime |String |`1792064087` |The last update time, as a Unix timestamp in seconds. |
|Description |String |`Image description` |The image description. |
|Classification |Object of [VodClassification](https://docs.byteplus.com/en/docs/25/124094#vodclassification) |`-` |The image category information. |
|OriginalImageInfo |Object of [VodImageFileInfo](https://docs.byteplus.com/en/docs/25/124094#vodimagefileinfo) |`-` |The original image file information. |
|ProcessedImageInfos |Array of [VodImageFileInfo](https://docs.byteplus.com/en/docs/25/124094#vodimagefileinfo) |`-` |The processed image files. |

### VodClassification

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SpaceName |String |`test` |The name of the VOD space. |
|ClassificationId |Long |`1643` |The category ID. |
|Level |Integer |`1` |Category Levels:<br><br>1: The first category<br><br>2: The secondary category<br><br>3: The third category |
|Classification |String |`01` |The category name. |
|ParentClassificationId |Long |`1345` |The parent category ID. |
|SubClassification |Object of [VodClassification](https://docs.byteplus.com/en/docs/25/124094#vodclassification) |`-` |The sub\-category information. |
|SubClassificationTrees |Array of [VodClassification](https://docs.byteplus.com/en/docs/25/124094#vodclassification) |`-` |The subcategory list. |
|CreatedAt |String |`2025-07-07T06:44:59Z` |The category creation time. |

### VodImageFileInfo

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Md5 |String |`b978a54d0d8a77eccea498e21d28536c` |The MD5 hash of the image file. |
|Size |String |`1182053` |The image file size, in bytes. |
|Width |String |`500` |The image width, in pixels. |
|FileId |String |`img_f9f4dd81a8fe951663d245f079afe8c9` |The image file ID. |
|Format |String |`gif` |The image format, such as `jpeg`, `png`, or `webp`. |
|Height |String |`282` |The image height, in pixels. |
|Duration |Double |`3.23` |The duration of the animated image, in seconds. For a static image, the value is 0. |
|FrameCnt |String |`17` |The number of frames. For a static image, the value is 1. |
|ImageUrl |String |`""` |The image URL. An empty string is returned if no available image playback domain is configured for the space. |
|StoreUri |String |`tos-vod-bp-mya-v-3b9c21e794ac0879/ceshi_dir/54adadc1d51e159e92618bf0ce5a96e1.gif` |The storage URI of the image file. |
|CreateTime |String |`1792061082` |The creation time, as a Unix timestamp in seconds. |
|UpdateTime |String |`1792064087` |The last update time, as a Unix timestamp in seconds. |
|StorageClass |String |`STANDARD` |The storage class of the image file, such as `STANDARD`. |

## Samples

### Sample request

```http
POST /?Action=GetImageInfos&Version=2023-07-01 HTTP/1.1
Host: vod.byteplusapi.com
Content-Type: application/json
```

```json
{
    "Pids": "i18f06gm0018db8at0itgd6bem70tiug",
    "SpaceName": "test-ll-vod-space"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20261029**********************",
        "Action": "GetImageInfos",
        "Version": "2023-07-01",
        "Service": "vod",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "NotExistPids": [],
        "ImageInfoList": [
            {
                "Pid": "i18f06gm0018db8at0itgd6bem70tiug",
                "SpaceName": "test-ll-vod-space",
                "Title": "ceshi.jpeg",
                "Description": "修改12",
                "Tags": [
                    "ceshitdff"
                ],
                "Category": "dynamic_img",
                "Classification": null,
                "CreateTime": "1792061082",
                "UpdateTime": "1792064087",
                "OriginalImageInfo": {
                    "FileId": "img_f9f4dd81a8fe951663d245f079afe8c9",
                    "StoreUri": "tos-vod-bp-mya-v-3b9c21e794ac0879/ceshi_dir/54adadc1d51e159e92618bf0ce5a96e1.gif",
                    "ImageUrl": "",
                    "Format": "gif",
                    "Size": "1182053",
                    "Width": "500",
                    "Height": "282",
                    "Md5": "b978a54d0d8a77eccea498e21d28536c",
                    "StorageClass": "STANDARD",
                    "FrameCnt": "17",
                    "Duration": 3.23,
                    "CreateTime": "1792061082",
                    "UpdateTime": "1792064087"
                },
                "ProcessedImageInfos": []
            }
        ]
    }
}
```

## Error codes

For common error codes, see [Common error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
