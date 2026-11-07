---
title: "UpdateSnapshot"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-147060"
---

If you start a snapshotting task, you can use `UpdateSnapshot` to update set parameters.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=UpdateSnapshot&Version=2022\-06\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateSnapshot` |Interface name. The value of this interface: `UpdateSnapshot` |
|Version |String |Yes |`2022-06-01` |OpenAPI version. The value of this interface: `2022-06-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app |
|BusinessId |String |No |`Your_****nessId` |The Business identifier for your audio & video app |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|TaskId |String |Yes |`Your_TaskId` |Task ID. |
|ImageConfig |Object of [ImageConfig](https://docs.byteplus.com/en/docs/12/14257#imageconfig) |No |`/` |Currently only `ImageConfig.Interval` is supportted. |


<span id="imageconfig"></span>
### ImageConfig


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Format |Integer |No |`0` |The format of the image.<br><br><br>* `0` ( default): `JPEG`<br><br>* `1`: `PNG`.<br><br>   When the value is invalid, it is automatically adjusted to the default value. |
|Width |Integer |No |`0` |The actual width of the video frame used in px, and the value range is `[0,1920]`. The default value is `0`, and in this case, it is the same as the actual width of the video stream. If the value is invalid, it will be automatically adjusted to the default value. |
|Height |Integer |No |`0` |The actual height of the video frame in px, and the value range is `[0,1080]` . The default value is `0`. And in this case, it is the same as the actual height of the video stream. If the value is illegal, it will be automatically adjusted to the default value. |
|Interval |Float |No |`2.0` |The interval between consecutive screenshots, in seconds. Floating\-point values are supported with millisecond precision (0.001s).<br><br><br>* **Valid range**: `[0.1, 600]`<br><br>* **Default**: `2.0`<br><br>* Values with more than 3 decimal places will be truncated. |


<span id="response-parameters"></span>
## Response parameters

`Result` returns "ok" only when the request succeeds and null when it fails.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=UpdateSnapshot&Version=2022-06-01
{
    "AppId": "You****pId",
    "BusinessId": "Your_****nessId",
    "RoomId": "Your_RoomId",
    "TaskId": "Your_TaskId",
    "ImageConfig": {
        "Interval": 2
    }
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "Result": "ok",
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "UpdateSnapshot",
        "Version": "2022-06-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
