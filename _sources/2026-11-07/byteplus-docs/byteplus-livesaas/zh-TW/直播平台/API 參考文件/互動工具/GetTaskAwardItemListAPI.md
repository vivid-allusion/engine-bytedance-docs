---
title: "GetTaskAwardItemListAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetTaskAwardItemListAPI-zh-TW"
---

獲取已在直播間發送的觀看時長抽獎獎品列表。

<span id="Requirements"></span>
## 需求


* 配額：每個帳戶每分鐘可查詢 120 次。

* 前提條件：需擁有 BytePlus 帳戶，或具備**Insights** \> **僅檢視**或**編輯**權限的 IAM 使用者。如需瞭解如何新增 IAM 使用者，請參見[管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：GET

* 端點：https://livesaas.byteplusapi.com/?Action=GetTaskAwardItemListAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下列表格未涵蓋所有通用請求參數。完整列表請參見[通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`GetTaskAwardItemListAPI` |API 操作名稱。 |
|Version |String |是 |`2020-06-01` |本 API 操作的版本號。當前版本：`2020-06-01`。 |
|ActivityId |Long |是 |1798615803\*\*\*\* |直播間的活動 ID。可透過呼叫[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)獲取 ID。 |
|PageNo |Integer |否 |1 |返回結果的頁碼。預設值：`1`。 |
|PageItemCount |Integer |否 |10 |每頁返回的結果數量。預設值：`10`。 |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|TaskAwardItemList |Array of[TaskAwardItemList](https://docs.byteplus.com/docs/byteplus-livesaas/GetTaskAwardItemListAPI-zh-TW#taskawarditemlist) |無 |觀看時長抽獎的獎品資訊列表。 |
|PageNo |Integer |1 |返回結果的頁碼。 |
|PageItemCount |Integer |10 |每頁返回的結果數量。 |
|PageTotalCount |Integer |1 |查詢結果總數。 |


<span id="taskawarditemlist"></span>
### TaskAwardItemList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|TaskAwardItemId |String |8480 |觀看時長抽獎的獎品 ID。 |
|AwardItemType |Integer |4 |獎品類型。有效值如下：<br><br><br>* `1`：實物獎品<br><br>* `2`：虛擬獎品<br><br>* `3`：自定義獎品<br><br>* `4`：兌換券獎品 |
|PeopleCount |Integer |1 |參與人數。 |
|AwardCount |Integer |1 |中獎人數。 |
|AwardItemName |String |實物獎品 |獎品名稱。 |
|AwardLotteryTicketAddr |String |https://example.com |兌換券獎品的領取網址。長度範圍為 1 至 256 個字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當<code>AwardItemType</code>設為 4 時，該參數為必填且生效。</div><br> |
|AwardStartTime |Long |1689570360 |觀看時長抽獎的開始時間。Unix 時間戳（秒）。 |
|AwardEndTime |Long |1689656640 |觀看時長抽獎的結束時間。Unix 時間戳（秒）。 |
|AwardItemNum |String |48151841 |積分獎品的批次號。長度範圍為 1 至 256 個字元。可使用此批次號標識企業積分並發放給觀眾。 |
|AwardItemAmounts |Integer |1 |每位中獎觀眾獲得的積分數量。取值範圍為 [0,99999]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當<code>AwardItemType</code>設為 3 時，該參數為必填且生效。</div><br> |
|TaskAwardIcon |String |//example\-image.image |獎品圖示的 URL，不含協議頭。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetTaskAwardItemListAPI&Version=2020-06-01&ActivityId=1798615803****&PageNo=1&PageItemCount=10
```


<span id="Sample response"></span>
### 回應範例

```JSON
{
  "ResponseMetadata": {
    "RequestId": "202301112319419CCB1169F45D1CD7A49F",
    "Action": "GetTaskAwardItemListAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "cn-north-1",
    "SystemTime": 1673450381
  },
  "Result": {
    "PageNo": 1,
    "PageItemCount": 10,
    "PageTotalCount": 1,
    "TaskAwardItemList": [
      {
        "TaskAwardItemId": "8480",
        "AwardItemType": 1,
        "PeopleCount": 1,
        "AwardCount": 0,
        "AwardItemName": "Prize A",
        "AwardLotteryTicketAddr": "",
        "AwardItemNum": "",
        "AwardItemAmounts": 0,
        "TaskAwardIcon": "//example.com/path/to/image.png",
        "AwardStartTime": 1689570360,
        "AwardEndTime": 1689656640
      }
    ]
  }
}
```


<span id="Error codes"></span>
## 錯誤碼

常見錯誤碼請參見[常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
