---
title: "ListSnapshots"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-listsnapshots"
---

This interface is used to obtain the screenshot results of a video.

## Usage scenario

The response result of this interface contains the screenshot download address. In addition, you can also obtain the image address by splicing it yourself. The splicing instructions for the image address are as follows:

* Rule: http(s)://{domain}/{store_uri}~tplv\-vod\-noop.image

* Description: http(s)://VOD cover acceleration domain name/screenshot storage address~template.image format. For details on the configuration, please refer to [Real-time image processing](https://docs.byteplus.com/docs/byteplus-vod/docs-realtime-image-processing).

* Example: http://www.example.com/tos\-cn\-v\-abcd/example~tplv\-vod\-noop.image

## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=ListSnapshots&Version=2023\-01\-01

## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListSnapshots` |The API action. For the current API, the value is `ListSnapshots`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|Vid |String |Yes |`v0dc24g10***s1v0ipljnh4h0` |The video ID. After audio and video are uploaded, it can be obtained as follows:<br><br><br>* Query through the [GetMediaList](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getmedialist) interface.<br><br>* If upload callbacks are enabled, the value of `Vid` will be returned in [FileUploadComplete](https://docs.byteplus.com/en/docs/byteplus-vod/docs-fileuploadcomplete). |

## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SpaceName |String |`test` |The VOD space name. |
|Vid |String |`v0dc24g10001cm***pljnh4h0` |The video ID. |
|PosterSnapshots |Array of [VodSnapshot](https://docs.byteplus.com/en/docs/25/8030#vodsnapshot) |`-` |The static image. |
|DynpostSnapshots |Array of [VodSnapshot](https://docs.byteplus.com/en/docs/25/8030#vodsnapshot) |`-` |Animation |
|AnimatedPosterSnapshots |Array of [VodSnapshot](https://docs.byteplus.com/en/docs/25/8030#vodsnapshot) |`-` |Repeated loop animation. |
|AiDynpostSnapshots |Array of [VodSnapshot](https://docs.byteplus.com/en/docs/25/8030#vodsnapshot) |`-` |AI animation |
|SpriteSnapshots |Array of [VodSpriteSnapshot](https://docs.byteplus.com/en/docs/25/8030#vodspritesnapshot) |`-` |Sprites |
|VSamplePosterSnapshots |Array of [VodSamplePosterSnapshot](https://docs.byteplus.com/en/docs/25/8030#vodsamplepostersnapshot) |`-` |The sampling screenshot. |

### VodSnapshot

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Format |String |`jpeg` |The file format. |
|Height |Integer |`360` |The height. |
|Width |Integer |`958` |The width. |
|StoreUri |String |`tos-vod-cn-v-03e4***3112705/12d74b97e37944***e524a7398c6` |The image URI. |
|Url |String |`https://example.test.com/tos-vod-cn-v-03e4d54***112705/12d74b97e3794***83e524a7398c6~noop.image` |The image address. |

### VodSpriteSnapshot

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Format |String |`jpeg` |The sprite image format. Returns `jpeg` for JPEG sprites or `webp` for WebP sprites. |
|ImgXLen |Integer |`5` |The number of small images in the horizontal direction. |
|ImgYLen |Integer |`5` |The number of small images in the vertical direction. |
|CellWidth |Integer |`240` |The small image width. |
|CellHeight |Integer |`90` |The small image height. |
|Interval |Float |`2` |The screenshot interval. |
|CaptureNum |Integer |`6` |The total number of screenshots limit. |
|StoreUris |Array of String |`["tos-vod-cn-v-03e4d54***12705/33b783a01d7a4***4a04f1f28b3436"]` |The list of image URIs. |
|Urls |Array of String |`["https://example.test.com/tos-vod-cn-v-03e4d***2705/33b783a01d7a4***04f1f28b3436~noop.image"]` |The list of image URLs. |

### VodSamplePosterSnapshot

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|StoreUris |Array of String |`["tos-vod-cn-v-03e4d54***12705/737f0b92faf84***fecb9493290","tos-vod-cn-v-03e4d5***12705/403810e1f986***61314bbf5b330","tos-vod-cn-v-03e4d***12705/e7fc3fdde31***7a279f20e908"]` |The addresses of multiple sampling screenshots. |
|ImgNum |Integer |`6` |The number of sampling screenshots. |
|CellWidth |Integer |`1436` |The sampling screenshot width. |
|CellHeight |Integer |`540` |The sampling screenshot is high. |
|Interval |Float |`2` |The screenshot interval. |
|Format |String |`jpeg` |The format. Currently, the default is `jpg`. |
|Duration |Float |`11.4` |The video duration. |
|Urls |Array of String |`["https://example.test.com/tos-vod-cn-v-03e4d54***2705/737f0b92faf***7231fecb9493290~noop.image","https://example.test.com/tos-vod-cn-v-03e4d54***2705/403810e1f9***561314bbf5b330~noop.image","https://example.test.com/tos-vod-cn-v-03e4d54***2705/e7fc3fdd***eaa7a279f20e908~noop.image"]` |The list of image URLs. |
|LargeSnapshotUri |String |`tos-vod-cn-v-03e4d54***2705/737f0b92faf***7231fecb9493290~noop.image` |The bulk screenshot result file URI. |
|LargeSnapshotDownloadUrl |String |`https://example.test.com/tos-vod-cn-v-03e4d54***2705/737f0b92faf***7231fecb9493290~noop.image` |The download address for a large number of screenshot result files. |
|LargeSnapshotFillType |String |`noop.image` |The template for processing a large number of screenshot results. |

## Samples

### Sample request

```text
https://vod.byteplusapi.com?Action=ListSnapshots&Version=2023-01-01&Vid=v0dc24g10***s1v0ipljnh4h0
```

### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "ListSnapshots",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Vid": "v0dc24g10001cm***pljnh4h0",
        "SpaceName": "test",
        "PosterSnapshots": [
            {
                "Url": "https://example.test.com/tos-vod-cn-v-03e4d54***112705/12d74b97e3794***83e524a7398c6~noop.image",
                "Width": 958,
                "Format": "jpeg",
                "Height": 360,
                "StoreUri": "tos-vod-cn-v-03e4***3112705/12d74b97e37944***e524a7398c6"
            }
        ],
        "SpriteSnapshots": [
            {
                "Urls": [
                    ""
                ],
                "Format": "jpeg",
                "ImgXLen": 5,
                "ImgYLen": 5,
                "Interval": 2,
                "CellWidth": 240,
                "StoreUris": [
                    ""
                ],
                "CaptureNum": 6,
                "CellHeight": 90
            }
        ],
        "DynpostSnapshots": [
            {
                "Url": "https://example.test.com/tos-vod-cn-v-03e4d54***112705/12d74b97e3794***83e524a7398c6~noop.image",
                "Width": 958,
                "Format": "jpeg",
                "Height": 360,
                "StoreUri": "tos-vod-cn-v-03e4***3112705/12d74b97e37944***e524a7398c6"
            }
        ],
        "AiDynpostSnapshots": [
            {
                "Url": "https://example.test.com/tos-vod-cn-v-03e4d54***112705/12d74b97e3794***83e524a7398c6~noop.image",
                "Width": 958,
                "Format": "jpeg",
                "Height": 360,
                "StoreUri": "tos-vod-cn-v-03e4***3112705/12d74b97e37944***e524a7398c6"
            }
        ],
        "VSamplePosterSnapshots": [
            {
                "Urls": [
                    ""
                ],
                "Format": "jpeg",
                "ImgNum": 6,
                "Duration": 11.4,
                "Interval": 2,
                "CellWidth": 1436,
                "StoreUris": [
                    ""
                ],
                "CellHeight": 540,
                "LargeSnapshotUri": "tos-vod-cn-v-03e4d54***2705/737f0b92faf***7231fecb9493290~noop.image",
                "LargeSnapshotFillType": "noop.image",
                "LargeSnapshotDownloadUrl": "https://example.test.com/tos-vod-cn-v-03e4d54***2705/737f0b92faf***7231fecb9493290~noop.image"
            }
        ],
        "AnimatedPosterSnapshots": [
            {
                "Url": "https://example.test.com/tos-vod-cn-v-03e4d54***112705/12d74b97e3794***83e524a7398c6~noop.image",
                "Width": 958,
                "Format": "jpeg",
                "Height": 360,
                "StoreUri": "tos-vod-cn-v-03e4***3112705/12d74b97e37944***e524a7398c6"
            }
        ]
    }
}
```

## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).
