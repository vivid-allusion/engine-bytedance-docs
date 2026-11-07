---
title: "SetCallbackEvent"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-setcallbackevent"
---

This interface is used to set the callback event.

## Usage scenario

For the callback mechanism and supported events, see [Event notification overview](https://docs.byteplus.com/docs/byteplus-vod/docs-callback-notifications-).

## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=SetCallbackEvent&Version=2023\-01\-01

## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`SetCallbackEvent` |The API action. For the current API, the value is `SetCallbackEvent`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |Yes |`test` |The VOD space name. It can be obtained in the following ways:<br><br><br>* View the names of all spaces under the current account on the BytePlus VOD control panel [Spaces](https://console.byteplus.com/vodpaas/overview/).<br><br>* Call the [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) interface to obtain the names of all spaces under the current account. |
|Events |String |Yes |`FileUploadByUrlComplete` |The callback event list. The values are as follows:<br><br><br>* `FileUploadByUrlComplete`: Batch URL pull and upload completed.<br><br>* `FileUploadComplete`: Media assets upload completed<br><br>* `MaterialUploadComplete`: Material upload completed<br><br>* `TranscodeComplete`: Workflow execution completed<br><br>* `DeleteMediaComplete`: Media assets deletion completed<br><br>* `DeleteTranscodesComplete`: Media file deletion completed<br><br>* `VideoTrackComplete`: Video editing completed<br><br>* `UploadGetMetaComplete`: Media assets metadata upload and extraction completed<br><br>* `UpdateMediaStorageClassComplete`: Modification of the media assets storage type completed<br><br>* `ImageProcessComplete`: Image enhancement or basic image processing completed.<br><br>* `ImageDeleteComplete`: Image asset deletion completed.<br><br><br>> **Note**<br><br><br>> Multiple callback events can be set, separated by `,`.<br> |
|AuthEnabled |String |Yes |`1` |Whether to enable callback authentication. Supported values:<br><br><br>* `0`: (Default) Disabled.<br><br>* `1`: Enabled. |
|PrivateKey |String |No |`dsfhaesg887977` |Set the callback authentication key. The value range is [8,20], supporting uppercase letters, lowercase letters, and numbers.<br><br>> **Note**<br><br><br>> The `PrivateKey` is effective only when the `AuthEnabled` parameter is set to `1`.<br> |

## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#response) in the response.

## Samples

### Sample request

```text
https://vod.byteplusapi.com?Action=SetCallbackEvent&Version=2023-01-01&SpaceName=test&Events=FileUploadByUrlComplete&AuthEnabled=1&PrivateKey=dsfhaesg887977
```

### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "SetCallbackEvent",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    }
}
```

## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
