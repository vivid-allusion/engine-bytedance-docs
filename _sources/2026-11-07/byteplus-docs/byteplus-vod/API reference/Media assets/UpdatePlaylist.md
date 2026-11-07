---
title: "UpdatePlaylist"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-updateplaylist"
---

Update playlist configurations. You can modify attributes such as playlist name, container format, encoding format, resolution, included video content, playback time range, and loop count.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=UpdatePlaylist&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdatePlaylist` |The API action. For the current API, the value is `UpdatePlaylist`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|Id |String |Yes |`pb2d***One4cjc77u86s7pnfag` |The playlist ID. |
|Name |String |No |`111` |The playlist name. |
|Format |String |No |`mp4` |The container format. Supported values:<br><br><br>* `mp4`<br><br>* `dash`<br><br>* `hls`<br><br>* `mp3`<br><br>* `m4a`<br><br>* `ogg` |
|Codec |String |No |`H264` |The encoding format. Supported values:<br><br><br>* `mp3`<br><br>* `aac`<br><br>* `opus`<br><br>* `H264`<br><br>* `H265` |
|Definition |String |No |`720p` |The video resolution. Supported values:<br><br><br>* `240p`<br><br>* `360p`<br><br>* `480p`<br><br>* `540p`<br><br>* `720p`<br><br>* `1080p`<br><br>* `2k`<br><br>* `4k`<br><br>* `od`<br><br>* `oe` |
|Vids |String |No |`vOcO***0cqisbc77udishrp46g,vOcOad***d0ncerrc77udishrpt3g,v0c0***0n939bc77udishrpst0` |The Vids of the videos in the playlist. Multiple Vids should be separated by commas. A playlist can contain 1 to 100 unique videos, and they must be in the same space. |
|StartTime |String |No |`1747612800` |The start timestamp of the playback in seconds. The start time cannot be earlier than the current time. |
|EndTime |String |No |`1748563200` |The end timestamp of the playback in seconds. The end time cannot be earlier than the start time. |
|Cycles |String |No |`1` |The number of playback cycles. Set this parameter to<br><br>0 for infinite looping. |
|SpaceName |String |No |`test` |The space name. You can call [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) to obtain the names of all spaces under the current account. If not provided, it will query all playlists under the current account. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) in the response.

<span id="samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=UpdatePlaylist&Version=2023-01-01
{
    "Id": "pb2d***One4cjc77u86s7pnfag",
    "Name": "111",
    "Format": "mp4",
    "Codec": "H264",
    "Definition": "720p",
    "Vids": "vOcO***0cqisbc77udishrp46g,vOcOad***d0ncerrc77udishrpt3g,v0c0***0n939bc77udishrpst0",
    "StartTime": "1747612800",
    "EndTime": "1748563200",
    "Cycles": "1",
    "SpaceName": "test"
}
```


<span id="Sample response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UpdatePlaylist",
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
