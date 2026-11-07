---
title: "RetrieveTranscodeResult"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-retrievetranscoderesults"
---

This interface is used to obtain the transcoding result. It requires the specified `Vid` and expected result type `ResultType` parameters.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=RetrieveTranscodeResult&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`RetrieveTranscodeResult` |The API action. For the current API, the value is `RetrieveTranscodeResult`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|Vid |String |Yes |`v0c2dfg7007***212h1nscckh79h0` |The video ID. After uploading audio and video, it can be obtained as follows:<br><br><br>* Query the audio and video Vid through the [GetMediaList](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getmedialist) interface.<br><br>* If a media asset upload completion callback event is set, the value of `Vid` will be returned in [FileUploadComplete](https://docs.byteplus.com/en/docs/byteplus-vod/docs-fileuploadcomplete). |
|ResultType |String |Yes |`inspection` |The expected type of results. The values are as follows:<br><br><br>* `inspection`: The result of film source inspection.<br><br>* `category_tags`: The result of video categorization.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">Supports multiple selections, separated by <code>,</code>. For example, <code>inspection,category_tags</code>.</div><br> |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vid |String |`v0c2dfg7007***212h1nscckh79h0` |The video ID, as the request value. |
|Inspection |Object of [Inspection](https://docs.byteplus.com/en/docs/25/8041#inspection) |`-` |The film source inspection result. |
|CategoryTags |Array of [CategoryTagInfo](https://docs.byteplus.com/en/docs/25/8041#categorytaginfo) |`-` |The video classification result. |


#{.custom\-md\-table\-4}#

<span id="inspection"></span>
### Inspection


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DeLogo |Array of [DeLogoInfo](https://docs.byteplus.com/en/docs/25/8041#delogoinfo) |`-` |The watermark detection result. |
|Quality |Object of [Quality](https://docs.byteplus.com/en/docs/25/8041#quality) |`-` |The video quality detection result. |


#{.custom\-md\-table\-4}#

<span id="delogoinfo"></span>
### DeLogoInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|AnchorWidth |Long |`671` |The anchor base width, measured in px. |
|AnchorHeight |Long |`893` |The anchor base width, measured in px. |
|PosX |Long |`462` |The watermark's top\-left X coordinate, measured in px. |
|PosY |Long |`654` |The watermark's top\-left Y coordinate, measured in px. |
|SizeX |Long |`601` |The watermark's width, measured in px. |
|SizeY |Long |`451` |The watermark's height, measured in px. |


#{.custom\-md\-table\-4}#

<span id="quality"></span>
### Quality


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Visual |Object of [VisualQuality](https://docs.byteplus.com/en/docs/25/8041#visualquality) |`-` |The film source inspection parameters. |
|VolumeInfo |Object of [VolumeInfo](https://docs.byteplus.com/en/docs/25/8041#volumeinfo) |`-` |The volume. |


#{.custom\-md\-table\-4}#

<span id="visualquality"></span>
### VisualQuality


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|VQScore |Double |`55.56` |The video quality score, ranging from [0, 100]. |
|Contrast |Double |`90.38` |The video contrast, ranging from [0, 100]. |
|Colorfulness |Double |`67.17` |The video colorfulness, ranging from [0, 100]. |
|Brightness |Double |`134.03` |The video brightness, ranging from [0, 100]. |
|Texture |Double |`12.04` |The video texture, ranging from [0, 100]. |
|Noise |Double |`86` |The video noise, ranging from [0, 100]. |


#{.custom\-md\-table\-4}#

<span id="volumeinfo"></span>
### VolumeInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Loudness |Double |`-37.5` |The loudness, measured in LUFS. |
|Peak |Double |`0.0912` |The peak value，ranging from (0, 1.0], normalized. |
|MeanVolume |Double |`-40.8` |The mean volume, measured in dB. |
|MaxVolume |Double |`-20.8` |The maximum volume, measured in dB. |


#{.custom\-md\-table\-4}#

<span id="categorytaginfo"></span>
### CategoryTagInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TagId |Long |`10101` |The tag ID. |
|Prob |Double |`0.022` |The confidence level. Confidence refers to the probability of the video classification result, ranging from [0,1]. |
|TagName |String |`Military` |The tag name. |
|Level |Long |`3` |The tag level. Values can be 1, 2, or 3. |
|ParentInfo |JSON Map |`{"1": "Arts","2": "Politics"}` |The parent node label. Format is `"key":"value"`.<br><br>`"key"` is of String type, representing the parent category level.<br><br>`"value"` is of String type, representing the parent category content. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=RetrieveTranscodeResult&Version=2023-01-01&Vid=v0c2dfg7007***212h1nscckh79h0&ResultType=inspection
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "RetrieveTranscodeResult",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Vid": "v0c2dfg7007***212h1nscckh79h0",
        "Inspection": {
            "DeLogo": [
                {
                    "PosX": 462,
                    "PosY": 654,
                    "SizeX": 601,
                    "SizeY": 451,
                    "AnchorWidth": 671,
                    "AnchorHeight": 893
                }
            ],
            "Quality": {
                "Visual": {
                    "Noise": 86,
                    "Texture": 12.04,
                    "VQScore": 55.56,
                    "Contrast": 90.38,
                    "Brightness": 134.03,
                    "Colorfulness": 67.17
                },
                "VolumeInfo": {
                    "Peak": 0.0912,
                    "Loudness": -37.5,
                    "MaxVolume": -20.8,
                    "MeanVolume": -40.8
                }
            }
        },
        "CategoryTags": [
            {
                "Prob": 0.022,
                "Level": 3,
                "TagId": 10101,
                "TagName": "Military",
                "ParentInfo": {
                    "1": "Arts",
                    "2": "Politics"
                }
            }
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
