---
title: "QueryUploadTaskInfo"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-queryuploadtaskinfo"
---

This interface is used to query the status of batch upload tasks. You can query using the `JobId` returned by the [UploadMediaByUrl](https://docs.byteplus.com/en/docs/byteplus-vod/reference-uploadmediabyurl) interface. If the upload is successful, the interface will return `Vid` along with the basic media information.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=QueryUploadTaskInfo&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`QueryUploadTaskInfo` |The API action. For the current API, the value is `QueryUploadTaskInfo`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|JobIds |String |Yes |`YourJobIds` |Job ID corresponding to the upload URL. you can query multiple IDs separated by commas, with a maximum of 20 entries. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Data |Object of [QueryUploadResult](https://docs.byteplus.com/en/docs/25/8019#queryuploadresult) |`-` |URL batch upload status query result. |


#{.custom\-md\-table\-4}#

<span id="queryuploadresult"></span>
### QueryUploadResult


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|MediaInfoList |Array of [URLSet](https://docs.byteplus.com/en/docs/25/8019#urlset) |`-` |Information corresponding to the exsiting `JobId`. |
|NotExistJobIds |Array of String |`-` |Return the list of `JobId` that were queried but do not exist. The `JobId` may be incorrect or expired. |


#{.custom\-md\-table\-4}#

<span id="urlset"></span>
### URLSet


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|RequestId |String |`RequestId` |The unique identifier for the request, used for log query. |
|JobId |String |`JobId` |The jobId used to query the upload status of a URL. |
|SourceUrl |String |`SourceUrl` |The upload URL. |
|State |String |`State` |The upload status. The possible values are:<br><br><br>* `initial`<br><br>* `processing`<br><br>* `success`<br><br>* `failed` |
|Vid |String |`Vid` |The video ID. |
|SpaceName |String |`SpaceName` |The VOD space name. |
|AccountId |String |`AccountId` |The user account ID. |
|SourceInfo |Object of [SourceInfo](https://docs.byteplus.com/en/docs/25/8019#sourceinfo) |`-` |The metadata of the video. |
|CallbackArgs |String |`xxxxxxxxxxxx` |Additional information that will be returned in the callback. |


#{.custom\-md\-table\-4}#

<span id="sourceinfo"></span>
### SourceInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|FileId |String |`v02b69g10***ldb8vjafvmg` |The file ID. |
|Md5 |String |`b9fd116504b***88e59a824878f07a` |The file MD5 value. |
|FileType |String |`video` |The file type. The values are as follows:<br><br><br>* `video`<br><br>* `audio` |
|Codec |String |`h264` |The codec. |
|Height |Integer |`270` |The video height, in pixels. |
|Width |Integer |`480` |The video width, in pixels. |
|Format |String |`MP4` |The file format. |
|Duration |Float |`2.944` |The video duration, measured in seconds. |
|Size |Double |`104847` |The file size, in bytes. |
|StoreUri |String |`tos-cn-v-febf3a/daeba******a18e61e1aebfaf39aa.mp4` |The object storage address. |
|Definition |String |`unknown` |The video resolution |
|Bitrate |Integer |`284910` |The bitrate, measured in bps. |
|Fps |Float |`25` |The frame rate, measured in fps. |
|CreateTime |String |`2022-12-28T08:57:58Z` |The creation time. |
|DynamicRange |String |`SDR` |Dynamic range. The values are as follows:<br><br><br>* `HDR`<br><br>* `SDR` |
|VideoStreamMeta |Object of [VideoStreamMeta](https://docs.byteplus.com/en/docs/25/8019#videostreammeta) |`-` |The video stream metadata. |
|AudioStreamMeta |Object of [AudioStreamMeta](https://docs.byteplus.com/en/docs/25/8019#audiostreammeta) |`-` |The audio stream metadata. |
|FileExtra |JSON Map |`-` |The additional attributes. |


#{.custom\-md\-table\-4}#

<span id="videostreammeta"></span>
### VideoStreamMeta


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Codec |String |`h264` |The video codec. |
|Height |Integer |`270` |The video height, in pixels. |
|Width |Integer |`480` |The video width, in pixels. |
|Duration |Float |`2.944` |The video duration, measured in seconds. |
|Definition |String |`720p` |The video clarity. |
|Bitrate |Integer |`284910` |The video bitrate, measured in bps. |
|Fps |Float |`25` |The video frame rate, measured in fps. |


#{.custom\-md\-table\-4}#

<span id="audiostreammeta"></span>
### AudioStreamMeta


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Codec |String |`aac` |The audio encoding format. |
|Duration |Float |`2.943` |The audio duration, in seconds. |
|SampleRate |Integer |`44100` |The audio sampling rate, measured in Hz. |
|Bitrate |Integer |`127658` |The audio bitrate, measured in bps. |
|Channels |Integer |`2` |The number of audio channels. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=QueryUploadTaskInfo&Version=2023-01-01&JobIds=YourJobIds
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "QueryUploadTaskInfo",
        "Region": "ap-singapore-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": {
        "MediaInfoList": [
            {
            "RequestId": "RequestId",
            "JobId": "JobId",
            "SourceUrl": "SourceUrl",
            "State": "State",
            "Vid": "Vid",
            "SpaceName": "SpaceName",
            "AccountId": "AccountId",
            "CallbackArgs": "xxxxxxxxxxxx",
            "SourceInfo": {
                "Md5": "Md5",
                "FileType": "FileType",
                "Height": 1,
                "Width": 1,
                "Format": "Format",
                "Duration": 0.1,
                "Size": 0.1,
                "StoreUri": "StoreUri",
                "Bitrate": 1
            }
            }
        ],
        "NotExistJobIds": [
            "NotExistJobIds"
        ]
        }
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see the [shared errors of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter.UploadParamsError |\- |Invalid parameter for uploading. |
|400 |InvalidParameter.AKMissMatchError |\- |Access key mismatch. Please check your access key and VOD space. |
|400 |InvalidParameter.JobIdEmptyError |\- |The task ID is empty. |
|400 |InvalidParameter.SpaceNotExistsError |\- |The space does not exist. |
|400 |InvalidParameter.UrlTotalError |\- |The number of URL requests has exceeded the limit. |
|400 |InvalidParameter.JobIdTotalError |\- |The number of requests for JobId has exceeded the limit. |
|500 |InternalError.QueryBodyError |\- |Query failed. |
|500 |InternalError.BodyParseError |\- |Text parsing error. |
|500 |InternalError.CreateUploadStateError |\- |Failed to create upload status. |
|500 |InternalError.BuildRavenDataError |\- |Failed to create consumer data. |
|500 |InternalError.NsqSendError |\- |Message queue sending failed. |
|500 |InternalError.GetAccountError |\- |Failed to get account. |


#{.custom\-md\-table\-4}#

&nbsp;
