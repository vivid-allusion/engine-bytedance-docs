---
title: "ListAwardConfigsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ListAwardConfigs-zh-TW"
---

呼叫 `ListAwardConfigsAPI` 以取得抽獎活動的配置詳細資訊。

<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳戶每秒最多 10 次請求

* 前置條件：需有 BytePlus 帳戶，或擁有 **Live control** \> **View only** 或 **Edit** 權限的 IAM 使用者。如需更多關於新增 IAM 使用者的資訊，請參閱 [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：GET

* 端點：https://livesaas.byteplusapi.com/?Action=ListAwardConfigsAPI&Version=2023\-08\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下表並未包含所有通用請求參數。完整列表請參閱 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ListAwardConfigsAPI` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。目前版本：`2023-08-01`。 |
|ActivityId |Long |是 |17218346\*\*\*\* |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得此 ID。 |
|All |Integer |是 |1 |指定是否查詢直播間內所有即時抽獎配置。預設值為 `0`。有效值如下：<br><br><br>* `0`：僅查詢已發送的抽獎配置<br><br>* `1`：查詢直播間內所有抽獎配置 |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|AwardConfigs |Array of[AwardConfigs](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs-zh-TW#awardconfigs) |`-` |即時抽獎配置資訊列表。 |


<span id="awardconfigs"></span>
### AwardConfigs


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Id |Long |`36576` |即時抽獎 ID。 |
|ActivityId |Long |17218346\*\*\*\* |直播間 ID。 |
|Name |String |Lucky draw |抽獎名稱。 |
|AwardType |Integer |1 |抽獎方式。有效值如下：<br><br><br>* `1`：自動抽獎<br><br>* `2`：手動抽獎 |
|DeadLine |Long |`1` |抽獎倒數剩餘分鐘數。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當<code>AwardType</code>的值為<code>1</code>時，此參數才有效。</div><br> |
|BarragePwd |String |comment |抽獎彈幕留言密碼。 |
|Status |Integer |`4` |抽獎狀態。有效值如下：<br><br><br>* `1`：未發送<br><br>* `2`：進行中<br><br>* `4`：已完成<br><br>* `5`：已刪除<br><br>* `7`：已撤回<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如需查詢未發送的幸運抽獎資訊，請將<code>All</code>參數設為<code>1</code>。</div><br> |
|WinnerCount |Integer |1 |本次獎項的中獎人數。 |
|ParticipantCount |Integer |`5` |參與人數。 |
|SendTime |Integer |`1673199096` |抽獎發送時間，Unix 時間戳（秒）。 |
|OpenAwardTime |Integer |`1673199158` |抽獎結果公布時間，Unix 時間戳（秒）。 |
|AwardNum |Integer |`1` |獎品總數。 |
|RangeStatus |Integer |0 |抽獎規則。有效值如下：<br><br><br>* `0`：所有觀眾中獎機率相同。<br><br>* `1`：未中獎觀眾優先。 |
|ShowPeopleNumber |Integer |0 |是否在觀看頁面顯示抽獎實際參與人數。有效值如下：<br><br><br>* `0`：顯示<br><br>* `1`：不顯示 |
|MsgIds |String |`155681` |透過控制台發送抽獎的圖文訊息 ID。 |
|AwardCondition |Object of[AwardCondition](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs-zh-TW#awardcondition) |`-` |參與抽獎的條件 |
|ShowWinnerComment |Integer |`0` |是否顯示抽獎中獎者詳細資訊。<br><br><br>* `0`：不顯示<br><br>* `1`：顯示 |
|AwardItemInfo |Array of[AwardItemInfo](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs-zh-TW#awarditeminfo) |`-` |獎品資訊。 |


<span id="awardcondition"></span>
### AwardCondition


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Quiz |String |all |設定用戶參與抽獎的問答條件。若未設定此參數（預設），則該條件將被停用。<br><br><br>* `「all」`：用戶必須在抽獎前，於直播期間回答**所有**發送的問題。<br><br>* `1`\-`999`：用戶必須提交**至少**此數量的答案才符合資格。例如，若值為`3`，則用戶需回答至少三個問題。 |
|RightQuiz |String |1 |用戶必須正確回答的最少問題數。若未設定此參數（預設），則該條件將被停用。<br><br><br>* `「all」`：用戶必須在抽獎前，於直播期間正確回答**所有**發送的問題。<br><br>* `1`\-`999`：用戶必須正確回答**至少**此數量的問題才符合資格。例如，若值為`3`，則用戶需正確回答至少三個問題。 |
|Questionnaire |String |1 |用戶必須提交的最少問卷數。若未設定此參數（預設），則該條件將被停用。<br><br><br>* `「all」`：用戶必須在抽獎前，於直播期間提交**所有**發送的問卷。<br><br>* `1`\-`999`：用戶必須提交**至少**此數量的問卷才符合資格。例如，若值為`3`，則用戶需提交至少三份問卷。 |
|CheckIn |String |all |用戶必須完成的最少簽到次數。若未設定此參數（預設），則該條件將被停用。<br><br><br>* `「all」`：用戶必須在抽獎前，於直播期間完成**所有**發送的簽到。<br><br>* `1`\-`999`：用戶必須完成**至少**此數量的簽到才符合資格。例如，若值為`3`，則用戶需完成至少三次簽到。 |
|Vote |String |1 |用戶必須提交的最少投票數。若未設定此參數（預設），則該條件將被停用。<br><br><br>* `「all」`：用戶必須在抽獎前，於直播期間提交**所有**發送的投票。<br><br>* `1`\-`999`：用戶必須提交**至少**此數量的投票才符合資格。例如，若值為`3`，則用戶需提交至少三次投票。 |


<span id="awarditeminfo"></span>
### AwardItemInfo


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|AwardItemId |Long |`908` |獎品 ID。 |
|AwardItemName |String |獎品券 |獎品名稱。 |
|AwardItemCount |Long |`1000` |獎品數量。 |
|AwardItemType |Integer |`4` |獎品類型。有效值如下：<br><br><br>* `1`：實體獎品<br><br>* `2`：虛擬獎品<br><br>* `3`：自定義獎品<br><br>* `4`：券類獎品 |
|AwardItemIcon |String |`//p.org/04ae0f42a3a04e7387e5f6fe7a18c4fb~tplv-6ed59yyum2-image.image` |獎品圖示的 URL，不含協議。 |
|AwardItemNum |String |48151841 |積分獎品批次號。長度範圍為 1 至 256 字元。可使用此批次號識別企業積分並發放給觀眾。 |
|AwardItemAmounts |Long |1 |每位中獎觀眾獲得的積分數。數值範圍為 [0,99999]。 |
|AwardLotteryTicketAddr |String |https://example.com |券類獎品的領取 URL。長度範圍為 1 至 256 字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數為必填項，僅當<code>AwardItemType</code>設為4時適用。</div><br> |
|WinnerInfoType |String |[1,2,3] |實體或虛擬獎品中獎者需提供的資訊類型。值：<br><br><br>* `1`：收貨地址<br><br>* `2`：電話號碼<br><br>* `3`：收件人姓名 |
|WinnerCount |Long |1 |當前獎項的中獎人數。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListAwardConfigsAPI&Version=2023-08-01&ActivityId=17218346****&All=1
```


<span id="Sample response"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListAwardConfigsAPI",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "AwardConfigs": [
            {
                "Name": "Lucky draw",
                "AwardType": 1,
                "DeadLine": 1,
                "BarragePwd": "comment",
                "Status": 4,
                "ActivityId": 17218346****,
                "SendTime": 1673199096,
                "OpenAwardTime": 1673199158,
                "RangeStatus": 0,
                "ShowPeopleNumber": 0,
                "MsgIds": "155681",
                "AwardCondition": {
                    "Quiz": "all",
                    "RightQuiz": "1",
                    "Questionnaire": "1",
                    "CheckIn": "all",
                    "Vote": "1"
                },
                "Id": 36576,
                "WinnerCount": 1,
                "ParticipantCount": 5,
                "ShowWinnerComment": 0,
                "AwardItemInfo": [
                    {
                        "AwardItemId": 908,
                        "AwardItemName": "Prize coupon",
                        "AwardItemCount": 1000,
                        "AwardItemType": 4,
                        "WinnerCount": 1,
                        "AwardItemIcon": "//p.org/04ae0f42a3a04e7387e5f6fe7a18c4fb~tplv-6ed59yyum2-image.image",
                        "AwardLotteryTicketAddr": "https://example.com",
                        "WinnerInfoType": "[1,2,3]",
                        "AwardItemNum": "48151841",
                        "AwardItemAmounts": 1
                    }
                ],
                "AwardNum": 1,
                "AwardSendTime": 1726734970,
                "AwardSendType": 1
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

常見錯誤碼列表請參閱 [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
