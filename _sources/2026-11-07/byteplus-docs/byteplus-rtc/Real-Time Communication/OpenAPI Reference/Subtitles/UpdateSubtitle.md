---
title: "UpdateSubtitle"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1402683"
---

Call `UpdateSubtitle` to update the language settings of an ongoing real\-time subtitle task for a specified RTC room or WTN stream.

## HTTP request

* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=UpdateSubtitle&Version=2024\-06\-01

## Request parameters

### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateSubtitle` |Interface name. The value of this interface: `UpdateSubtitle` |
|Version |String |Yes |`2024-06-01` |OpenAPI version. The value of this interface: `2024-06-01` |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`661e****543cf` |The only identifier for your audio & video app. See [get the AppId](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865#step-3-create-a-byteplus-rtc-app-and-get-the-appid). |
|TaskId |String |Yes |`TestTaskID` |The ID of the subtitle task to update.<br><br>This value must be the same TaskId specified when calling `StartSubtitle`. |
|LanguageConfig |Object of [LanguageConfig](https://docs.byteplus.com/en/docs/12/120386#languageconfig) |No |`-` |Subtitle language configuration to update, including source and target languages. |
|RoomId |String |No |`Room1` |The ID of the RTC room where the subtitle task is running.<br><br>> **注意**<br><br><br>> Required only for RTC room subtitles started with `LanguageConfig.SourceLanguages[].UserId`. Pass the same `RoomId` used to start the task.<br> |
|ReceiverList |Array of String |No |`["user1","user2"]` |Users who receive subtitles on the client.<br><br><br>* If this parameter is not passed, the current receiver list remains unchanged.<br><br>* If this parameter is passed as an empty array, all users in the room can receive subtitles.<br><br>* If a user ID list is specified, only users in the list can receive subtitles.<br><br><br>> **注意**<br><br><br>> This parameter takes effect only when `DistributionMode` is `1` or `3`.<br> |

### LanguageConfig

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|SourceLanguages |Array of [SourceLanguages](https://docs.byteplus.com/en/docs/12/120386#sourcelanguages) |No |`-` |The source language of the RTC user's or WTN stream's speech. |
|RoomTargetLanguages |Array of String |No |`["en"]` |Target languages for translated subtitles. |

### SourceLanguages

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|UserId |String |No |`user1` |The ID of the user in the RTC room.<br><br>> **注意**<br><br><br>> You must specify either `UserId` or `WtnStreamId`, but not both.<br> |
|WtnStreamId |String |No |`wtn_stream_123` |The ID of the WTN stream whose source language configuration is updated.<br><br>> **注意**<br><br><br>> You must specify either `UserId` or `WtnStreamId`, but not both.<br> |
|LanguageCode |Array of String |No |`["zh-CN"]` |The source language of the RTC user's or WTN stream's speech:<br><br><br>* `zh-CN`: Chinese<br><br>* `en-US`: English |

## Response parameters

This interface does not have any specific return parameters. See [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters) for returned common parameters.

On success, the Result field in the response is "success".

## Samples

### Sample request

```json
POST https://open.byteplusapi.com?Action=UpdateSubtitle&Version=2024-06-01
{
    "AppId": "661e****543cf",
    "RoomId": "Room1",
    "TaskId": "TestTaskID",
    "LanguageConfig": {
        "SourceLanguages": [
            {
                "UserId": "user1",
                "LanguageCode": [
                    "zh-CN"
                ]
            }
        ],
        "RoomTargetLanguages": [
            "en"
        ]
    },
    "ReceiverList": [
        "user1",
        "user2"
    ]
}
```

### Sample response

```json
{
    "Result": "success",
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateSubtitle",
        "Version": "2024-06-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    }
}
```

## Error codes

You can visit Common [Error Codes](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70426) for error code information.
