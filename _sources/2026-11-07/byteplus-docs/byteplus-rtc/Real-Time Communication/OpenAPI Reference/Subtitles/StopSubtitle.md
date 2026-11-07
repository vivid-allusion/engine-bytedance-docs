---
title: "StopSubtitle"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1402682"
---

Call StopSubtitle to stop an ongoing real\-time subtitle task in a specified RTC room. After the task is stopped, subtitle generation and delivery for the specified task end.

## HTTP request

* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=StopSubtitle&Version=2024\-06\-01

## Request parameters

### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`StopSubtitle` |Interface name. The value of this interface: `StopSubtitle` |
|Version |String |Yes |`2024-06-01` |OpenAPI version. The value of this interface: `2024-06-01` |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`661e****543cf` |The only identifier for your audio & video app. See [get the AppId](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865#step-3-create-a-byteplus-rtc-app-and-get-the-appid). |
|TaskId |String |Yes |`TestTaskID` |The ID of the subtitle task to update.<br><br>This value must be the same TaskId specified when calling `StartSubtitle`. |
|RoomId |String |No |`Room1` |The ID of the RTC room where the subtitle task is running. This value must be the same RoomId used when starting the subtitle task.<br><br>> **注意**<br><br><br>> Required only for RTC room subtitles when `LanguageConfig.SourceLanguages[].UserId` is specified.<br> |

## Response parameters

This interface does not have any specific return parameters. See [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters) for returned common parameters.

On success, the Result field in the response is "success".

## Samples

### Sample request

```json
POST https://open.byteplusapi.com?Action=StopSubtitle&Version=2024-06-01
{
    "AppId": "661****3cf",
    "RoomId": "Room1",
    "TaskId": "TestTaskID"
}
```

### Sample response

```json
{
    "Result": "success",
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "StopSubtitle",
        "Version": "2024-06-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    }
}
```

## Error codes

You can visit Common [Error Codes](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70426) for error code information.
