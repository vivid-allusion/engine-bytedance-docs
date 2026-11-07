---
title: "ListPullToPushTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtask-2023-zh-TW"
---

呼叫 `ListPullToPushTask` API，以分頁方式查詢中繼任務列表，並支援依任務名稱模糊搜尋。

## 需求

速率限制：每個帳戶每秒最多 15 次查詢。

## HTTP 請求

* 方法：GET

* 端點：[https://open.byteplusapi.com/?Action=ListPullToPushTask&Version=2023-01-01](https://open.byteplusapi.com/?Action=ListPullToPushTask&Version=2023-01-01)

## 請求參數

### 通用參數

所有 API 除了需傳遞 API 專屬參數外，還必須包含 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查詢

|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ListPullToPushTask` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |
|Page |Integer |否 |`1` |頁碼。值必須大於或等於 `1`。預設值：`1`。 |
|Size |Integer |否 |`20` |每頁查詢結果數量。有效值：[1,500]。預設值：`20`。<br><br>> **说明**<br><br><br>> 如果您將此參數設為 `0`，則使用預設值。<br> |
|Title |String |否 |`doc` |中繼任務名稱。搜尋不區分大小寫，並支援模糊搜尋。例如，若將 `Title` 設為 `doc`，則可能取得名稱中包含 `doc` 的中繼任務列表，如 `docspace`、`docs`、以及 `DOC`。 |

## 回應參數

如需 API 專屬回應參數，請參閱下表。更多詳細資訊請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|List |[List](https://docs.byteplus.com/en/docs/24/107372#list) 陣列 |`-` |您的中繼任務列表。 |
|Pagination |[Pagination](https://docs.byteplus.com/en/docs/24/107372#pagination) 物件 |`-` |分頁資訊。 |

### 列表

|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Title |String |`task001` |中繼任務名稱。 |
|TaskId |String |`fde6aa0281d*******9a6e24236` |任務 ID。 |
|StartTime |String |`2022-04-01T00:00:00Z` |中繼任務開始時間（RFC 3339 格式的 UTC 時間）。 |
|EndTime |String |`2022-04-02T00:00:00Z` |中繼任務結束時間（RFC 3339 格式的 UTC 時間）。 |
|CallbackURL |String |`http://example.mtime.cn/live/example/callbackapi` |用於接收中繼任務事件的回調地址。 |
|Type |Integer |`0` |串流來源類型。有效值包括：<br><br><br>* `0`：串流內容來自直播來源。<br><br>* `1`：串流內容來自隨選影片。 |
|CycleMode |Integer |`-1` |串流循環模式。唯一有效值為 `-1`：順序循環。 |
|DstAddr |String |`rtmp://example.mtime.cn/Video/2022/02/04/mp4/190204084208765161.mp4` |推流地址。 |
|SrcAddr |String |`http://example.mtime.cn/Video/2003/02/04/mp4/190204084208765161.mp4` |拉流地址，當 Type 為 0 時返回。 |
|SrcAddrS |String 陣列 |`["http://example.mtime.cn/Video/2003/02/04/mp4/190204084208765161.mp4"]` |隨選影片列表，當 Type 為 1 時返回。 |
|Status |String |`Pending` |中繼任務狀態。<br><br><br>* `Disabled`：中繼任務已停用。<br><br>* `Pending`：中繼任務準備啟動。<br><br>* `Enabled`：表示中繼任務正在進行中，並於設定的開始時間啟動。<br><br>* `Ended`：此狀態於中繼任務設定的結束時間後出現。 |
|DstAddrType |Integer |`1` |推流地址類型。有效值包括：<br><br><br>* `1`：BytePlus MediaLive 推流地址。<br><br>* `2`：第三方推流地址。 |

### 分頁

|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|PageCur |Integer |`1` |目前頁碼。 |
|PageSize |Integer |`10` |每頁結果數量。 |
|PageTotal |Integer |`108` |頁數總數。 |
|TotalCount |整數 |`1073` |結果總數。 |

## 範例

### 範例請求

### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202112311457440101742350380352BCC7",
        "Action": "ListPullToPushTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "List": [
            {
                "CallbackURL": "",
                "CycleMode": -1,
                "DstAddr": "rtmp://example.org/Video/2022/02/04/mp4/190204084208765161.mp4",
                "EndTime": "2022-01-01T23:44:32+08:00",
                "SrcAddr": "http://example.org/Video/2003/02/04/mp4/190204084208765161.mp4",
                "SrcAddrS": [],
                "DstAddrType": 2,
                "StartTime": "2021-12-31T22:44:23+08:00",
                "Status": "Pending",
                "TaskId": "8fde6aa0281d9f6e15e6059a6e242365",
                "Title": "sutest007",
                "Type": 0
            }
        ],
        "Pagination": {
            "PageCur": 1,
            "PageSize": 10,
            "PageTotal": 108,
            "TotalCount": 1073
        }
    }
}
```

## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|**狀態碼** |**錯誤碼** |**錯誤訊息** |**描述** |
|---|---|---|---|
|200 |CommonErr | |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam | |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107372#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證未通過。請檢查資料型別是否正確。 |
|403 |RequestForbidden | |因當前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置、憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |請求被拒絕。當前帳戶下無請求資源（網域空間、網域名稱、應用、配置範本、憑證）。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 未開通計費狀態，請開通服務或充值。 |尚未啟用視訊直播服務或帳戶欠費，導致帳單不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|403 |AccessDenied |使用者未獲授權執行：%s 於資源：%s |請求被拒絕。當前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、應用、配置範本、憑證）或 API 權限。 |
|404 |ResourceNotFound | |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置、憑證）。建議重試。若仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
