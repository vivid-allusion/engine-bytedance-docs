---
title: "DescribeLiveTranscodeInfoData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivetranscodeinfodata-2023-zh-TW"
---

呼叫 `DescribeLiveTranscodeInfoData` API，查詢指定時間範圍內特定直播網域或直播流的詳細資料，例如轉碼任務 ID、流名稱、轉碼尾碼，以及轉碼開始和結束時間。

## 要求

* 速率限制：每個帳號每秒 100 次查詢

* 資料延遲：20 分鐘

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLiveTranscodeInfoData&Version=2023\-01\-01

## 請求參數

### 通用參數

除了 API 特定參數外，所有 API 都必須使用[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)呼叫。

### 查詢

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveTranscodeInfoData` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### 主體參數

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|DomainList |String 陣列 |否 |`["push.example.com","push.example2.com"]` |網域清單。預設為空，表示將查詢您 BytePlus MediaLive 下所有網域的轉碼資料。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 主控台的[網域](https://console.byteplus.com/live/main/domain/list)頁面，取得要查詢的網域。 |
|App |String |否 |`live` |直播流 URL 中的 AppName 欄位。可包含大寫字母 (A\-Z)、小寫字母 (a\-z)、數字 (0\-9)、底線 (_)、連字號 (\-) 和句點 (.)，長度為 1 到 30 個字元。<br><br>> **说明**<br><br><br>> 查詢流粒度資料時，`App` 和 `Stream` 參數皆為必填。<br> |
|Stream |String |否 |`example_stream` |直播流 URL 中的 StreamName 欄位。可包含大寫字母 (A\-Z)、小寫字母 (a\-z)、數字 (0\-9)、底線 (_)、連字號 (\-) 和句點 (.)，長度範圍為 1 到 100 個字元。<br><br>> **说明**<br><br><br>> 查詢流粒度資料時，`App` 和 `Stream` 參數皆為必填。<br> |
|StartTime |String |是 |`2021-04-13T00:00:00Z` |查詢範圍的開始時間，採用 RFC 3339 格式，精確到秒。<br><br>> **说明**<br><br><br>> 歷史查詢的最大時間範圍為 366 天。<br> |
|EndTime |String |是 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，採用 RFC 3339 格式，精確到秒。 |
|TranscodeType |String 陣列 |否 |`["Normal_H264","ByteHD_H265"]` |視訊編解碼器。預設值為空，表示未指定視訊編解碼器。可取以下值：<br><br><br>* `Normal_H264`：H.264 標準轉碼；<br><br>* `Normal_H265`：H.265 標準轉碼；<br><br>* `ByteHD_H264`：H.264 低位元率高畫質；<br><br>* `ByteHD_H265`：H.265 低位元率高畫質；<br><br>* `ByteQE`：視訊增強；<br><br>* `Audio`：音訊流。 |
|Resolution |String 陣列 |否 |`["720P","1080P"]` |轉碼視訊的解析度。例如，720P 解析度表示轉碼視訊的總面積大於 480P (640 × 480)，且小於或等於 720P (1280 × 720)。<br><br><br>* `480P`：640 × 480；<br><br>* `720P`：1280 × 720；<br><br>* `1080P`：1920 × 1088；<br><br>* `2K`：2560 × 1440；<br><br>* `4K`：4096 × 2160；<br><br>* `8K`：\> 4096 x 2160；<br><br>* `0P`：音訊流轉碼。 |
|PageNum |Integer |否 |`1` |頁碼。值必須大於或等於 `1`。預設值：`1`。 |
|PageSize |Integer |否 |`20` |每頁查詢結果數量。有效值：[1,100000]。預設值：`20`。<br><br>> **说明**<br><br><br>> 如果將此參數設為 `0`，則使用預設值。<br> |

## 回應參數

如需 API 特定的唯一回應參數，請參閱下表。如需更多詳細資訊，請參閱[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|DomainList |String 陣列 |`["push.example.com","push.example2.com"]` |網域名稱清單。 |
|App |String |`live` |直播流 URL 中的 AppName 欄位，用於查詢流粒度。 |
|Stream |String |`example_stream` |直播流 URL 中的 StreamName 欄位，用於查詢流粒度。 |
|StartTime |String |`2021-04-13T00:00:00Z` |查詢範圍的開始時間，採用 RFC 3339 格式，精確到秒。 |
|EndTime |String |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，採用 RFC 3339 格式，精確到秒。 |
|TranscodeType |String 陣列 |`["Normal_H264","ByteHD_H265"]` |視訊編解碼器。預設值為空，表示未指定視訊編解碼器。可取以下值：<br><br><br>* `Normal_H264`：H.264 標準轉碼；<br><br>* `Normal_H265`：H.265 標準轉碼；<br><br>* `ByteHD_H264`：H.264 低位元率高畫質；<br><br>* `ByteHD_H265`：H.265 低位元率高畫質；<br><br>* `ByteQE`：視訊增強；<br><br>* `Audio`：音訊流。 |
|Resolution |String 陣列 |`["720P","1080P"]` |轉碼視訊的解析度。例如，720P 解析度表示轉碼視訊的總面積大於 480P (640 × 480)，且小於或等於 720P (1280 × 720)。<br><br><br>* `480P`：640 × 480；<br><br>* `720P`：1280 × 720；<br><br>* `1080P`：1920 × 1088；<br><br>* `2K`：2560 × 1440；<br><br>* `4K`：4096 × 2160；<br><br>* `8K`：\> 4096 x 2160；<br><br>* `0P`：音訊流轉碼。 |
|TranscodeInfoDataList |[TranscodeInfoDataList](https://docs.byteplus.com/en/docs/24/107455#transcodeinfodatalist) 陣列 |`-` |所有時間粒度的資料。 |
|Pagination |[Pagination](https://docs.byteplus.com/en/docs/24/107455#pagination) 物件 |`-` |分頁資訊。 |

### TranscodeInfoDataList

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|TaskID |String |`yvnytvvnigm3456` |轉碼任務 ID。 |
|Stream |String |`example_stream` |直播流 URL 中的 StreamName 欄位。 |
|TranscodeSuffix |String |`hd` |轉碼尾碼。 |
|TranscodeType |String |`Normal_H264` |轉碼格式。可取以下值：<br><br><br>* `Normal_H264`：H.264 標準轉碼；<br><br>* `Normal_H265`：H.265 標準轉碼；<br><br>* `ByteHD_H264`：H.264 低位元率高畫質；<br><br>* `ByteHD_H265`：H.265 低位元率高畫質；<br><br>* `ByteQE`：視訊增強；<br><br>* `Audio`：音訊流。 |
|Resolution |String |`720P` |轉碼視訊的解析度。例如，720P 解析度表示轉碼視訊的總面積大於 480P (640 × 480)，且小於或等於 720P (1280 × 720)。<br><br><br>* `480P`：640 × 480；<br><br>* `720P`：1280 × 720；<br><br>* `1080P`：1920 × 1088；<br><br>* `2K`：2560 × 1440；<br><br>* `4K`：4096 × 2160；<br><br>* `8K`：\> 4096 x 2160；<br><br>* `0P`：音訊流轉碼。 |
|StartTime |String |`2022-03-07T00:00:00Z` |查詢範圍的開始時間，採用 RFC 3339 格式，精確到秒。 |
|EndTime |String |`2022-03-08T00:00:00Z` |查詢範圍的結束時間，採用 RFC 3339 格式，精確到秒。 |
|Duration |Float |`1.4475713543666666` |目前轉碼任務在查詢時間範圍內的轉碼時長，單位為分鐘。 |

### Pagination

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|PageCur |Integer |`1` |目前頁碼。 |
|PageSize |Integer |`20` |每頁結果數量。 |
|TotalCount |Integer |`1000` |結果總數。 |

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveTranscodeInfoData&Version=2023-01-01
{
    "DomainList": [
        "push.example.com",
        "push.example2.com"
    ],
    "StartTime": "2021-04-13T00:00:00Z",
    "EndTime": "2021-04-14T00:00:00Z",
    "App": "live",
    "Stream": "example_stream",
    "Resolution": [
        "720P",
        "1080P"
    ],
    "PageNum": 1,
    "PageSize": 20,
    "TranscodeType": [
        "Normal_H264",
        "ByteHD_H265"
    ]
}
```

### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveTranscodeInfoData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com",
            "push.example2.com"
        ],
        "StartTime": "2021-04-13T00:00:00Z",
        "EndTime": "2021-04-14T00:00:00Z",
        "App": "live",
        "Stream": "example_stream",
        "Resolution": [
            "720P",
            "1080P"
        ],
        "TranscodeInfoDataList": [
            {
                "Duration": 1.4475713543666666,
                "Resolution": "720P",
                "TranscodeType": "Normal_H264",
                "Stream": "example_stream",
                "TranscodeSuffix": "hd",
                "StartTime": "2022-03-07T00:00:00Z",
                "EndTime": "2022-03-08T00:00:00Z",
                "TaskID": "yvnytvvnigm3456"
            }
        ],
        "Pagination": {
            "PageCur": 1,
            "PageSize": 20,
            "TotalCount": 1000
        },
        "TranscodeType": [
            "Normal_H264",
            "ByteHD_H265"
        ]
    }
}
```

## 錯誤碼

以下是與目前操作相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|狀態碼 |錯誤碼 |錯誤訊息 |說明 |
|---|---|---|---|
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107455#request-parameters)說明進行檢查。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|403 |RequestForbidden |\- |請求遭拒，因為目前帳號下沒有請求的資源。資源包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證。 |
