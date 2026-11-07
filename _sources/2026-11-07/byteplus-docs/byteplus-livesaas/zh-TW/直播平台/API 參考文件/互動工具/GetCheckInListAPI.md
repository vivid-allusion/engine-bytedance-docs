---
title: "GetCheckInListAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetCheckInListAPI-zh-TW"
---

呼叫 `GetCheckInListAPI` API 以取得指定直播間的所有簽到或指定簽到資訊，包括簽到 ID、參與人數、簽到時長等。

<span id="Requirements"></span>
## 需求


* 配額：每個帳戶每分鐘最多 120 次查詢。

* 前提條件：需有 BytePlus 帳戶，或具備 **Insights** \> **View only** 或 **Edit** 權限的 IAM 使用者。如需新增 IAM 使用者的詳細資訊，請參閱 [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：GET

* 端點：https://livesaas.byteplusapi.com/?Action=GetCheckInListAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下表未包含所有通用請求參數。完整列表請參閱 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`GetCheckInListAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |Long |是 |17218346\*\*\*\* |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得 ID。 |
|PageNo |Integer |否 |1 |要返回的頁碼。預設值：`1`。 |
|PageCount |Integer |否 |10 |每頁返回的結果數量。預設值：`10`。 |
|CheckInId |String |否 |checkIn1754478641140736 |簽到 ID。 |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|CheckInList |Array of[CheckInList](https://docs.byteplus.com/docs/byteplus-livesaas/GetCheckInListAPI-zh-TW#checkinlist) |`-` |簽到資訊列表。 |
|PageNo |Integer |`1` |返回結果的頁碼。 |
|PageCount |Integer |`10` |每頁返回的結果數量。 |


<span id="checkinlist"></span>
### CheckInList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|CheckInId |String |`checkIn1754478641140736` |簽到 ID。 |
|CheckInName |String |開始簽到 |簽到標題。 |
|CheckInCount |Integer |`0` |簽到參與人數。 |
|Deadline |Long |`1` |簽到時長（分鐘）。 |
|Status |String |`Deadline` |簽到狀態。有效值如下：<br><br><br>* `Init`：已建立<br><br>* `Export`：已發送<br><br>* `Deadline`：已結束<br><br>* `Delete`：已刪除<br><br>* `Retract`：已撤回 |
|ActivityId |Long |`175450930238536` |直播間 ID。 |
|NeedPersonInfo |Integer |`0` |是否需要簽到資訊。有效值如下：<br><br><br>* `0`：不需要<br><br>* `1`：需要 |
|OpenCheckTime |Integer |`1673202771` |簽到結束時間（截止時間）。此為以秒為單位的 Unix 時間戳。 |
|CheckInInfo |String |簽到 |簽到提示文字 |
|StartTime |String |`1673202711` |簽到開始時間。Unix 時間戳，以秒為單位。 |
|IsSendComment |Integer |`1` |是否在簽到後發送評論。有效值如下：<br><br><br>* `0`：不發送<br><br>* `1`：發送 |
|CommentContent |String |#用戶暱稱# 已簽到 |簽到後發送的評論內容。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅在 <code>IsSendComment</code> 設為 <code>1</code> 時生效</div><br> |
|DeadlineSecond |Integer |31 |簽到時長的秒數部分。 |
|CannotWathcLiveWhenNotCheckIn |Integer |1 |是否未及時簽到的觀眾會被移出直播間。有效值如下：<br><br><br>* `0`：不移除。<br><br>* `1`：移除。 |
|SendType |Integer |1 |簽到發送方式。有效值如下：<br><br><br>* `0`：手動發送<br><br>* `1`：定時發送 |
|AutoSendTime |Long |1723455354 |定時發送時間。Unix 時間戳，以秒為單位。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅在<code>SendType</code>被設為<code>1</code>時有效。</div><br> |
|CannotWatchLivePrompt |String |因長時間未簽到，觀看已被暫停 |移除用戶時發送的通知訊息。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅在<code>CannotWathcLiveWhenNotCheckIn</code>被設為<code>1</code>時生效。</div><br> |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetCheckInListAPI&Version=2020-06-01&ActivityId=17218346****&PageNo=1&PageCount=10&CheckInId=checkIn1754478641140736
```


<span id="Sample response"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetCheckInListAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "CheckInList": [
            {
                "CheckInId": "checkIn1754478641140736",
                "CheckInName": "Start check-in",
                "CheckInCount": 0,
                "Deadline": 1,
                "Status": "Deadline",
                "ActivityId": 175450930238****,
                "NeedPersonInfo": 0,
                "OpenCheckTime": 1673202771,
                "CheckInInfo": "Check in",
                "StartTime": "1673202711",
                "CommentContent": "#User nickname# has checked in",
                "IsSendComment": 1,
                "AutoSendTime": 1723455354,
                "CannotWathcLiveWhenNotCheckIn": 1,
                "DeadlineSecond": 31,
                "SendType": 1,
                "CannotWatchLivePrompt": "Viewing has been suspended due to prolonged failure to check in"
            }
        ],
        "PageNo": 1,
        "PageCount": 10
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

常見錯誤碼列表請參閱 [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
