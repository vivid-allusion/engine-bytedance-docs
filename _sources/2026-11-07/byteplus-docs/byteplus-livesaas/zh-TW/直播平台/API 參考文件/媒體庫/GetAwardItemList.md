---
title: "GetAwardItemList"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetAwardItemList-zh-TW"
---

調用 `GetAwardItemList` API 以獲取當前帳戶獎品庫中的獎品清單，包括獎品名稱、庫存、圖片及其他資訊。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">以 IAM 使用者調用本 API 時，僅能獲取該 IAM 使用者可存取或可編輯的獎品資訊。如需瞭解如何設定 IAM 使用者的用戶範圍與分類範圍，請參閱 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles">管理使用者、組織與角色</a>。</div>


<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳戶每秒最多 10 次請求

* 前置條件：需擁有 BytePlus 帳戶，或具備 **媒體庫** \> **獎品庫** \> **編輯** 或 **僅檢視** 權限的 IAM 使用者。如需瞭解如何新增 IAM 使用者，請參閱 [管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：GET

* 端點：https://livesaas.byteplusapi.com/?Action=GetAwardItemList&Version=2023\-08\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下列表格未涵蓋所有通用請求參數。完整清單請參閱 [通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`GetAwardItemList` |API 操作名稱。 |
|Version |String |是 |`2023-08-01` |本 API 操作的版本。當前版本：`2023-08-01`。 |
|Name |String |否 |Prize A |獎品名稱。支援模糊搜尋，且不區分大小寫。<br><br>例如，若參數設為 **A**，則會返回 **Prize A**、**Prize abc** 等獎品。 |
|PageNumber |Integer |否 |1 |要返回的頁碼。預設值：`1`。值必須大於或等於 1。 |
|PageSize |Integer |否 |200 |每頁返回的結果數量。預設值：`200`。取值範圍為 [1,1000]。 |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|AwardItemList |[AwardItemList](https://docs.byteplus.com/en/docs/11/113735#awarditemlist) 陣列 |*  |獎品庫中的獎品清單。 |
|TotalCount |Long |1 |查詢結果總數。 |


<span id="awarditemlist"></span>
### AwardItemList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|AwardItemIcon |String |https://www.example.com/test.png |獎品圖片的 URL（含協議）。 |
|AwardItemType |Integer |1 |獎品類型。有效值包括：<br><br><br>* `1`：實物獎品<br><br>* `2`：虛擬獎品<br><br>* `3`：自訂獎品<br><br>* `4`：兌換券獎品 |
|AwardItemName |String |Prize A |獎品名稱。 |
|Id |Long |1715\*\*\*\*1256 |獎品 ID。獲取獎品 ID 後，可調用 [UpdateAwardItem](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateawarditem) API 更新獎品資訊，或調用 [DeleteAwardItem](https://docs.byteplus.com/en/docs/byteplus-livesaas/deleteawarditem) API 刪除該獎品。 |
|AwardLotteryTicketAddr |String |https://example.com |抽獎券獎品的領取 URL。 |
|AwardItemStock |Long |200 |獎品庫存。值為 `-1` 表示不限庫存。 |
|AwardItemNum |String |48151841 |積分獎品的批次號。可使用此批次號標識企業積分並發放給觀眾。 |
|AwardItemAmounts |Long |1 |每位中獎觀眾獲得的積分數量。僅當 `DeliveryMethod` 為 2 時有效。 |
|DeliveryMethod |Integer |1 |自訂獎品的類別。僅當 `AwardItemType` 為 3 時有效。取值：<br><br><br>* `1`：優惠券<br><br>* `2`：積分 |
|WinnerInfoType |Integer 陣列 |[1,2,3] |實物或虛擬獎品中獎者需提供的資訊類型。取值：<br><br><br>* `1`：收貨地址<br><br>* `2`：電話號碼<br><br>* `3`：收件人姓名 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetAwardItemList&Version=2023-08-01&Name=Prize A&PageNumber=1&PageSize=200
```


<span id="Sample response"></span>
### 回應範例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetAwardItemList",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "cn-north-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "AwardItemList": [
            {
                "AwardItemIcon": "https://www.example.com/test.png",
                "AwardItemType": 1,
                "AwardItemName": "Prize A",
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
        ],
        "TotalCount": 1
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

常見錯誤碼請參閱 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
