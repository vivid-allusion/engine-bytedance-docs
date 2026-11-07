---
title: "DeleteMedia"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-deletemedia"
---

This interface is used to delete all media assets associated with the specified `Vid` (video ID), including the uploaded source file, media processing output files, video covers, and frame extraction result records and files.

<span id="usage-scenario"></span>
## Usage scenario

After this interface is called successfully, the system will generate an asynchronous deletion task. You can configure the callback notification for the completion of media deletion. After it is enabled, you will receive a callback message for each Vid deletion. For detailed configuration methods, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/docs-callback-notification).

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DeleteMedia&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DeleteMedia` |The API action. For the current API, the value is `DeleteMedia`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|Vids |String |Yes |`v0dc24g1000***ps1v0lve1gj96g` |The video ID list. Multiple Vids are separated by a comma `,`. A maximum of 20 can be supported at one time. |
|CallbackArgs |String |No |`YourCallbackArgs` |You can customize the field, which will be transparently returned during the callback. Parse it yourself when handling the callback message. The maximum length is 512 bytes. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|NotExistVids |Array of String |`["v0dc24g10001cm***s1v0lve1gj96g"]` |The list of non\-existent video IDs. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=DeleteMedia&Version=2023-01-01&Vids=v0dc24g1000***ps1v0lve1gj96g&CallbackArgs=YourCallbackArgs
```


<span id="Sample response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DeleteMedia",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "NotExistVids": [
            "v0dc24g10001cm***s1v0lve1gj96g"
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see the [shared errors of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter.ItemLimitExceeded |\- |The number of input `Vid` exceeds the limit of 20. |


#{.custom\-md\-table\-4}#

&nbsp;
