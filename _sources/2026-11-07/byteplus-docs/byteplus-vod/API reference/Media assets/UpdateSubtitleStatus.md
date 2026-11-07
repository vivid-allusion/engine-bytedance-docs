---
title: "UpdateSubtitleStatus"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-updatesubtitlestatus"
---

This interface is used to modify the subtitle publish status.

<span id="usage-scenario"></span>
## Usage scenario

You can specify conditions to change the status of subtitles that meet the conditions to published or unpublished.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=UpdateSubtitleStatus&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateSubtitleStatus` |The API action. For the current API, the value is `UpdateSubtitleStatus`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|Vid |String |Yes |`v02c24g100***s1v0ss463bglg` |The video ID. After uploading audio and video, the methods to obtain it are as follows:<br><br><br>* Query through the [GetMediaList](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getmedialist) interface.<br><br>* If upload callbacks are enabled, the value of `Vid` will be returned in [FileUploadComplete](https://docs.byteplus.com/en/docs/byteplus-vod/docs-fileuploadcomplete). |
|FileIds |String |No |`v02c24g****s1v0ss463bglg` |The list of transcoded file IDs. If not provided, it defaults to returning all subtitles under the Vid. Separate multiple IDs with a comma `,`, with a maximum of 20 IDs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Duplicate or empty values in the parameters will be filtered out by default.</div><br> |
|Languages |String |No |`cmn-Hans-CN` |The list of the Subtitle languages. Supported values:<br><br><br>* `cmn-Hans-CN`: Simplified Chinese.<br><br>* `eng-US`: English.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more languages, see <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-subtitle-language">subtitle languages</a>.</div><br> |
|Formats |String |No |`webvtt` |The subtitle format list, separated by commas `,`. The supported values:<br><br><br>* `webvtt`<br><br>* `ass`<br><br>* `srt`<br><br>* `ssa` |
|Status |String |Yes |`Published` |The subtitle status list. Supported values:<br><br><br>* `Published`: Published.<br><br>* `Unpublished`: Unpublished. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|NotExistFileIds |Array of String |`["v0dc24g10001cm***s1v0lve1gj96g"]` |The list of non\-existent transcoding `FileId`. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=UpdateSubtitleStatus&Version=2023-01-01&Vid=v02c24g100***s1v0ss463bglg&FileIds=v02c24g****s1v0ss463bglg&Languages=cmn-Hans-CN&Formats=webvtt&Status=Published
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UpdateSubtitleStatus",
        "Region": "ap-singapore-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "NotExistFileIds": [
            "v0dc24g10001cm***s1v0lve1gj96g"
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
