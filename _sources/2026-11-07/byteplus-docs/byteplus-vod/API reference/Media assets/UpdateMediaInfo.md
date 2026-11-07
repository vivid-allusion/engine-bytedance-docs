---
title: "UpdateMediaInfo"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-updatemediainfo"
---

This interface is used to update media asset information through the `Vid` (video ID), including the title, description, tags, category, cover image, expiration time, etc.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=UpdateMediaInfo&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateMediaInfo` |The API action. For the current API, the value is `UpdateMediaInfo`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|Vid |String |Yes |`v03c24g100***ps1v0vcd6b5r1g` |The video ID. After the audio and video are uploaded, the methods to obtain it are as follows:<br><br><br>* Query through the [GetMediaList](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getmedialist) interface.<br><br>* If the upload callback is enabled, the value of `Vid` will be returned in [FileUploadComplete](https://docs.byteplus.com/en/docs/byteplus-vod/docs-fileuploadcomplete). |
|PosterUri |String |No |`tos-vod-cn-v-03***112705/hello vod_cover` |The video cover image URI. You can first obtain the URI of an image and then use this parameter to set the image as the video cover. For more information, please see [Video cover](https://docs.byteplus.com/en/docs/byteplus-vod/docs-video-cover). |
|Title |String |No |`The video.` |The video name. The maximum length is 128 characters. |
|Description |String |No |`The video test.` |The video description. The maximum length is 1,024 characters. |
|Tags |String |No |`01` |Video tags. Separate multiple entries with an English comma `,`.<br><br><br>* If you provide an empty string as input, all current tags will be deleted.<br><br>* If you don't specify this parameter, the current tags will remain unchanged. |
|ClassificationId |Long |No |`001` |The video classification ID.<br><br><br>* If not provided: No modification.<br><br>* If 0 is passed: Unclassified.<br><br>* If a classification ID is passed: Set to the corresponding classification. The classification ID can be created via [CreateVideoClassification](https://docs.byteplus.com/en/docs/byteplus-vod/reference-createvideoclassification). |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) in the response.

<span id="samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=UpdateMediaInfo&Version=2023-01-01&Vid=v03c24g100***ps1v0vcd6b5r1g&PosterUri=tos-vod-cn-v-03***112705/hello vod_cover&Title=The video.&Description=The video test.&Tags=01&ClassificationId=001&ExpireTime=2024-08-30T20:10:11+08:00
```


<span id="Sample response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UpdateMediaInfo",
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
