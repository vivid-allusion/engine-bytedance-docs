---
title: "ListFrameExtractions"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-listframeextractions"
---

Queries frame extraction results by video ID. Returns a list of frame extraction snapshots, with one entry per extraction strategy.

<span id="HTTP request"></span>
## HTTP request


* Method：GET

* Endpoint：https://vod.byteplusapi.com?Action=ListFrameExtractions&Version=2023\-01\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="Query"></span>
### Query


|**Parameter**  |**Data Type**  |**Required**  |**Sample Value**  |**Description**  |
|---|---|---|---|---|
|Action |String |Yes |`ListFrameExtractions` |The API action. For the current API, the value is `ListFrameExtractions`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |Yes |test |Space name. |
|Vid |String |Yes |v0dc24g10\*\*\*s1v0ipljnh4h0 |Video ID. |
|UserTag |String |No |tag1 |User\-defined tag. Only one tag can be specified. If not specified, results are not filtered by tag. |
|RunId |String |No |3732f0bd7565494d8faf7956d4f99f31 |Task ID, the unique identifier for the execution task (run ID). This ID can be retrieved from the response of the `StartExecution` API. At most one `RunId` can be specified. If not specified, results are not filtered by run ID. |


<span id="Response parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|Vid |String |v0dc24g10001cm\*\*\*pljnh4h0 |Video ID. |
|SpaceName |String |test |Space name. |
|FrameExtractionSnapshots |Array of [FrameExtractionSnapshot](https://docs.byteplus.com/en/docs/25/108396#frameextractionsnapshot) |\- |List of frame extraction snapshots. Each extraction strategy produces one entry. |


<span id="frameextractionsnapshot"></span>
### FrameExtractionSnapshot


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|RunId |String |3732f0bd7565494d8faf7956d4f99f31 |Task ID. |
|Width |Integer |1920 |Image width in pixels. |
|Format |String |jpeg |Image format. |
|Height |Integer |1080 |Image height in pixels. |
|UserTag |String |tag1 |User\-defined tag. |
|Duration |Double |600 |Total video duration in seconds. |
|UserData |String |test |Custom parameters passed in the frame extraction task. |
|Snapshots |Array of [FrameSnapshot](https://docs.byteplus.com/en/docs/25/108396#framesnapshot) |\- |List of extracted frames. |


<span id="framesnapshot"></span>
### FrameSnapshot


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|Url |String |https://console\-image\-my.byteplusvod.com/tos\-vod\-bp\-mya\-v\-xxx/01snapshot.jpg |URL of the frame image. |
|Size |Long |251906 |Size of the frame image in bytes. |
|FrameNo |Long |5 |Frame number, starting from 0. |
|StoreURI |String |tos\-vod\-bp\-mya\-v\-xxx/01snapshot.jpg |URI of the frame image. |
|StartTime |Long |5000 |Timestamp of the frame in milliseconds. |
|SceneChangeRate |Double |0.85 |Scene change score. |


<span id="Sample-request"></span>
### Sample request

```JSON
GET https://vod.byteplusapi.com?Action=ListFrameExtractions&Version=2023-01-01&SpaceName=test&Vid=v0dc24g10***s1v0ipljnh4h0&UserTag=tag1&RunId=3732f0bd7565494d8faf7956d4f99f31
```


<span id="Sample-request"></span>
### Sample request

```JSON
{
    "ResponseMetadata": {
        "Action": "ListFrameExtractions",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Vid": "v0dc24g10001cm***pljnh4h0",
        "SpaceName": "test",
        "FrameExtractionSnapshots": [
            {
                "RunId": "3732f0bd7565494d8faf7956d4f99f31",
                "Width": 1920,
                "Format": "jpeg",
                "Height": 1080,
                "UserTag": "tag1",
                "Duration": 600,
                "UserData": "test",
                "Snapshots": [
                    {
                        "Url": "https://console-image-my.byteplusvod.com/tos-vod-bp-mya-v-xxx/01snapshot.jpg",
                        "Size": 251906,
                        "FrameNo": 5,
                        "StoreURI": "tos-vod-bp-mya-v-xxx/01snapshot.jpg",
                        "StartTime": 5000,
                        "SceneChangeRate": 0.85
                    }
                ]
            }
        ]
    }
}
```


<span id="Error codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).
