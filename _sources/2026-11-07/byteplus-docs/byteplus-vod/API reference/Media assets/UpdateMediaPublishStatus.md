---
title: "UpdateMediaPublishStatus"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-updatemediapublishstatus"
---

This interface is used to modify the media release status through the `Vid` (video ID).

<span id="usage-scenario"></span>
## Usage scenario

The video release status is divided into **Published** or **Unpublished**. The playback link can only be obtained after the video is published.

<span id="requirements"></span>
## Requirements

Effective time: The media asset publishing status changes take effect immediately.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=UpdateMediaPublishStatus&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateMediaPublishStatus` |The API action. For the current API, the value is `UpdateMediaPublishStatus`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|Vid |String |Yes |`v03c24g1000***hs1v0pm264r9gg` |The media ID. After the media is uploaded, it can be retrieved as follows:<br><br><br>* By querying the media Vid through the [GetMediaList](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getmedialist) interface, which is the value for the request parameter Vid.<br><br>* If upload callbacks are enabled, the value of `Vid` will be returned in [FileUploadComplete](https://docs.byteplus.com/en/docs/byteplus-vod/docs-fileuploadcomplete). |
|Status |String |Yes |`Unpublished` |The video publication status. The values are as follows:<br><br><br>* `Published`: video is released.<br><br>* `Unpublished`: video is offline. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=UpdateMediaPublishStatus&Version=2023-01-01&Vid=v03c24g1000***hs1v0pm264r9gg&Status=Unpublished
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UpdateMediaPublishStatus",
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
