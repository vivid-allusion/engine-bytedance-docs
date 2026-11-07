---
title: "CommitUploadInfo"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-commituploadinfo"
---

Confirms the media assets uploading and gets the information of uploaded files.

> **Note**

* > For details on media asset types and formats, please refer to the [Uploading media assets overview page](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview).

* > For the complete upload process, please see [Server\-side uploads](https://docs.byteplus.com/docs/byteplus-vod/docs-server-side-uploads).

* > Once the upload is confirmed, `Vid` and other media asset information will be returned.

* > You can configure [FileUploadComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadcomplete) event notifications. When the media upload is completed, you will receive an event callback message. For configuration instructions, please see [Configuring callback settings](https://docs.byteplus.com/docs/byteplus-vod/docs-system#callbacks).

## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=CommitUploadInfo&Version=2023\-01\-01

## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`CommitUploadInfo` |The API action. For the current API, the value is `CommitUploadInfo`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |Yes |`test` |The VOD space name. You can obtain the space name through the following methods:<br><br><br>* View the names of all spaces under the current account on the [Spaces page](https://console.byteplus.com/vodpaas/overview/?) of the BytePlus Console.<br><br>* Call [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) to obtain the names of all spaces under the current account. |
|SessionKey |String |Yes |`eyJleHRyYSI6InM2MjM4Nz*****0ZzEwMDAxY20wa25paHMxdjBocWpnZ2RkODAifQ==` |The session ID. You can obtain it from the return parameters of the [ApplyUploadInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-applyuploadinfo) interface. |
|CallbackArgs |String |No |`Yourcallbackargs` |The customed pass\-through information. This is typically information that the server wishes to pass through from the client during an upload. |
|Functions |String |No |`[{"Name":"GetMeta"},{"Input":{"Title":"Video01.mp4"},"Name":"AddOptionInfo"},{"Input":{"TemplateId":"8ecbf1ede093407aa9908fe700cedd06"},"Name":"StartWorkflow"}]` |The upload functions, which can be used to take screenshots, set media asset information, trigger workflows, etc. To create an image asset, set `RecordType` to `3` in the `AddOptionInfo` upload function. For more details, see [Upload functions](https://docs.byteplus.com/docs/byteplus-vod/upload-functions). |

## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#response) section.

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Data |Object of [VodCommitUploadInfoData](https://docs.byteplus.com/en/docs/25/8017#vodcommituploadinfodata) |`-` |Media assets information. |

### VodCommitUploadInfoData

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vid |String |`v0dc24g10001c***ihs1v0hqjggdd80` |The video ID.<br><br>> **Note**<br><br><br>> When the request parameter `RecordType` is 1 (audio and video), return this parameter.<br> |
|PosterUri |String |`tos-vod-cn-v-03e4d***3112705/video01_cover` |The URI of the cover image corresponding to the video. |
|SourceInfo |Object of [VodSourceInfo](https://docs.byteplus.com/en/docs/25/8017#vodsourceinfo) |`-` |The video source information. |
|Mid |String |`weyiujweir379***` |The material ID.<br><br>> **Note**<br><br><br>> When the request parameter `RecordType` is 2 (material), return this parameter.<br> |

### VodSourceInfo

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
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
|Quality |String |`higher` |The audio quality. |
|DynamicRange |String |`SDR` |Dynamic range. The values are as follows:<br><br><br>* `HDR`<br><br>* `SDR` |
|FileName |String |`088ecee226***29d3e906c6.mp4` |The file path.<br><br>> **Note**<br><br><br>> This field is temporarily unavailable.<br> |
|VideoStreamMeta |Object of [VodVideoStreamMeta](https://docs.byteplus.com/en/docs/25/8017#vodvideostreammeta) |`-` |The video stream metadata. |
|AudioStreamMeta |Object of [VodAudioStreamMeta](https://docs.byteplus.com/en/docs/25/8017#vodaudiostreammeta) |`-` |The audio stream metadata. |

### VodVideoStreamMeta

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Codec |String |`h264` |The video codec. |
|Height |Integer |`270` |The video height, in pixels. |
|Width |Integer |`480` |The video width, in pixels. |
|Duration |Float |`2.944` |The video duration, measured in seconds. |
|Definition |String |`720p` |The video clarity. |
|Bitrate |Integer |`284910` |The video bitrate, measured in bps. |
|Fps |Float |`25` |The video frame rate, measured in fps. |

### VodAudioStreamMeta

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Codec |String |`aac` |The audio encoding format. |
|Duration |Float |`2.943` |The audio duration, in seconds. |
|SampleRate |Integer |`44100` |The audio sampling rate, measured in Hz. |
|Bitrate |Integer |`127658` |The audio bitrate, measured in bps. |
|Quality |String |`higher` |The audio quality, with the following values:<br><br><br>* `medium`: Standard<br><br>* `higher`: High<br><br>* `highest`: Music |

## Samples

### Sample request 1

Upload an audio or video file.

```text
https://vod.byteplusapi.com?Action=CommitUploadInfo&Version=2023-01-01&SpaceName=YourSpaceName&SessionKey=ApplyUploadInfoReturnSessionKey&CallbackArgs=""&GetMetaMode=&Functions=[{"Name": "GetMeta"},{"Name":"Snapshot","Input":{"SnapshotTime": 2.0}}]
```

### Sample response 1

```json
{
    "ResponseMetadata": {
        "Action": "CommitUploadInfo",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": {
            "Vid": "v0c255fa007abu0lc8a0oej77lbbv***",
            "SourceInfo": {
                "StoreUri": "tos-path-v-da1421/49ad5efabc3a4b32bed5df34fa7fd***",
                "Md5": "cf2b56eaa3fe3ec856ec4503a068a***",
                "Width": 960,
                "Height": 540,
                "Duration": 52.036,
                "Bitrate": 2068561,
                "Format": "MP4",
                "Size": 13454959,
                "FileType": "video"
            },
            "PosterUri": "tos-path-v-da1421/3108f4e3298248bda9e5658ae0a52***",
            "CallbackArgs": ""
        }
    }
}
```

### Sample request 2

Upload an audio or video material.

```text
https://vod.byteplusapi.com?Action=CommitUploadInfo&Version=2023-01-01&SpaceName=YourSpaceName&SessionKey=ApplyUploadInfoReturnSessionKey&CallbackArgs=""&GetMetaMode=&Functions=[{"name":"GetMeta"},{"name":"AddOptionInfo","input":{"Title":"01.mp4","Category":"video","FileType":"media","Format":"mp4","RecordType":2}}]
```

### Sample response 2

```json
{
    "ResponseMetadata": {
        "Action": "CommitUploadInfo",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": {
            "SourceInfo": {
                "Md5": "f6bd77b31cbd***4687a886df9c8",
                "FileType": "video",
                "Height": 1080,
                "Width": 2872,
                "Format": "MP4",
                "Duration": 11.423,
                "Size": 4301565,
                "StoreUri": "tos-vod-cn-v-03e4d54***112705/01.mp4",
                "Bitrate": 3012564,
                "Fps": 30,
                "VideoStreamMeta": {
                    "Codec": "h264",
                    "Height": 1080,
                    "Width": 2872,
                    "Duration": 11.423,
                    "Definition": "unknown",
                    "Bitrate": 3012564,
                    "Fps": 30
                },
                "AudioStreamMeta": {
                    "Duration": 11.422766,
                    "SampleRate": 44100,
                    "Bitrate": 128455
                },
                "FileName": "01.mp4"
            },
            "PosterUri": "tos-vod-cn-v-03e4d5***12705/01_cover",
            "Mid": "v02c24g10001cm***s1v0vvbrod9rg"
        }
    }
}
```

### Sample request 3

Upload an image material.

```text
https://vod.byteplusapi.com?Action=CommitUploadInfo&Version=2023-01-01&SpaceName=YourSpaceName&SessionKey=ApplyUploadInfoReturnSessionKey&CallbackArgs=""&GetMetaMode=&Functions=[{"name":"GetMeta"},{"name":"AddOptionInfo","input":{"Title":"03.png","Category":"image","FileType":"image","Format":"png","RecordType":2}}]
```

### Sample response 3

```json
{
    "ResponseMetadata": {
        "Action": "CommitUploadInfo",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": {
            "SourceInfo": {
                "Md5": "7ea8e3d4739d***6546dc9f71ac1d0",
                "Height": 378,
                "Width": 966,
                "Format": "png_pipe",
                "Size": 24221,
                "StoreUri": "tos-vod-cn-v-03e4d54***12705/03.png",
                "FileName": "03.png"
            },
            "Mid": "i0032s8ri4dl***83c77u4bfeg3utg"
        }
    }
}
```

### Sample request 4

Upload a subtitle or font material.

```text
https://vod.byteplusapi.com?Action=CommitUploadInfo&Version=2023-01-01&SpaceName=YourSpaceName&SessionKey=eyJBcHBJRCI6IiIsIkxlZ2FsIjoiIiwiVXNlcklEIjo***MjcwNS/lrZfluZUwMSJ9&CallbackArgs=""&GetMetaMode=&Functions=[{"name":"GetMeta"},{"name":"AddOptionInfo","input":{"Title":"subtitle.AAC.ass","Category":"subtitle","FileType":"object","Format":"ass","RecordType":2}}]
```

### Sample response 4

```json
{
    "ResponseMetadata": {
        "Action": "CommitUploadInfo",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": {
            "SourceInfo": {
                "Size": 228349,
                "StoreUri": "tos-vod-cn-v-03e4d5***112705/subtitle01",
                "FileName": "subtitle01"
            },
            "Mid": "s00d250hbohsc***jc77u3of8hvsfg"
        }
    }
}
```

## Error codes

The following are the error codes related to the current operation. For other error codes, see the [shared errors of BytePlus VOD](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter.InvalidAccessKeyError |\- |Invalid access key. |
|400 |InvalidParameter.InvalidParamError |\- |Invalid parameter. |
|400 |InvalidParameter.UserNotSupportTosError |\- |Account configuration error. |
|429 |RequestLimitExceeded.TooManyRequestError |\- |Request exceeds the limit. |
|400 |InvalidParameter.InvalidSpaceError |\- |Invalid space. |
|404 |ResourceNotFound.VideoNotFoundError |\- |Video not found. |
|400 |InvalidParameter.InvalidTopAccountError |\- |Account does not have permission. |
|400 |InvalidParameter.CategoryMismatchError |\- |The `Category` and `FileType` do not match for material upload. |
|400 |InvalidParameter.ImageDataProcessError |\- |Image data processing error. |
|403 |RequestForbidden.AccessIsRestricted |\- |Account access is restricted. |
|500 |InternalError.SaveDBError |\- |Internal error. |
|500 |InternalError.RunFunctionError |\- |Internal Error, function execution failed. |
|500 |InternalError.GetSignError |\- |Internal error, failed to get the upload URL signature. |
|500 |InternalError.RunPluginError |\- |Internal Error, plugin execution failed. |
