---
title: "GetWorkflowExecutionResult"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/getworkflowexecutionresult"
---

Call `GetWorkflowExecutionResult` with the workflow task ID to obtain the execution result of the workflow task.

<span id="requirements"></span>
## Requirements


* The currently supported time range for querying the task is **30 days**.


<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=GetWorkflowExecutionResult&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetWorkflowExecutionResult` |The API action. For the current API, the value is `GetWorkflowExecutionResult`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|RunId |String |Yes |`dfsd7469***349df` |The unique identifier for the current workflow execution task. This ID can be retrieved from the response of the [StartWorkflow](https://docs.byteplus.com/en/docs/byteplus-vod/reference-startworkflow) interface. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|RunId |String |`b926faef0e1***bd0801831c7c5` |The workflow task ID. |
|DirectUrl |Object of [DirectUrl](https://docs.byteplus.com/en/docs/25/63723#directurl) |`-` |The file storage path in the DirectUrl mode. |
|Vid |String |`v0c51bg7007***4jc77u6on28tm5g` |The video ID. This field is mutually exclusive with `DirectUrl`, meaning only one of them will be present in the response. |
|TemplateId |String |`5372bbb2759***ad93274ed119` |The workflow ID. |
|SpaceName |String |`test` |The VOD space name. |
|CallbackArgs |String |`YourCallbackArgs` |The callback parameter. |
|Status |String |`0` |The execution status.<br><br><br>* After the workflow task is completed, the values are as follows:<br><br>   * `0`: Successful.<br><br>   * `[1000,1999]`: Failure due to user error.<br><br>   * `[2000,2999]`: Failure due to system error.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more details, see <a href="https://docs.byteplus.com/en/docs/byteplus-vod/workflow-status-codes">Workflow status codes</a>.   </div><br>   <br><br>* During the execution of the workflow task, the values are as follows:<br><br>   * `PendingStart`: Queuing.<br><br>   * `Running`: In progress.<br><br>* When the user terminates the task, and the workflow execution ends, the values are as follows:<br><br>   * `Terminated`: Terminated. |
|TranscodeInfos |Array of [VodTranscodeInfo](https://docs.byteplus.com/en/docs/25/63723#vodtranscodeinfo) |`-` |The transcoding output information. Returned only when the workflow includes video transcoding, audio transcoding, or low\-bitrate HD transcoding. Contains details such as file format, size, duration, and stream metadata. |
|Snapshots |Array of [SnapshotResult](https://docs.byteplus.com/en/docs/25/63723#snapshotresult) |`-` |Snapshot results returned when the workflow contains a snapshot task. |


#{.custom\-md\-table\-4}#

<span id="directurl"></span>
### DirectUrl


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SpaceName |String |`test` |The VOD space name. |
|FileName |String |`example.mp4` |The file path. |
|BucketName |String |`tos-cn-v-cd3a11` |The name of the storage bucket bound to the space. |


#{.custom\-md\-table\-4}#

<span id="vodtranscodeinfo"></span>
### VodTranscodeInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|FileId |String |`v020c9g10001***hs1v0go2sgujq0` |The file ID. |
|Md5 |String |`dd9fd3ad7f99f***ce70609aec68589` |The file MD5 value. |
|FileType |String |`video` |The type of the file. The possible values are as follows:<br><br><br>* `video`: the video file;<br><br>* `audio`: the audio file. |
|LogoType |String |`aa` |The watermark label. You can set the watermark label when creating a [watermark template](https://docs.byteplus.com/en/docs/byteplus-vod/docs-watermark-and-ad-insertion-template) in the BytePlus VOD console. |
|Encrypt |Boolean |`false` |Indicates whether the transcoded file is encrypted. The possible values are as follows:<br><br><br>* `false`: not encrypted;<br><br>* `true`: encrypted. |
|Format |String |`mp3` |Encoding format. The values are as follows:<br><br><br>* Video transcoding: `MP4`, `DASH`, `HLS`, `FLV`, `TS`<br><br>* Audio transcoding: `MP3`, `M4A`, `MP4`, `DASH`, `HLS`, `OGG` |
|Duration |Float |`2.944` |The duration, in seconds. |
|Size |Double |`104847` |The file size, in bytes. |
|StoreUri |String |`tos-cn-v/34fdg***58sd.mp4` |The object storage address. |
|VideoStreamMeta |Object of [VodVideoStreamMeta](https://docs.byteplus.com/en/docs/25/63723#vodvideostreammeta) |`-` |The video stream metadata. |
|AudioStreamMeta |Object of [VodAudioStreamMeta](https://docs.byteplus.com/en/docs/25/63723#vodaudiostreammeta) |`-` |The audio stream metadata. |
|CreateTime |String |`2021-04-02T02:47:33Z` |The creation time of the transcoded file, formatted in UTC following the RFC3339 standard with second\-level precision (yyyy\-MM\-ddTHH:mm:ssZ). |
|DynamicRange |String |`HDR` |The dynamic range of the transcoded video. The possible values are as follows:<br><br><br>* `HDR`: High Dynamic Range;<br><br>* `SDR`: Standard Dynamic Range. |
|TosStorageClass |String |`STANDARD` |The video storage type. The possible values are as follows:<br><br><br>* `STANDARD`: The standard storage.<br><br>* `ARCHIVE`: The archive storage. |


#{.custom\-md\-table\-4}#

<span id="vodvideostreammeta"></span>
### VodVideoStreamMeta


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Codec |String |`h264` |The video encoding format. |
|Height |Integer |`270` |The video height, in px. |
|Width |Integer |`480` |The video width, in px. |
|Duration |Float |`2.944` |The video duration, in seconds. |
|Definition |String |`720p` |The video clarity. |
|Bitrate |Integer |`284910` |The video bitrate, in bps. |
|Fps |Float |`25` |The video frame rate, measured in fps. |


#{.custom\-md\-table\-4}#

<span id="vodaudiostreammeta"></span>
### VodAudioStreamMeta


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Codec |String |`aac` |The audio encoding format. |
|Duration |Float |`2.943` |The audio duration, measured in seconds. |
|SampleRate |Integer |`44100` |The audio sampling rate, in Hz. |
|Bitrate |Integer |`127658` |The audio bitrate, with the unit of bps. |
|Quality |String |`higher` |The audio quality. This parameter is returned only after audio transcoding. The possible values are as follows:<br><br><br>* `medium`: the standard audio quality<br><br>* `higher`: the high audio quality<br><br>* `highest`: the music audio quality |


#{.custom\-md\-table\-4}#

<span id="snapshotresult"></span>
### SnapshotResult


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Type |String |`Sample` |Snapshot types. The values are as follows:<br><br><br>* `Poster`: the static snapshot<br><br>* `Dynpost`: the dynamic snapshot<br><br>* `AnimatedPoster`: the looped animated image<br><br>* `AIDynpost`: the AI animated image<br><br>* `Sprite`: the sprite snapshot<br><br>* `Sample`: the sampled snapshot |
|Poster |Object of [SnapshotParamsPoster](https://docs.byteplus.com/en/docs/25/63723#snapshotparamsposter) |`-` |The static graph information. |
|Dynpost |Object of [SnapshotParamsDynpost](https://docs.byteplus.com/en/docs/25/63723#snapshotparamsdynpost) |`-` |The animated image information. |
|AnimatedPoster |Object of [SnapshotParamsAnimatedPoster](https://docs.byteplus.com/en/docs/25/63723#snapshotparamsanimatedposter) |`-` |The animated GIF information of repetitive loops. |
|AIDynpost |Object of [SnapshotParamsAIDynpost](https://docs.byteplus.com/en/docs/25/63723#snapshotparamsaidynpost) |`-` |The AI animated image information. |
|Sprite |Object of [SnapshotParamsSprite](https://docs.byteplus.com/en/docs/25/63723#snapshotparamssprite) |`-` |The sprite image information. |
|Sample |Object of [SnapshotParamsSample](https://docs.byteplus.com/en/docs/25/63723#snapshotparamssample) |`-` |The sampled snapshot information. |


#{.custom\-md\-table\-4}#

<span id="snapshotparamsposter"></span>
### SnapshotParamsPoster


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Format |String |`jpeg` |The snapshot format. |
|StoreUri |String |`tos***/cbe797357ecf439***c4a26b69dd5` |The storage address. |
|Width |Integer |`360` |The snapshot width, in px. |
|Height |Integer |`640` |The snapshot height, in px. |


#{.custom\-md\-table\-4}#

<span id="snapshotparamsdynpost"></span>
### SnapshotParamsDynpost


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Format |String |`gif` |The snapshot format. The possible values are as follows:<br><br><br>* `jpeg`<br><br>* `jpg`<br><br>* `png` |
|StoreUri |String |`tos***/c5d95e55fdbb***62c8c5f7e4a6aa` |The storage address. |
|Width |Integer |`360` |The snapshot width, in px. |
|Height |Integer |`640` |The snapshot height, in px. |


#{.custom\-md\-table\-4}#

<span id="snapshotparamsanimatedposter"></span>
### SnapshotParamsAnimatedPoster


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Format |String |`webp` |The snapshot format. |
|StoreUri |String |`tos***/89523e5554a74***9c6898761055a8` |The storage address. |
|Width |Integer |`540` |The snapshot width, in px. |
|Height |Integer |`960` |The snapshot height, in px. |


#{.custom\-md\-table\-4}#

<span id="snapshotparamsaidynpost"></span>
### SnapshotParamsAIDynpost


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Format |String |`webp` |The snapshot format. |
|StoreUri |String |`tos***/89523e5554a74***9c6898761055a8` |The storage address. |
|Width |Integer |`540` |The snapshot width, in px. |
|Height |Integer |`960` |The snapshot height, in px. |


#{.custom\-md\-table\-4}#

<span id="snapshotparamssprite"></span>
### SnapshotParamsSprite


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Format |String |`jpeg` |The snapshot format. |
|StoreUris |Array of String |`tos***/14437a144eb14***38b8b731f8a96` |The storage address. |
|CellWidth |Integer |`240` |The width of the thumbnail, in px. |
|CellHeight |Integer |`360` |The height of the thumbnail, in px. |
|ImgXLen |Integer |`5` |The number of small images in the horizontal direction. |
|ImgYLen |Integer |`5` |The number of small images in the vertical direction. |
|Interval |Float |`10` |The snapshot interval, in seconds. |
|CaptureNum |Integer |`1` |The number of snapshots. |


#{.custom\-md\-table\-4}#

<span id="snapshotparamssample"></span>
### SnapshotParamsSample


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Format |String |`jpeg` |The snapshot format. |
|Width |Integer |`540` |The snapshot width, in px. |
|Height |Integer |`960` |The snapshot height, in px. |
|Interval |Float |`10` |The snapshot interval, in seconds. |
|CaptureNum |Integer |`1` |The number of snapshots. |
|Duration |Float |`14` |The source video duration, in seconds. |
|Offsets |Array of Float |`5` |Custom sampling time points for snapshot capture.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is returned only when you specify the sampling time points for snapshot capture by setting the <code>Snapshot.SampleOffsets</code> parameter while calling the StartWorkflow API.</div><br> |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=GetWorkflowExecutionResult&Version=2023-01-01&RunId=dfsd7469***349df
```


<span id="Sample response"></span>
### Sample response

```json
{
    "Result": {
        "Vid": "v0c51bg7007***4jc77u6on28tm5g",
        "RunId": "b926faef0e1***bd0801831c7c5",
        "Status": "0",
        "DirectUrl": {
            "FileName": "example.mp4",
            "SpaceName": "test",
            "BucketName": "tos-cn-v-cd3a11"
        },
        "Snapshots": [
            {
                "Type": "Sample",
                "Poster": {
                    "Width": 360,
                    "Format": "jpeg",
                    "Height": 640,
                    "StoreUri": "tos***/cbe797357ecf439***c4a26b69dd5"
                },
                "Sample": {
                    "Width": 540,
                    "Format": "jpeg",
                    "Height": 960,
                    "Offsets": [
                        null
                    ],
                    "Duration": 14,
                    "Interval": 10,
                    "CaptureNum": 1
                },
                "Sprite": {
                    "Format": "jpeg",
                    "ImgXLen": 5,
                    "ImgYLen": 5,
                    "Interval": 10,
                    "CellWidth": 240,
                    "StoreUris": [
                        ""
                    ],
                    "CaptureNum": 1,
                    "CellHeight": 360
                },
                "Dynpost": {
                    "Width": 360,
                    "Format": "gif",
                    "Height": 640,
                    "StoreUri": "tos***/c5d95e55fdbb***62c8c5f7e4a6aa"
                },
                "AIDynpost": {
                    "Width": 540,
                    "Format": "webp",
                    "Height": 960,
                    "StoreUri": "tos***/89523e5554a74***9c6898761055a8"
                },
                "AnimatedPoster": {
                    "Width": 540,
                    "Format": "webp",
                    "Height": 960,
                    "StoreUri": "tos***/89523e5554a74***9c6898761055a8"
                }
            }
        ],
        "SpaceName": "test",
        "TemplateId": "5372bbb2759***ad93274ed119",
        "ClientToken": "",
        "CallbackArgs": "YourCallbackArgs",
        "TranscodeInfos": [
            {
                "Md5": "dd9fd3ad7f99f***ce70609aec68589",
                "Size": 104847,
                "FileId": "v020c9g10001***hs1v0go2sgujq0",
                "Format": "mp3",
                "Encrypt": true,
                "Duration": 2.944,
                "FileType": "video",
                "LogoType": "aa",
                "StoreUri": "tos-cn-v/34fdg***58sd.mp4",
                "CreateTime": "2021-04-02T02:47:33Z",
                "DynamicRange": "HDR",
                "AudioStreamMeta": {
                    "Codec": "aac",
                    "Bitrate": 127658,
                    "Quality": "higher",
                    "Channels": 2,
                    "Duration": 2.943,
                    "SampleRate": 44100
                },
                "TosStorageClass": "STANDARD",
                "VideoStreamMeta": {
                    "Fps": 25,
                    "Codec": "h264",
                    "Width": 480,
                    "Height": 270,
                    "Bitrate": 284910,
                    "Duration": 2.944,
                    "Definition": "720p"
                }
            }
        ]
    },
    "ResponseMetadata": {
        "Action": "GetWorkflowExecutionResult",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
