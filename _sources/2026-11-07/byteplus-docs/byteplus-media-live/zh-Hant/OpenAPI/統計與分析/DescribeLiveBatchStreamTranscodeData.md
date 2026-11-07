---
title: "DescribeLiveBatchStreamTranscodeData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivebatchstreamtranscodedata-2023-zh-TW"
---

呼叫 `DescribeLiveBatchStreamTranscodeData` API，以查詢指定時間範圍內該網域名稱下所有轉碼串流的轉碼資料，例如轉碼時長、解析度等級和編碼方式。

## 要求

* 限制：支援查詢指定網域名稱下的流量資料，包括已刪除的網域名稱。

* 頻率限制：每個帳號每秒 30 次查詢。

* 資料延遲：資料延遲為 15 分鐘。

## HTTP 請求

* 方法：POST

* 端點：[https://open.byteplusapi.com/?Action=DescribeLiveBatchStreamTranscodeData&Version=2023-01-01](https://open.byteplusapi.com/?Action=DescribeLiveBatchStreamTranscodeData&Version=2023-01-01)

## 請求參數

### 公共參數

呼叫所有 API 時，除了 API 特定參數外，還必須帶上[公共參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查詢

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveBatchStreamTranscodeData` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### Body 參數

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|DomainList |String 陣列 |否 |`["push.example.com", "push2.example.com"]` |拉流網域清單。預設為空，表示將查詢所有網域。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面，以取得要查詢的拉流網域。 |
|StartTime |String |是 |`2022-11-10T00:00:00Z` |查詢範圍的開始時間（UTC 時間，採用 RFC 3339 格式，精確到秒）。<br><br>> **说明**<br><br><br>> 歷史查詢時間範圍的最大時間跨度為 366 天。<br> |
|EndTime |String |是 |`2022-11-11T00:00:00Z` |查詢範圍的結束時間（UTC 時間，採用 RFC 3339 格式，精確到秒）。 |
|PageSize |Integer |否 |`1000` |每頁的查詢結果數。有效值：[100,1000]。預設值：`1000`。<br><br>> **说明**<br><br><br>> 如果將此參數設為 `0`，則會使用預設值。<br> |
|PageNum |Integer |否 |`1` |頁碼。值必須大於或等於 `1`。預設值：`1`。 |

## 回應參數

如需 API 特定的唯一回應參數，請參閱下表。如需更多詳細資訊，請參閱[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|DomainList |String 陣列 |`["push.example.com", "push2.example.com"]` |網域清單。 |
|StartTime |String |`2022-11-10T00:00:00Z` |查詢的開始時間，為 UTC 時間，依 RFC3339 格式化，精確到秒。 |
|EndTime |String |`2022-11-11T00:00:00Z` |查詢的結束時間，為 UTC 時間，依 RFC3339 格式化，精確到秒。 |
|TotalDuration |Float |`40.1` |目前查詢條件下所有串流的總轉碼時長，單位為分鐘。 |
|StreamInfoList |[StreamInfoList](https://docs.byteplus.com/en/docs/24/107391#streaminfolist) 陣列 |`-` |依串流分段的資料。 |
|Pagination |[Pagination](https://docs.byteplus.com/en/docs/24/107391#pagination) 物件 |`-` |分頁資訊。 |

### StreamInfoList

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|Domain |String |`push.example.com` |網域名稱。 |
|App |String |`live` |串流位址的 AppName 欄位。 |
|Stream |String |`example_stream` |串流位址的 StreamName 欄位。 |
|Resolution |String |`720P` |轉碼解析度級別為選填，預設不套用特定解析度級別。例如，選擇 `720P` 表示轉碼設定將以視訊面積大於 `480P` 解析度（640x480），且小於或等於 `720P` 解析度（1280x720）的影片為目標。面積透過較長邊乘以較短邊計算。支援的值及其含義如下：<br><br><br>* `480P`：640 × 480；<br><br>* `720P`：1280 × 720；<br><br>* `1080P`：1920 × 1080；<br><br>* `2K`：2560 × 1440；<br><br>* `4K`：4096 × 2160；<br><br>* `8K`：大於 4096 x 2160；<br><br>* `0P`：純音訊轉碼，表示沒有視訊內容。 |
|Duration |Float |`20.1` |查詢時間內目前串流的總轉碼時長，單位為分鐘。 |
|VCodec |String |`Normal_H264` |視訊編碼格式：如果留空，預設值表示未指定編碼格式。支援的值及其含義如下：<br><br><br>* `Normal_H264`：H.264。<br><br>* `Normal_H265`：H.265。<br><br>* `Normal_H266`：H.266。<br><br>* `ByteHD_H264`：低位元率 HD 模式的 H.264。<br><br>* `ByteHD_H265`：低位元率 HD 模式的 H.265。<br><br>* `ByteHD_H266`：低位元率 HD 模式的 H.266。<br><br>* `ByteQE`：視訊畫質增強。<br><br>* `Audio`：純音訊串流。 |
|Coderate |Integer |`2000` |目前串流的轉碼位元率。 |

### Pagination

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|PageNum |Integer |`1` |目前頁碼。 |
|PageSize |Integer |`1000` |每頁的結果數。 |
|TotalCount |Integer |`2` |結果總數。 |

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveBatchStreamTranscodeData&Version=2023-01-01
{
  "StartTime": "2022-11-10T00:00:00Z",
  "EndTime": "2022-11-11T00:00:00Z"
}
```

### 範例回應

```json
{
  "ResponseMetadata":{
    "RequestId": "201806041104200100100232280022D30",
    "Action": "DescribeLiveBatchStreamTranscodeData",
    "Version": "2023-01-01",
    "Service": "live",
    "Region": "ap-singapore-1"
  },
  "Result":{
    "StartTime": "2022-11-10T00:00:00Z",
    "EndTime": "2022-11-11T00:00:00Z",
    "TotalDuration": 40,
    "StreamInfoList": [
      {
        "Domain": "pull.example.com"
        "Stream": "example_stream001",
        "App": "live",
        "Resolution": "720P",
        "Duration": 20,
        "VCodec": "Normal_H264"
      },
      {
        "Domain": "pull.example.com"
        "Stream": "example_stream002",
        "App": "live",
        "Resolution": "720P",
        "Duration": 20,
        "VCodec": "Normal_H264"
      }
    ],
    "Pagination": {
        "PageNum":    1,
        "PageSize":   1000,
        "TotalCount": 2,
    }
}
```

## 錯誤碼

以下是與目前操作相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 的通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|狀態碼 |錯誤碼 |錯誤訊息 |說明 |
|---|---|---|---|
|200 |CommonErr |\- |未分類錯誤。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107391#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |參數驗證失敗。請檢查資料類型是否正確。 |
|403 |RequestForbidden |\- |請求遭拒，因為目前帳號下沒有請求的資源（資源包括網域名稱空間、網域名稱、App 名稱、設定和憑證）。 |
|404 |ResourceNotFound |\- |找不到資源（包括網域名稱空間、網域名稱、App 名稱、設定和憑證）。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service 逾時。請[聯絡支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
