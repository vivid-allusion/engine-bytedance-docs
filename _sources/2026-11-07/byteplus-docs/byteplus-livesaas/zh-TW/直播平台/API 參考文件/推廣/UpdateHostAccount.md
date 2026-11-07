---
title: "UpdateHostAccount"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/UpdateHostAccount-zh-TW"
---

在您的帳戶下新增一個主持人帳戶，或更新現有主持人帳戶的資訊。

<span id="Usage scenario"></span>
## 使用情境

您可以透過 `Id` 參數新增或更新主持人帳戶。


* 若要新增主持人帳戶，請在請求參數中省略 `Id`（主持人帳戶 ID），或將 `Id` 設為 `0`。

* 若要更新主持人帳戶資訊，請在請求參數中將 `Id` 設為欲更新的主持人帳戶 ID。您可以透過呼叫 [ListHostAccounts](https://docs.byteplus.com/en/docs/byteplus-livesaas/listhostaccounts) 取得 ID。


<span id="Requirements"></span>
## 需求


* 速率限制：每個帳戶每分鐘 120 次請求

* 前置條件：需有 BytePlus 帳戶，或具備行銷工具包 \> 編輯權限的 IAM 使用者。如需更多資訊，請參閱 [管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://livesaas.byteplusapi.com/?Action=UpdateHostAccount&Version=2023\-08\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下列表格未涵蓋所有通用請求參數。完整列表請參閱 [通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateHostAccount` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。目前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|HostAccount |[HostAccount](https://docs.byteplus.com/en/docs/11/113612#hostaccount) 物件 |否 |`-` |主持人帳戶資訊列表。 |
|GetFollowDataUrl |String |否 |`https://example.com` |查詢請求 URL。您需自行開發 OpenAPI 以查詢觀眾是否關注該主持人。如需更多資訊，請參閱 [將您的系統整合至 BytePlus Live](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-adding-a-brand-account#integrating-your-system-with-byteplus-live)。 |
|UpdateFollowDataUrl |String |否 |`https://example.com` |更新請求 URL。您需自行開發 OpenAPI 以更新觀眾對該主持人的關注狀態。如需更多資訊，請參閱 [將您的系統整合至 BytePlus Live](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-adding-a-brand-account#integrating-your-system-with-byteplus-live)。 |


<span id="hostaccount"></span>
### HostAccount


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Id |Long |否 |`114333` |主持人帳戶 ID。<br><br><br>* 新增主持人帳戶：可省略此參數，或將參數值設為 `0`。<br><br>* 更新主持人帳戶資訊：將欲更新的主持人帳戶 ID 設為參數值。您可以透過呼叫 [ListHostAccounts](https://docs.byteplus.com/en/docs/byteplus-livesaas/listhostaccounts) 取得 ID。 |
|Name |String |是 |`Host A` |主持人帳戶名稱。<br><br>值長度必須為 1\-260 個字元。 |
|AvatarUrl |String |是 |`https://example.com/a.png` |主持人帳戶頭像的 URL，必須以 https 開頭。 |
|IsFollowEnable |Integer |否 |`1` |指定是否允許觀眾在觀看頁面關注主持人。預設值：`0`。可用值：<br><br><br>* `0`：不允許觀眾關注主持人。<br><br>* `1`：允許觀眾關注主持人。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">若您正在更新主持人帳戶資訊，僅當與該主持人帳戶關聯的直播間在 <strong>Producer</strong> \> <strong>觀看限制</strong> 頁面將驗證類型或評論限制設為自訂時，觀眾才可關注主持人。如需更多資訊，請參閱 <a href="https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions">自訂驗證登入</a>。   </div><br>    |
|HomeUrl |String |否 |`https://example.com` |主持人帳戶首頁 URL。當觀眾在觀看頁面點擊主持人頭像或名稱時，將會跳轉至該 URL。 |
|ExternalPlatformId |String |否 |`abc123` |外部平台 ID，只能包含大小寫字母及數字，且長度不得超過 128 個字元。 |
|ExtraInfo |字串 |否 |`abc` |與主機帳戶相關的額外資訊。 |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|HostAccountId |長整型 |`114333` |新增或更新主機帳戶的 ID。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://livesaas.byteplusapi.com/?Action=UpdateHostAccount&Version=2023-08-01
{
    "HostAccount": {
        "Id": 114333,
        "Name": "Host A",
        "AvatarUrl": "https://example.com/a.png",
        "IsFollowEnable": 1,
        "HomeUrl": "https://example.com",
        "ExternalPlatformId": "abc123",
        "ExtraInfo": "abc"
    },
    "GetFollowDataUrl": "https://example.com",
    "UpdateFollowDataUrl": "https://example.com"
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateHostAccount",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1715326286
    },
    "Result": {
        "HostAccountId": 114333
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

常見錯誤碼請參閱 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
