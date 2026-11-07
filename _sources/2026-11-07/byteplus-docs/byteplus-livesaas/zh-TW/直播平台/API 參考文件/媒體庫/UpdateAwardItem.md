---
title: "UpdateAwardItem"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/UpdateAwardItem-zh-TW"
---

調用 `UpdateAwardItem` API，可向獎品庫新增獎品，或更新現有獎品的名稱、庫存及其他資訊。

<span id="Usage scenario"></span>
## 使用場景

通過本 API 的 `Id` 參數，可以向獎品庫新增獎品或更新現有獎品。


* **新增獎品：**  請勿在請求參數中傳入 `Id`，或將 `Id` 設為 0，即可創建新獎品。

* **更新現有獎品：**  請將待更新獎品的 ID 作為 `Id` 參數的值傳入。可通過調用 `GetAwardItemList` API 獲取獎品 ID。


<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳戶每秒最多 10 次請求

* 前置條件：需擁有 BytePlus 帳戶，或具備 **媒體庫** \> **獎品庫** \> **編輯** 權限的 IAM 使用者。如需瞭解如何新增 IAM 使用者，請參見 [管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://livesaas.byteplusapi.com/?Action=UpdateAwardItem&Version=2023\-08\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下列表格未涵蓋所有通用請求參數。完整列表請參見 [通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateAwardItem` |API 操作名稱。 |
|Version |String |是 |`2023-08-01` |本 API 操作的版本號。當前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|AwardItem |[AwardItem](https://docs.byteplus.com/en/docs/11/113730#awarditem) 物件 |是 |*  |獎品庫中的獎品列表。 |


<span id="awarditem"></span>
### AwardItem


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|AwardItemIcon |String |否 |https://www.example.com/test.png |獎品圖片的 URL（含協議）。 |
|AwardItemType |Integer |否 |1 |獎品類型。有效值如下：<br><br><br>* `1`：實物獎品<br><br>* `2`：虛擬獎品<br><br>* `3`：自定義獎品<br><br>* `4`：兌換券獎品<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">新增獎品時，此參數為必填。</div><br> |
|AwardItemName |String |否 |獎品A |獎品名稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">新增獎品時，此參數為必填。</div><br> |
|Id |Long |否 |1715\*\*\*\*1256 |獎品 ID。<br><br><br>* **新增獎品：**  請勿傳入此參數，或將其值設為 `0`。獎品庫最多可存放 10,000 個獎品。<br><br>* **更新獎品資訊：**  請傳入待更新獎品的 ID。可通過調用 [GetAwardItemList](https://docs.byteplus.com/en/docs/byteplus-livesaas/getawarditemlist) API 獲取 ID。 |
|AwardLotteryTicketAddr |String |否 |https://example.com |兌換券獎品的領取 URL。長度範圍為 1 至 256 字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數為必填，且僅當<code>AwardItemType</code>設為4時生效。</div><br> |
|AwardItemStock |Long |否 |200 |獎品庫存。取值範圍為 [1, 100000]。若值為 `-1`，表示庫存無上限。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">新增獎品時，此參數為必填。</div><br> |
|AwardItemNum |String |否 |48151841 |積分獎品的批次號。長度範圍為 1 至 256 字元。可用此批次號標識企業積分並發放給觀眾。 |
|AwardItemAmounts |Long |否 |1 |每位中獎觀眾獲得的積分數量。取值範圍為 [0,99999]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數為必填，且僅當<code>AwardItemType</code>設為3且<code>DeliveryMethod</code>設為2時生效。</div><br> |
|DeliveryMethod |Integer |否 |1 |自定義獎品的類別。取值：<br><br><br>* `1`：優惠券<br><br>* `2`：積分<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數為必填，且當<code>AwardItemType</code>設為3時生效。</div><br> |
|WinnerInfoType |Array of Integer |否 |[1,2,3] |實物或虛擬獎品中獎者需提供的資訊類型。取值：<br><br><br>* `1`：收貨地址<br><br>* `2`：手機號碼<br><br>* `3`：收件人姓名<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數為必填，且僅當<code>AwardItemType</code>設為<code>1</code>或<code>2</code>時生效。</div><br><br><br><div data-tips="true" data-tips-type="tip">當<code>AwardItemType</code>設為<code>2</code>時，此參數僅支援值<code>2</code>。</div><br> |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Status |Boolean |true |獎品是否新增或更新成功。若操作成功，回傳`true`。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateAwardItem&Version=2023-08-01
{
    "AwardItem": {
        "AwardItemIcon": "https://www.example.com/test.png",
        "AwardItemType": 1,
        "AwardItemName": "Prize",
        "Id": 1715****1256,
        "AwardLotteryTicketAddr": "https://example.com",
        "AwardItemStock": 200,
        "AwardItemNum": "48151841",
        "AwardItemAmounts": 1,
        "DeliveryMethod": 1,
        "WinnerInfoType": [
            1,
            2,
            3
        ]
    }
}
```


<span id="Sample response"></span>
### 回應範例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateAwardItem",
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

常見錯誤碼請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
