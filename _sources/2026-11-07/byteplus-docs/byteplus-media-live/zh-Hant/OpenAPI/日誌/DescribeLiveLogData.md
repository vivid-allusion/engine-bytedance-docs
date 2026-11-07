---
title: "DescribeLiveLogData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivelogdata-zh-TW"
---

呼叫 `DescribeLiveLogData` API，查詢網域產生的日誌檔案資訊。

## 要求

* 限制：

   * 支援查詢指定網域下產生的日誌檔案資訊（包含已刪除的網域）。

   * 支援查詢最近 31 天內產生的日誌資料。

   * 支援查詢日誌封裝檔案資訊。如需各種日誌格式的說明，請參閱[日誌格式](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-managing-logs#log-format)。

* 速率限制：每個帳號每秒 100 次查詢

* 資料延遲：1 小時

* 延遲日誌彙總：日誌檔案可能會有彙總延遲，內容會持續補充與附加。最完整的日誌檔案最多會在 24 小時內提供。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLiveLogData&Version=2023\-01\-01

## 請求參數

### 通用參數

呼叫所有 API 時，除了 API 特定參數外，還必須帶上[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查詢

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveLogData` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### 主體參數

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|StartTime |String |是 |`2022-04-13T10:00:00Z` |查詢範圍的結束時間，採用 RFC 3339 格式，精確到秒。<br><br>> **说明**<br><br><br><br>* > 目前只能查詢最近 31 天的日誌資料。<br><br><br>* > 日誌檔案依整點小時切分。請確保查詢的開始和結束時間包含查詢期間的整點時間。例如，如果需要查詢某天 07:30:00 到 08:10:00 的日誌資料，日誌查詢的開始時間應早於 07:00:00，結束時間應晚於 09:00:00。<br> |
|EndTime |String |是 |`2022-04-13T11:00:00Z` |查詢範圍的結束時間，採用 RFC 3339 格式，精確到秒。 |
|DomainList |String 陣列 |否 |`["push.example.com","push2.example.com"]` |網域名稱清單。預設表示目前使用者的所有推流和拉流網域名稱。<br><br>> **说明**<br><br><br>> 當日誌類型為 relay，即 `'Type': 'relay'` 時，此參數無效。<br> |
|Type |String |是 |`pull` |支援的日誌類型包括：<br><br><br>* `pull`：拉流日誌；<br><br>* `push`：推流日誌；<br><br>* `source`：回源日誌；<br><br>* `relay`：拉轉推流轉換日誌。 |
|PageNum |Integer |否 |`1` |頁碼。值必須大於或等於 `1`。預設值：`1`。 |
|PageSize |Integer |否 |`20` |每頁查詢結果數量。有效值：[1,1000]。預設值：`20`。<br><br>> **说明**<br><br><br>> 如果將此參數設為 `0`，則會使用預設值。<br> |

## 回應參數

如需 API 特有的回應參數，請參閱下表。如需更多詳細資訊，請參閱[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|StartTime |String |`2022-04-13T10:00:00Z` |查詢範圍的開始時間（UTC 時間，採用 RFC 3339 格式，精確到秒）。 |
|EndTime |String |`2022-04-13T11:00:00Z` |查詢範圍的結束時間（UTC 時間，採用 RFC 3339 格式，精確到秒）。 |
|DomainList |String 陣列 |`["push.example.com", "push2.example.com"]` |網域清單。 |
|Type |String |`pull` |支援的日誌類型包括：<br><br><br>* `pull`：拉流日誌；<br><br>* `push`：推流日誌；<br><br>* `source`：回源日誌；<br><br>* `relay`：拉轉推流轉換日誌。 |
|Pagination |[Pagination](https://docs.byteplus.com/en/docs/24/107378#pagination) 物件 |`-` |資料分頁資訊。 |
|LogInfoList |[LogInfoList](https://docs.byteplus.com/en/docs/24/107378#loginfolist) 陣列 |`-` |日誌檔案資訊清單。 |

### Pagination

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|PageNum |Integer |`1` |目前頁碼。 |
|PageSize |Integer |`20` |每頁顯示的資料項目數量。 |
|TotalCount |Integer |`123` |查詢結果中的資料項目總數。 |

### LogInfoList

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|Domain |String |`push.example.com` |網域名稱。<br><br>> **说明**<br><br><br>> 當日誌類型為 relay，即 `'Type': 'relay'` 時，此欄位為空。<br> |
|LogName |String |`example.com_2023_09_01_000000_010000_0.gz` |日誌檔案名稱，遵循如下命名慣例。<br><br><br>* 與網域名稱相關時：加速網域名稱_年_月_日_開始時間_結束時間_檔案分割編號。例如，`www.example.com_2023_08_11_000000_010000_0.gz`；<br><br>* 與網域名稱無關時：年_月_日_開始時間_結束時間_檔案分割編號。例如，`2023_08_11_000000_010000_0.gz`；<br><br>* 如果目前事件在某小時內產生的日誌數量超過 150 萬筆，則會產生多個日誌檔案，檔案分割編號表示日誌檔案順序，例如 `2023_08_11_000000_010000_0.gz`、`2023_08_11_000000_010000_1.gz`。 |
|LogSize |Integer |`12` |日誌檔案大小，單位為位元組。 |
|DateTime |String |`2022-04-13T00:00:00Z` |日誌檔案對應的小時區間，採用 RFC3339 格式 UTC 時間，精確到秒。 |
|DownloadUrl |String |`http://example.com/download/20230901/example.com_2023_09_01_000000_010000_0.gz?x-expires=1693918129` |日誌檔案的下載連結。 |

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveLogData&Version=2023-01-01
{
    "StartTime": "2023-09-01T00:00:00Z",
    "EndTime": "2023-09-01T23:00:00Z",
    "Type": "pull",
    "DomainList": [
        "example.com"
    ],
    "PageSize": 20,
    "PageNum": 1
}
```

### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "DescribeLiveLogData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "StartTime": "2023-09-01T00:00:00Z",
        "EndTime": "2023-09-01T23:00:00Z",
        "Type": "pull",
        "LogInfoList": [
            {
                "DateTime": "2023-09-01T22:00:00Z",
                "Domain": "example.com",
                "DownloadUrl": "http://example.com/download/20230901/example.com_2023_09_01_000000_010000_0.gz?x-expires=1693918129",
                "LogName": "example.com_2023_09_01_000000_010000_0.gz",
                "LogSize": 24900
            }
        ],
        "Pagination": {
            "PageNum": 1,
            "PageSize": 1,
            "TotalCount": 1
        }
    }
}
```

## 錯誤碼

以下是與目前操作相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|狀態碼 |錯誤碼 |錯誤訊息 |說明 |
|---|---|---|---|
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107378#request-parameters)說明進行檢查。 |
|403 |RequestForbidden |\- |由於目前帳號下沒有請求的資源，請求遭拒。資源包括網域名稱空間、網域名稱、應用程式名稱、組態和憑證。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
