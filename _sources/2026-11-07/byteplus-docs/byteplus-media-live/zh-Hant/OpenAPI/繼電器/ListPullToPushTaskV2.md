---
title: "ListPullToPushTaskV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtaskv2-zh-tw"
---

呼叫 `ListPullToPushTaskV2` API，以分頁方式查詢轉推任務清單，支援依 Task 名稱模糊搜尋。

## 要求

速率限制：每個帳號每秒 15 次查詢。

## HTTP 請求

* 方法：POST

* 端點：[https://open.byteplusapi.com/?Action=ListPullToPushTaskV2&Version=2023-01-01](https://open.byteplusapi.com/?Action=ListPullToPushTaskV2&Version=2023-01-01)

## 請求參數

### 通用參數

所有 API 除 API 特定參數外，還必須搭配[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)呼叫。

### 查詢

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`ListPullToPushTaskV2` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### Body 參數

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|GroupNames |Array of String |否 |`default` |任務所屬的群組名稱。您可以呼叫 [ListPullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushgroup-2023) API 取得群組名稱。<br><br>> **说明**<br><br><br><br>* > 使用主帳號呼叫時，此欄位非必填。<br><br><br>* > 使用子帳號呼叫時，此欄位為必填。<br> |
|Title |String |否 |`doc` |轉推任務名稱。搜尋不區分大小寫，並支援模糊搜尋。例如，如果您將 `Title` 設為 `doc`，可能會取得名稱中包含 `doc` 的轉推任務清單，例如 `docspace`、`docs` 和 `DOC`。 |
|Page |Integer |否 |`1` |頁碼。值必須大於或等於 `1`。預設值：`1`。 |
|Size |Integer |否 |`20` |每頁查詢結果數量。有效值：[1,500]。預設值：`20`。<br><br>> **说明**<br><br><br>> 如果您將此參數設為 `0`，則使用預設值。<br> |

## 回應參數

如需 API 特定的唯一回應參數，請參閱下表。如需更多詳細資訊，請參閱[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|List |Array of [List](https://docs.byteplus.com/en/docs/24/124057#list) |`-` |您的轉推任務清單。 |
|Pagination |Object of [Pagination](https://docs.byteplus.com/en/docs/24/124057#pagination) |`-` |分頁資訊。 |

### List

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|Title |String |`task001` |轉推任務名稱。 |
|TaskId |String |`fde6aa0281d*******9a6e24236` |Task ID。 |
|StartTime |String |`2022-04-01T00:00:00Z` |轉推任務的開始時間（RFC 3339 格式的 UTC 時間）。 |
|EndTime |String |`2022-04-02T00:00:00Z` |轉推任務的結束時間（RFC 3339 格式的 UTC 時間）。 |
|CallbackURL |String |`http://example.mtime.cn/live/example/callbackapi` |用於接收轉推任務事件的回呼地址。 |
|Type |Integer |`0` |串流來源類型。有效值包括：<br><br><br>* `0`：串流內容從直播串流來源拉取。<br><br>* `1`：串流內容從隨選視訊拉取。 |
|CycleMode |Integer |`-1` |串流的循環模式。唯一有效值為 `-1`：循序循環。 |
|DstAddr |String |`rtmp://example.mtime.cn/Video/2022/02/04/mp4/190204084208765161.mp4` |推流地址。 |
|SrcAddr |String |`http://example.mtime.cn/Video/2003/02/04/mp4/190204084208765161.mp4` |拉流地址，當 Type 為 0 時傳回。 |
|SrcAddrS |Array of String |`["http://example.mtime.cn/Video/2003/02/04/mp4/190204084208765161.mp4"]` |隨選視訊清單，當 Type 為 1 時傳回。 |
|Status |String |`未开始` |轉推任務狀態。<br><br><br>* `Disabled`：轉推任務已停用。<br><br>* `Pending`：轉推任務已準備開始。<br><br>* `Enabled`：表示轉推任務正在進行中，並在定義的開始時間啟用。<br><br>* `Ended`：此狀態會在轉推任務的定義結束時間之後出現。 |
|DstAddrType |Integer |`1` |推流地址類型。有效值包括：<br><br><br>* `1`：BytePlus MediaLive 的推流地址。<br><br>* `2`：第三方推流地址。 |
|GroupName |String |`group001` |任務所屬的群組名稱。您可以呼叫 [ListPullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushgroup-2023) API 取得群組名稱。<br><br>> **说明**<br><br><br><br>* > 使用主帳號呼叫時，此欄位非必填。<br><br><br>* > 使用子帳號呼叫時，此欄位為必填。<br> |

### Pagination

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|PageCur |Integer |`1` |目前頁碼。 |
|PageSize |Integer |`10` |每頁的結果數量。 |
|PageTotal |Integer |`108` |總頁數。 |
|TotalCount |Integer |`1073` |結果總數。 |

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=ListPullToPushTaskV2&Version=2023-01-01
{
    "Page": 1,
    "Size": 20,
    "Title": "task001",
    "GroupNames": [
        "default"
    ]
}
```

### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202112311457440101742350380352BCC7",
        "Action": "ListPullToPushTaskV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
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
                "Status": "未开始",
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

以下是與目前操作相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|狀態碼 |錯誤碼 |錯誤訊息 |說明 |
|---|---|---|---|
|200 |CommonErr |\- |未分類錯誤。建議重試。如果仍傳回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/124057#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |參數驗證失敗。請檢查資料類型是否正確。 |
|403 |RequestForbidden |\- |請求遭拒，因為目前帳號下沒有請求的資源（資源包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |請求遭拒，因為目前帳號下沒有請求的資源（資源包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證）。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |視訊直播服務尚未啟用，或帳號欠費，導致帳單不可用。請檢查服務啟用狀態和帳號欠費狀態。 |
|403 |AccessDenied |User is not authorized to perform: %s on resource: %s |請求遭拒。目前帳號下沒有請求的資源（資源包括網域名稱空間、網域名稱、應用程式、設定範本、憑證）或 API 權限。 |
|404 |ResourceNotFound |\- |找不到資源（包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證）。建議重試。如果仍傳回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
