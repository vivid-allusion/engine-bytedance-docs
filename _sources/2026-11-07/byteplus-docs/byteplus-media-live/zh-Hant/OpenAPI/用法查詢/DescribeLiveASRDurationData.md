---
title: "DescribeLiveASRDurationData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveasrdurationdata-zh-TW"
---

調用 `DescribeLiveASRDurationData` API 以查詢指定時間範圍內 AI 語音轉字幕的時長。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒 30 次查詢

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLiveASRDurationData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳遞 API 專屬參數外，還必須傳遞 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveASRDurationData` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["push.example.com"]` |域名列表。預設為空，表示查詢你在 BytePlus MediaLive 下所有域名的 AI 語音轉字幕使用時長資料。你可以調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API 或前往 BytePlus MediaLive 控制台的 [域名](https://console.byteplus.com/live/main/domain/list) 頁面獲取需查詢的域名。 |
|AppList |Array of String |否 |`["live"]` |應用名稱列表，必須與直播流 URL 中的 AppName 欄位值一致。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 30 個字元。 |
|ASRSourceType |String |否 |`ZH` |此參數指 AI 語音轉字幕時語音的語言類型。預設表示查詢所有語言。具體取值及含義如下：<br><br><br>* `ZH`：中文；<br><br>* `EN`：英文；<br><br>* `JA`：日文；<br><br>* `KO`：韓文。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>ASRTargetTypeList</code> 與 <code>ASRSourceType</code> 必須同時指定。</div><br> |
|ASRTargetTypeList |Array of String |否 |`["ZH"]` |AI 語音轉字幕時生成的字幕語言類型列表。預設表示查詢所有語言。具體取值及含義如下：<br><br><br>* `ZH`：中文；<br><br>* `EN`：英文；<br><br>* `JA`：日文；<br><br>* `KO`：韓文。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>ASRTargetTypeList</code> 與 <code>ASRSourceType</code> 必須同時指定。</div><br> |
|StartTime |String |是 |`2021-04-13T00:00:00Z` |查詢範圍的開始時間，需符合 RFC 3339 格式，精確到秒。 |
|EndTime |String |是 |`2021-04-13T00:00:00Z` |查詢範圍的結束時間，需符合 RFC 3339 格式，精確到秒。 |
|Aggregation |Integer |否 |`300` |聚合時間粒度，單位為秒，支持以下時間粒度：<br><br><br>* `300`：（預設）5 分鐘。當時間粒度為 5 分鐘時，單次查詢的最大時間跨度為 31 天，歷史查詢時間範圍為 93 天；<br><br>* `3600`：1 小時。當時間粒度為 1 小時時，單次查詢的最大時間跨度為 93 天，歷史查詢時間範圍為 93 天；<br><br>* `86400`：1 天。當時間粒度為 1 天時，單次查詢的最大時間跨度為 93 天，歷史查詢時間範圍為 93 天。 |


<span id="Response parameters"></span>
## 回應參數

有關唯一的 API 專屬回應參數，請參見下表。更多詳情請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|DomainList |Array of String |`["push.example.com"]` |網域列表。 |
|AppList |字串陣列 |`["live"]` |應用程式名稱列表。 |
|ASRSourceType |字串 |`ZH` |AI 語音轉字幕過程中語音的語言類型，值及含義如下：<br><br><br>* `ZH`：中文；<br><br>* `EN`：英文；<br><br>* `JA`：日文；<br><br>* `KO`：韓文。 |
|ASRTargetTypeList |字串陣列 |`["ZH"]` |AI 語音轉字幕過程中生成字幕的語言類型列表，值及含義如下：<br><br><br>* `ZH`：中文；<br><br>* `EN`：英文；<br><br>* `JA`：日文；<br><br>* `KO`：韓文。 |
|StartTime |字串 |`2021-04-13T00:00:00Z` |查詢範圍的起始時間，格式為 RFC 3339，精確到秒。 |
|EndTime |字串 |`2021-04-13T00:00:00Z` |查詢範圍的結束時間，格式為 RFC 3339，精確到秒。 |
|Aggregation |整數 |`300` |資料粒度，單位為秒。 |
|Duration |浮點數 |`1.1` |AI 語音轉字幕轉碼的總時長，單位為分鐘。 |
|ASRDurationData |[ASRDurationData](https://docs.byteplus.com/en/docs/24/107410#asrdurationdata) 陣列 |`-` |所有時間粒度的資料。 |
|ASRDurationDetailData |[ASRDurationDetailData](https://docs.byteplus.com/en/docs/24/107410#asrdurationdetaildata) 陣列 |`-` |根據 AI 語音轉字幕過程中生成字幕的語言類型分割的時間粒度詳細資料。 |


<span id="asrdurationdata"></span>
### ASRDurationData


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|TimeStamp |字串 |`2021-04-13T00:00:00Z` |按時間粒度聚合資料時，每個時間粒度的起始時間，格式為 RFC3339 的 UTC 時間戳，精確到秒。 |
|Duration |浮點數 |`1.1` |在當前資料聚合時間粒度內，AI 語音轉字幕的時長，單位為分鐘。 |


<span id="asrdurationdetaildata"></span>
### ASRDurationDetailData


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|ASRSourceType |字串 |`ZH` |AI 語音轉字幕過程中語音的語言類型。 |
|ASRTargetTypeList |字串陣列 |`["ZH"]` |AI 語音轉字幕過程中生成字幕的語言類型列表。 |
|ASRDurationData |[ASRDurationData](https://docs.byteplus.com/en/docs/24/107410#asrdurationdata) 陣列 |`-` |根據語音的語言類型分割的所有時間粒度資料。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveASRDurationData&Version=2023-01-01
{
    "DomainList": [
        "push.example.com"
    ],
    "AppList": [
        "live"
    ],
    "ASRSourceType": "ZH",
    "ASRTargetTypeList": [
        "ZH"
    ],
    "StartTime": "2021-04-13T00:00:00Z",
    "EndTime": "2021-04-13T00:00:00Z",
    "Aggregation": 300
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveASRDurationData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com"
        ],
        "AppList": [
            "live"
        ],
        "ASRSourceType": "ZH",
        "ASRTargetTypeList": [
            "ZH"
        ],
        "StartTime": "2021-04-13T00:00:00Z",
        "EndTime": "2021-04-13T00:00:00Z",
        "Aggregation": 300,
        "Duration": 1.1,
        "ASRDurationData": [
            {
                "TimeStamp": "2021-04-13T00:00:00Z",
                "Duration": 1.1
            }
        ],
        "ASRDurationDetailData": [
            {
                "ASRSourceType": "ZH",
                "ASRTargetTypeList": [
                    "ZH"
                ],
                "ASRDurationData": [
                    {
                        "TimeStamp": "2021-04-13T00:00:00Z",
                        "Duration": 1.1
                    }
                ]
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [Request Parameters](https://docs.byteplus.com/en/docs/24/107410#request-parameters) 說明進行檢查。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [contact support](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [contact support](https://console.byteplus.com/workorder/create)。 |
