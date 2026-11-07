---
title: "UpdateSubtitleInfo"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-updatesubtitleinfo"
---

This interface is used to update the basic information of the subtitles, including the title, tags, etc.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=UpdateSubtitleInfo&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateSubtitleInfo` |The API action. For the current API, the value is `UpdateSubtitleInfo`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|Vid |String |Yes |`v02c24g10001***s1v0ss463bglg` |The video ID. After the audio and video are uploaded, the methods to obtain it are as follows:<br><br><br>* Query through the [GetMediaList](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getmedialist) interface.<br><br>* If upload callbacks are enabled, the value of `Vid` will be returned in [FileUploadComplete](https://docs.byteplus.com/en/docs/byteplus-vod/docs-fileuploadcomplete). |
|FileId |String |Yes |`v02c24g100****s1v0ss463bglg` |The media processing output file ID. |
|Language |String |No |`cmn-Hans-CN` |The list of the subtitle languages. Supported values:<br><br><br>* `cmn-Hans-CN`: Simplified Chinese.<br><br>* `eng-US`: English.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more languages, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-subtitle-language">subtitle languages</a>.</div><br> |
|Format |String |Yes |`webvtt` |The subtitle format. Supported values:<br><br><br>* `webvtt`<br><br>* `ass`<br><br>* `srt`<br><br>* `ssa` |
|Title |String |No |`The subtitle caption test.` |The subtitle title. The length cannot exceed 128 characters.<br><br><br>* If you don't specify this parameter, the current title will remain unchanged.<br><br>* If you provide an empty string as input, the current title will be deleted. |
|Tag |String |No |`The subtitle label test.` |The subtitle tag. The length cannot exceed 128 characters.<br><br><br>* If you don't specify this parameter, the current tag will remain unchanged.<br><br>* If you provide an empty string as input, the current tag will be deleted. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=UpdateSubtitleInfo&Version=2023-01-01&Vid=v02c24g10001***s1v0ss463bglg&FileId=v02c24g100****s1v0ss463bglg&Language=cmn-Hans-CN&Format=webvtt&Title=The subtitle caption test.&Tag=The subtitle label test.
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UpdateSubtitleInfo",
        "Region": "ap-singapore-1",
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
