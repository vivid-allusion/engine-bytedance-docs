---
title: "GetSubtitleInfoList"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-getsubtitleinfolist"
---

This interface is used to obtain the subtitle file.

<span id="usage-scenario"></span>
## Usage scenario

Supports getting all subtitle files under a specified `Vid`, or getting corresponding subtitles by specifying conditions (file ID, language, tag, status, etc.).

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=GetSubtitleInfoList&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetSubtitleInfoList` |The API action. For the current API, the value is `GetSubtitleInfoList`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|Vid |String |Yes |`v02c24g10***1v0vp92fsfu0` |The video ID. After uploading the audio and video, the methods to obtain the `Vid` are as follows:<br><br><br>* Query through the [GetMediaList](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getmedialist) interface.<br><br>* If upload callbacks are enabled, the value of `Vid` will be returned in [FileUploadComplete](https://docs.byteplus.com/en/docs/byteplus-vod/docs-fileuploadcomplete). |
|FileIds |String |No |`ueyrfeuiw2388***` |The list of transcoded file IDs. If not provided, it defaults to returning all subtitles under `Vid`. Separate multiple IDs with a comma `,`. A maximum of 20 IDs are allowed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Duplicate or null values in the parameters will be filtered out by default.</div><br> |
|Languages |String |No |`cmn-Hans-CN` |The list of subtitle languages. Supported values:<br><br><br>* `cmn-Hans-CN`: Simplified Chinese.<br><br>* `eng-US`: English.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more languages, see <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-subtitle-language">subtitle languages</a>.</div><br> |
|Formats |String |No |`webvtt` |The subtitle format. The values are as follows:<br><br><br>* `webvtt`<br><br>* `ass`<br><br>* `srt`<br><br>* `ssa` |
|LanguageIds |String |No |`1` |The subtitle language ID list. Separate multiple values with ",". The values are as follows:<br><br><br>* `1`: Simplified Chinese.<br><br>* `2`: English.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more languages, see <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-subtitle-language">subtitle languages</a>.</div><br> |
|SubtitleIds |String |No |`-482590843` |The subtitle ID list, multiple separated by a comma `,`. |
|Status |String |No |`Published` |Subtitle Status List. The values are as follows:<br><br><br>* `Published`: Published.<br><br>* `Unpublished`: Unpublished. |
|Title |String |No |`The video.` |The title. |
|Tag |String |No |`The video 01.` |The label. |
|Offset |String |No |`0` |Offset. Default is 0.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect when specifying <code>FileIds</code> to retrieve subtitle files.</div><br> |
|PageSize |String |No |`10` |Page size. The default is 10, with a maximum of 20.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect when specifying <code>FileIds</code> to retrieve subtitle files.</div><br> |
|Ssl |String |No |`0` |Whether the subtitle URL is an HTTPS address. Supported values:<br><br><br>* `1`: Yes.<br><br>* `0`: No (default). |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vid |String |`v02c24g1000***s1v0vp92fsfu0` |The video ID. |
|FileSubtitleInfoList |Array of [VodFileSubtitleInfo](https://docs.byteplus.com/en/docs/25/8027#vodfilesubtitleinfo) |`-` |The list of subtitle information |
|NotExistFileIds |Array of String |`[]` |The list of file IDs that do not exist. |
|TotalCount |Integer |`1` |The total number of results that meet the conditions. |
|Offset |Integer |`0` |The offset of the current query. |
|PageSize |Integer |`10` |The page size. |


#{.custom\-md\-table\-4}#

<span id="vodfilesubtitleinfo"></span>
### VodFileSubtitleInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|FileId |String |`ueyrfeuiw2388***` |The subtitle file ID. |
|SubtitleInfoList |Array of [VodSubtitleInfo](https://docs.byteplus.com/en/docs/25/8027#vodsubtitleinfo) |`-` |The subtitle list. |


#{.custom\-md\-table\-4}#

<span id="vodsubtitleinfo"></span>
### VodSubtitleInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vid |String |`v029c1g10003civ2i5mqib*******` |The video ID. |
|FileId |String |`v029c1g10003civ2i5mqib*******` |The subtitle file ID. |
|Language |String |`eng-US` |The subtitle language. |
|LanguageId |Integer |`1` |The subtitle language ID. For details, see [subtitle languages](https://docs.byteplus.com/en/docs/byteplus-vod/docs-subtitle-language). |
|Format |String |`webvtt` |The subtitle format. |
|SubtitleId |String |`123` |The subtitle ID. |
|Title |String |`subtitle.vtt` |The subtitle caption. |
|Tag |String |`subtitle` |The subtitle tag. |
|Status |String |`enable` |The subtitle status. |
|Source |String |`MU` |The subtitle source. |
|StoreUri |String |`tos-vod-cn-**/191fe22a1c4a49************` |The subtitle file storage location. |
|SubtitleUrl |String |`http://example.com/191fe22a1c4a************` |The subtitle file URL. |
|CreateTime |String |`2019-10-12T07:20:50.52Z` |The creation time. |
|Version |String |`1` |The subtitle version. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=GetSubtitleInfoList&Version=2023-01-01&Vid=v02c24g10***1v0vp92fsfu0&FileIds=ueyrfeuiw2388***&Languages=cmn-Hans-CN&Formats=webvtt&LanguageIds=1&SubtitleIds=-482590843&Status=Published&Title=The video.&Tag=The video 01.&Offset=0&PageSize=10&Ssl=0
```


<span id="Sample response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "GetSubtitleInfoList",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Vid": "v02c24g1000***s1v0vp92fsfu0",
        "Offset": 0,
        "PageSize": 10,
        "TotalCount": 1,
        "NotExistFileIds": [],
        "FileSubtitleInfoList": [
            {
                "FileId": "ueyrfeuiw2388***",
                "SubtitleInfoList": [
                    {
                        "Tag": "subtitle",
                        "Vid": "v029c1g10003civ2i5mqib*******",
                        "Title": "subtitle.vtt",
                        "FileId": "v029c1g10003civ2i5mqib*******",
                        "Format": "webvtt",
                        "Source": "MU",
                        "Status": "enable",
                        "Version": "1",
                        "Language": "eng-US",
                        "StoreUri": "tos-vod-cn-**/191fe22a1c4a49************",
                        "CreateTime": "2019-10-12T07:20:50.52Z",
                        "LanguageId": 1,
                        "SubtitleId": "123",
                        "SubtitleUrl": "http://example.com/191fe22a1c4a************"
                    }
                ]
            }
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see the [shared errors of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter.ItemLimitExceeded |\- |The number of `FileId` is greater than 20. |


#{.custom\-md\-table\-4}#

&nbsp;
