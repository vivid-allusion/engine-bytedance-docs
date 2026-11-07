---
title: "DeleteAwardItem"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/DeleteAwardItem-zh-TW"
---

您可以使用此 API 從獎品庫中刪除指定的獎品。

<span id="Requirements"></span>
## 需求


* 速率限制：每個帳戶每秒最多 10 次請求

* 前提條件：需有 BytePlus 帳戶，或具備 **媒體庫** \> **獎品庫** \> **編輯** 權限的 IAM 使用者。如需新增 IAM 使用者的詳細資訊，請參閱 [管理使用者、組織和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://livesaas.byteplusapi.com/?Action=DeleteAwardItem&Version=2023\-08\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下表未包含所有通用請求參數。完整列表請參閱 [通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DeleteAwardItem` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。目前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Id |Long |是 |1715\*\*\*\*1256 |獎品 ID。您可以透過呼叫 [GetAwardItemList](https://docs.byteplus.com/en/docs/byteplus-livesaas/getawarditemlist) API 取得此 ID。 |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Status |Boolean |true |獎品是否成功刪除。成功時回傳 `true`。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```JSON
POST https://livesaas.byteplusapi.com/?Action=DeleteAwardItem&Version=2023-08-01
{
    "Id": 1715****1256
}
```


<span id="Sample response"></span>
### 回應範例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteAwardItem",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "Status": true
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

常見錯誤碼列表請參閱 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
