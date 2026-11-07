---
title: "GetImageList"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-getimagelist"
---

Lists image assets in a space. You can filter the results by image ID, title, tags, category, creation time, or storage class.

## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=GetImageList&Version=2023\-07\-01

HTTP method: GET or POST

## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetImageList` |The API action. For this operation, set the value to `GetImageList`. |
|Version |String |Yes |`2023-07-01` |The API version. For this operation, set the value to `2023-07-01`. |
|SpaceName |String |Yes |`test-ll-vod-space` |The space name. You can call [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) to obtain the space names under your account. |
|Pid |String |No |`i18f06gm0018db8at0itgd6bem70tiug` |The image asset ID (Pid). Matches the ID exactly. |
|Title |String |No |`ceshi.jpeg` |The image title to search for. Fuzzy matching is supported. |
|Order |String |No |`desc` |The sort order by creation time. Valid values: `asc` and `desc`. |
|Tags |String |No |`ceshitdff` |The image tags. Separate multiple tags with commas. |
|StartTime |String |No |`1792022400` |The lower bound of the image creation time, as a Unix timestamp in seconds. |
|EndTime |String |No |`1792108800` |The upper bound of the image creation time, as a Unix timestamp in seconds. |
|Offset |String |No |`0` |The data offset. Default: 0. |
|PageSize |String |No |`20` |The page size. Default: 20. Valid range: 1 to 100. |
|ClassificationIds |String |No |`1791373087` |The category IDs. Separate multiple IDs with commas. |
|StorageClasses |String |No |`STANDARD` |The storage classes. Separate multiple values with commas. |
|Category |String |No |`image` |The image type: `image` for a static image (one frame and a duration of 0), or `dynamic_img` for an animated image. |

## Response parameters

For API\-specific response parameters, see the following tables. For common response parameters, see [Response](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#response).

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Offset |Integer |`0` |The data offset. Default: 0. |
|PageSize |Integer |`20` |The page size. |
|SpaceName |String |`test-ll-vod-space` |The space name. You can call [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) to obtain the space names under your account. |
|TotalCount |Integer |`1` |The total number of results that match the filters. |
|ImageInfoList |Array of [VodImageListItem](https://docs.byteplus.com/en/docs/25/124093#vodimagelistitem) |`-` |The list of image assets. |

### VodImageListItem

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Md5 |String |`b978a54d0d8a77eccea498e21d28536c` |The MD5 hash of the image file. |
|Pid |String |`i18f06gm0018db8at0itgd6bem70tiug` |The image asset ID (Pid). |
|Size |String |`1182053` |The image file size, in bytes. |
|Tags |Array of String |`["ceshitdff"]` |The image tag list. |
|Title |String |`ceshi.jpeg` |The image title. |
|Width |String |`500` |The image width, in pixels. |
|Format |String |`gif` |The image format, such as `jpeg`, `png`, or `webp`. |
|Height |String |`282` |The image height, in pixels. |
|Category |String |`dynamic_img` |The image type: `image` for a static image (one frame and a duration of 0), or `dynamic_img` for an animated image. |
|Duration |Double |`3.23` |The duration of the animated image, in seconds. For a static image, the value is 0. |
|FrameCnt |String |`17` |The number of frames. For a static image, the value is 1. |
|StoreUri |String |`tos-vod-bp-mya-v-3b9c21e794ac0879/ceshi_dir/54adadc1d51e159e92618bf0ce5a96e1.gif` |The storage URI of the image file. |
|SpaceName |String |`test-ll-vod-space` |The space name. You can call [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) to obtain the space names under your account. |
|CreateTime |String |`1792061082` |The creation time, as a Unix timestamp in seconds. |
|UpdateTime |String |`1792064087` |The last update time, as a Unix timestamp in seconds. |
|Description |String |`Image description` |The image description. |
|StorageClass |String |`STANDARD` |The storage class of the image file, such as `STANDARD`. |
|Classification |Object of [VodClassification](https://docs.byteplus.com/en/docs/25/124093#vodclassification) |`-` |The image category information. |

### VodClassification

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SpaceName |String |`test` |The name of the VOD space. |
|ClassificationId |Long |`1643` |The category ID. |
|Level |Integer |`1` |Category Levels:<br><br>1: The first category<br><br>2: The secondary category<br><br>3: The third category |
|Classification |String |`01` |The category name. |
|ParentClassificationId |Long |`1345` |The parent category ID. |
|SubClassification |Object of [VodClassification](https://docs.byteplus.com/en/docs/25/124093#vodclassification) |`-` |The sub\-category information. |
|SubClassificationTrees |Array of [VodClassification](https://docs.byteplus.com/en/docs/25/124093#vodclassification) |`-` |The subcategory list. |
|CreatedAt |String |`2025-07-07T06:44:59Z` |The category creation time. |

## Samples

### Sample request

```http
POST /?Action=GetImageList&Version=2023-07-01 HTTP/1.1
Host: vod.byteplusapi.com
Content-Type: application/json
```

```json
{
    "SpaceName": "test-ll-vod-space",
    "Pid": "i18f06gm0018db8at0itgd6bem70tiug",
    "Offset": "0",
    "PageSize": "20"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20261029**********************",
        "Action": "GetImageList",
        "Version": "2023-07-01",
        "Service": "vod",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Offset": 0,
        "PageSize": 20,
        "SpaceName": "test-ll-vod-space",
        "TotalCount": 1,
        "ImageInfoList": [
            {
                "StoreUri": "tos-vod-bp-mya-v-3b9c21e794ac0879/ceshi_dir/54adadc1d51e159e92618bf0ce5a96e1.gif",
                "Format": "gif",
                "Size": "1182053",
                "Width": "500",
                "Height": "282",
                "Md5": "b978a54d0d8a77eccea498e21d28536c",
                "StorageClass": "STANDARD",
                "FrameCnt": "17",
                "Duration": 3.23,
                "CreateTime": "1792061082",
                "UpdateTime": "1792064087",
                "Pid": "i18f06gm0018db8at0itgd6bem70tiug",
                "SpaceName": "test-ll-vod-space",
                "Title": "ceshi.jpeg",
                "Description": "修改12",
                "Tags": [
                    "ceshitdff"
                ],
                "Category": "dynamic_img",
                "Classification": null
            }
        ]
    }
}
```

## Error codes

For common error codes, see [Common error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
