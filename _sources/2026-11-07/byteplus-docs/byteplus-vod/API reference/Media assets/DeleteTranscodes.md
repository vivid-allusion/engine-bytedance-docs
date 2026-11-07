---
title: "DeleteTranscodes"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-deletetranscodes"
---

This interface is used to delete the transcoded files under the specified `Vid` (video ID) without deleting the source clips.

<span id="usage-scenario"></span>
## Usage scenario


* This interface can delete all or part of the transcoded files. If you only want to delete some files, you need to first obtain the `FileId` corresponding to the media file to be deleted through the [GetMediaInfos](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getmediainfos) interface.

* After this interface is successfully called, the system will generate an asynchronous deletion task. You can enable the callback notification of the completion of transcoded file deletion. After enabling it, you will receive a callback message after each `FileId` is deleted. For detailed configuration methods, see [Event notification](https://docs.byteplus.com/en/docs/byteplus-vod/docs-callback-notification).


<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DeleteTranscodes&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DeleteTranscodes` |The API action. For the current API, the value is `DeleteTranscodes`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|Vid |String |Yes |`v02c24g100***ps1v0q66n2o2h0` |The video ID. Only a single Vid is supported. The methods to obtain it are as follows:<br><br><br>* Query through the [GetMediaList](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getmedialist) interface.<br><br>* If upload callbacks are enabled, the value of `Vid` will be returned in [FileUploadComplete](https://docs.byteplus.com/en/docs/byteplus-vod/docs-fileuploadcomplete). |
|FileIds |String |No | |The list of transcoded file IDs. Multiple `FileId`s are separated by commas `,`, with a maximum of 20.<br><br>If you do not specify this parameter or the length is `0`, all transcoded files under the `Vid` will be deleted.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning"><code>FileId</code> must not include the <code>FileId</code> corresponding to the source clip. To delete all videos including the source clip, please use the <a href="https://docs.byteplus.com/en/docs/byteplus-vod/reference-deletemedia">DeleteMedia</a> interface.</div><br> |
|CallbackArgs |String |No |`YourCallbackArgs` |You can customize the field, which will be transparently returned during the callback. Parse it yourself when handling the callback message. The maximum length is 512 bytes. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|NotExistFileIds |Array of String |`[]` |The list of non\-existent transcoding file IDs. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=DeleteTranscodes&Version=2023-01-01&Vid=v02c24g100***ps1v0q66n2o2h0&FileIds=&CallbackArgs=YourCallbackArgs
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DeleteTranscodes",
        "Region": "ap-singapore-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "NotExistFileIds": []
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see the [shared errors of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter.ItemLimitExceeded |\- |The number of `FileIds` entered exceeds the limit of 20. |


#{.custom\-md\-table\-4}#

&nbsp;
