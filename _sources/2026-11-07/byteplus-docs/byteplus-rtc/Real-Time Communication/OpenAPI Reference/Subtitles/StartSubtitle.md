---
title: "StartSubtitle"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1402681"
---

Call the StartSubtitle interface to start a real\-time subtitle task for a specified RTC room or WTN stream.

## Usage scenario

* The QPS under the account must not exceed 60.

* Before calling this API, you must enable this function on [RTC console-Settings-Realtime subtitle](https://console.byteplus.com/rtc/cloudRTC?&tab=subtitle).

* Using real\-time subtitles incurs additional charges. For billing details, see [Billing of Subtitle](https://docs.byteplus.com/docs/byteplus-rtc/docs-2608589).

* If the system detects that there is no audio upload in the room for 3 consecutive minutes, it will automatically stop the real\-time subtitle task for that room.

* The generated subtitles can be returned to the client or server in the form of a binary message encoded in Base64. You need to parse them before use (e.g., for real\-time display, storage, etc.). For the subtitle format description and how to parse, refer to [Real-time Call Subtitles and Translation](https://docs.byteplus.com/en/docs/byteplus-rtc/real-time-call-subtitles-and-translation-server-side).

## HTTP request

* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=StartSubtitle&Version=2024\-06\-01

## Request parameters

### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`StartSubtitle` |Interface name. The value of this interface: `StartSubtitle` |
|Version |String |Yes |`2024-06-01` |OpenAPI version. The value of this interface: `2024-06-01` |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`661e****543cf` |The only identifier for your audio & video app. See [get the AppId](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865#step-3-create-a-byteplus-rtc-app-and-get-the-appid). |
|TaskId |String |Yes |`Task1` |Subtitle task ID.<br><br>You can customize it to identify and manage (update, stop) subtitle tasks.<br><br><br>* **Naming convention**: It should match the regular expression [a\-zA\-Z0\-9_@\-.]{1,128}.<br><br>* **Uniqueness rule**: For RTC room subtitles, TaskId must be unique for each `AppId` and `RoomId` combination. |
|LanguageConfig |Object of [LanguageConfig](https://docs.byteplus.com/en/docs/12/120385#languageconfig) |Yes |`-` |Subtitle language configuration, including the source languages of RTC users or WTN streams and the target languages for translation. |
|RoomId |String |No |`Room1` |The ID of the RTC room where the subtitle task is running.<br><br>> **注意**<br><br><br>> Required only for RTC room subtitles when `LanguageConfig.SourceLanguages[].UserId` is specified.<br> |
|DistributionMode |Integer |Yes |`1` |The method used to receive subtitle results. Valid values:<br><br><br>* `1`: Receive subtitles on the client. Subtitle results are returned to the client in real time. This mode is suitable for real\-time subtitle display.<br><br>* `2`: Receive subtitles on the server. Subtitle results are returned sentence by sentence to the specified server address. This mode is suitable for storing and analyzing conversation data.<br><br>* `3`: Receive subtitles on both the client and the server.<br><br><br>> **注意**<br><br><br><br>* > When `LanguageConfig.SourceLanguages[].WtnStreamId` is specified, `DistributionMode` must be set to `2`.<br><br><br>* > When this parameter is set to `1` or `3`, the client must listen for the `onRoomBinaryMessageReceived` callback to receive subtitle data; When this parameter is set to 2 or 3, `ServerMessage` is required.<br><br><br>* > The generated subtitles will be returned to the client or server in binary format and need to be parsed before use. For the subtitle format description and how to parse, refer to [Real\-time Call Subtitles and Translation](https://docs.byteplus.com/en/docs/byteplus-rtc/real-time-call-subtitles-and-translation-server-side).<br> |
|ServerMessage |Object of [ServerMessage](https://docs.byteplus.com/en/docs/12/120385#servermessage) |No |`-` |The server\-side configuration for receiving subtitle results.<br><br>> **注意**<br><br><br>> This parameter is required when `DistributionMode` is set to `2` or `3`.<br> |
|ASRConfig |Object of [ASRConfig](https://docs.byteplus.com/en/docs/12/120385#asrconfig) |No |`-` |ASR advanced configuration. If this parameter is not passed, the default ASR recognition configuration is used. |
|ReceiverList |Array of String |No |`["user1","user2"]` |Users who receive subtitles on the client.<br><br><br>* If this parameter is not passed or is an empty array, all users in the room can receive subtitles.<br><br>* If a user ID list is specified, only users in the list can receive subtitles.<br><br><br>> **注意**<br><br><br>> This parameter takes effect only when `DistributionMode` is `1` or `3`.<br> |

### LanguageConfig

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|SourceLanguages |Array of [SourceLanguages](https://docs.byteplus.com/en/docs/12/120385#sourcelanguages) |Yes |`-` |Specifies the original speech language for RTC users or WTN streams. Each RTC user or WTN stream can be configured with only one source language. |
|RoomTargetLanguages |Array of String |No |`["en"]` |Target language for translated subtitles. If this parameter is not passed or is an empty array, only source\-language subtitles are generated and no translation is performed. For supported language codes, see Supported languages and language codes. |

### SourceLanguages

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|UserId |String |No |`user1` |ID of the user in the RTC room, to specify which user's speech the source language applies to.<br><br>> **注意**<br><br><br>> You must specify either `UserId` or `WtnStreamId`, but not both. When `UserId` is specified, `RoomId` is required.<br> |
|WtnStreamId |String |No |`<YOUR_WTN_STREAM_ID>` |Identifies the target WTN stream whose speech will be transcribed.<br><br>> **注意**<br><br><br>> You must specify either `UserId` or `WtnStreamId`, but not both. When `WtnStreamId` is specified, `DistributionMode` must be set to `2`.<br> |
|LanguageCode |Array of String |Yes |`["zh-CN"]` |The source language of the RTC user's or WTN stream's speech:<br><br><br>* `zh-CN`: Chinese<br><br>* `en-US`: English |

### ServerMessage

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Url |String |Yes |`https://example.com/subtitlemsg` |The server callback URL used to receive subtitle results. It needs to support the HTTP(S) protocol. |
|Signature |String |Yes |`TestSignature` |The callback authentication signature. When the platform sends subtitle callback requests to the specified `Url`, the request body contains the signature field. Your server must verify that the received signature is the same as the value configured here to confirm that the request source is trusted. |

### ASRConfig

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AdvancedParams |Object of [AdvancedParams](https://docs.byteplus.com/en/docs/12/120385#advancedparams) |No |`-` |Advanced parameters passed through to the BytePlus ASR service. |

### AdvancedParams

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|context |String |No |`{"hotwords":[{"word":"one"}, {"word":"two"}]}` |Hotword configuration passed through to ASR. |
|output_zh_variant |String |No |`traditional` |Controls whether Chinese ASR results are returned in Simplified Chinese or Traditional Chinese. Supported values are `traditional`, `tw`, and `hk`. If not passed, the result is Simplified Chinese. |

## Response parameters

This interface does not have any specific return parameters. See [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters) for returned common parameters.

On success, the Result field in the response is "success".

## Samples

### Sample request 1

RTC room subtitle

```json
POST https://open.byteplusapi.com?Action=StartSubtitle&Version=2024-06-01
{
    "AppId": "661e****543cf",
    "RoomId": "Room1",
    "TaskId": "Task1",
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
    "DistributionMode": 3,
    "ServerMessage": {
        "Signature": "TestSignature",
        "Url": "https://example.com/subtitlemsg"
    },
    "ReceiverList": [
        "user1",
        "user2"
    ],
    "ASRConfig": {
        "AdvancedParams": {
            "context": "{\"hotwords\": [{\"word\": \"CO2\"}]}"
        }
    }
}
```

### Sample response 1

```json
{
    "Result": "success",
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "StartSubtitle",
        "Version": "2024-06-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    }
}
```

### Sample request 2

WTN stream subtitle

```json
POST https://open.byteplusapi.com?Action=StartSubtitle&Version=2024-06-01
{
    "AppId": "661e****543cf",
    "TaskId": "Task1",
    "LanguageConfig": {
        "SourceLanguages": [
            {
                "WtnStreamId": "wtn_stream_123",
                "LanguageCode": [
                    "zh-CN"
                ]
            }
        ],
        "RoomTargetLanguages": [
            "en"
        ]
    },
    "DistributionMode": 2,
    "ServerMessage": {
        "Signature": "TestSignature",
        "Url": "https://example.com/subtitlemsg"
    },
    "ASRConfig": {
        "AdvancedParams": {
            "context": "{\"hotwords\":[{\"word\":\"one\"}, {\"word\":\"two\"}]}",
            "output_zh_variant": "traditional"
        }
    }
}
```

## Error codes

You can visit Common [Error Codes](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70426) for error code information.
