---
title: "LimitTokenPrivilege"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1188352"
---

You can use this interface to restrict the publishing permissions of a user's Token by specifying your AppId and RoomId.

<span id="usage-scenario"></span>
## Usage scenario

After restricting the publishing permissions of a user's token, the user who is currently publishing will be immediately stopped from publishing, and the users who have not yet published will not be able to publish within the restricted time.

When the publishing permissions of the current user are prohibited:


* The publishing\-side SDK will receive the onStreamStateChanged callback, with the error code ERROR_CODE_NO_PUBLISH_PERMISSION \-1002.

* The subscribing\-side SDK will receive a `onUserUnpublishStream` or `onUserUnpublishScreen` callback, with the StreamRemoveReason being `STREAM_REMOVE_REASON_OTHER(5)`.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=LimitTokenPrivilege&Version=2023\-11\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`LimitTokenPrivilege` |Interface name. The value of this interface: `LimitTokenPrivilege` |
|Version |String |Yes |`2023-11-01` |OpenAPI version. The value of this interface: `2023-11-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app. |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|UserId |String |Yes |`Your_UserId` |The ID of the users you wish to restrict. |
|Token |String |Yes |`You****ken` |The Token to be restricted |
|ForbiddenInterval |Integer |Yes |`60` |The duration for which the Token's publishing permissions are restricted, in seconds. The range of values is `[60,259200]`. If the value is greater than `0` and less than `60`, it is automatically changed to `60`. If the value is greater than `259200`, it is automatically changed to `259200`. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Message |String |`success` |Return "Success" when the request is successful, and empty upon failure. |
|EndTime |Integer |`1681660939` |The end time of the Token's permission restriction, in Unix time, with the unit being seconds. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=LimitTokenPrivilege&Version=2023-11-01
{
    "AppId": "You****pId",
    "RoomId": "Your_RoomId",
    "UserId": "Your_UserId",
    "Token": "You****ken",
    "ForbiddenInterval": 60
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "LimitTokenPrivilege",
        "Version": "2023-11-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Message": "success",
        "EndTime": 1681660939
    }
}
```


&nbsp;
