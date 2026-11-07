---
title: "GetPlaylists"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplaylists"
---

Get specified playlist information. Queries by ID, name, and other methods are supported.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=GetPlaylists&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetPlaylists` |The API action. For the current API, the value is `GetPlaylists`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |No |`test` |The space name. You can call [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) to obtain the names of all spaces under the current account. If not provided, it will query all playlists under the current account. |
|Ids |String |No |`pb2d500c119ddOn9cujc77uerlv1socg` |The IDs of the playlists. Multiple playlist IDs should be separated by commas. |
|Name |String |No |`11` |The name of the playlist (fuzzy matching supported). |
|Limit |Long |No |`0` |The default value is 0, which means all playlists under the current account will be returned. |
|Offset |Long |No |`0` |The offset of the current query. The default value is 0. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Total |Integer |`1` |The total number of playlists. |
|Playlists |Array of [VodPlaylistInfo](https://docs.byteplus.com/en/docs/25/8036#vodplaylistinfo) |`-` |The playlist information. |
|InvalidPlaylists |Array of [InvalidPlaylist](https://docs.byteplus.com/en/docs/25/8036#invalidplaylist) |`-` |The invalid playlist IDs. |


#{.custom\-md\-table\-4}#

<span id="vodplaylistinfo"></span>
### VodPlaylistInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Id |String |`pb2d500c119ddOn9cujc77uerlv1socg` |The playlist ID. |
|Name |String |`111` |The playlist name. |
|Codec |String |`H264` |The encoding format. Possible values:<br><br><br>* `mp3`<br><br>* `aac`<br><br>* `opus`<br><br>* `H264`<br><br>* `H265` |
|Cycles |String |`1` |The number of playback cycles. |
|Format |String |`mp4` |The container format. Possible values:<br><br><br>* `mp4`<br><br>* `dash`<br><br>* `hls`<br><br>* `mp3`<br><br>* `m4a`<br><br>* `ogg` |
|StartTime |String |`1746057600` |The start timestamp of the playback, in seconds. |
|EndTime |String |`1748044799` |The end timestamp of the playback, in seconds. |
|CreatedAt |Long |`1747885554` |The create timestamp of the playlist, in seconds. |
|UpdatedAt |Long |`1747916350` |The update timestamp of the playlist, in seconds. |
|Definition |String |`720p` |The video resolution. Supported values:<br><br><br>* `240p`<br><br>* `360p`<br><br>* `480p`<br><br>* `540p`<br><br>* `720p`<br><br>* `1080p`<br><br>* `2k`<br><br>* `4k`<br><br>* `od`<br><br>* `oe` |
|VideoInfos |Array of [VodPlaylistVideoInfo](https://docs.byteplus.com/en/docs/25/8036#vodplaylistvideoinfo) |`-` |The video information in the playlist. |


#{.custom\-md\-table\-4}#

<span id="vodplaylistvideoinfo"></span>
### VodPlaylistVideoInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vid |String |`vOc0adg78000d0n939bc77udishxpst0` |The video ID. |
|Title |String |`English.mp4` |The video title. |
|Duration |Double |`114.467` |The video duration. |
|PosterUrl |String |`http://byteplus-test.com/test.image` |The video cover URL. |
|VideoStatus |String |`Published` |The video status.Supported values:<br><br><br>* `Published`<br><br>* `Unpublished`<br><br>* `Deleted` |


#{.custom\-md\-table\-4}#

<span id="invalidplaylist"></span>
### InvalidPlaylist


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Id |String |`vOc0adg78111d0n939bc77udishxpst0` |The invalid playlist ID. |
|ErrorMessage |String |`invalid playlist` |The error message. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=GetPlaylists&Version=2023-01-01
{
    "SpaceName": "test",
    "Name": "11"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "GetPlaylists",
        "Region": "ap-singapore-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Total": 1,
        "Playlists": [
            {
                "Id": "pb2d500c119ddOn9cujc77uerlv1socg",
                "Name": "111",
                "Codec": "H264",
                "Cycles": "1",
                "Format": "mp4",
                "EndTime": "1748044799",
                "CreatedAt": 1747885554,
                "StartTime": "1746057600",
                "UpdatedAt": 1747916350,
                "Definition": "720p",
                "VideoInfos": [
                    {
                        "Vid": "vOc0adg78000d0n939bc77udishxpst0",
                        "Title": "English.mp4",
                        "Duration": 114.467,
                        "PosterUrl": "http://byteplus-test.com/test.image",
                        "VideoStatus": "Published"
                    }
                ]
            }
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
