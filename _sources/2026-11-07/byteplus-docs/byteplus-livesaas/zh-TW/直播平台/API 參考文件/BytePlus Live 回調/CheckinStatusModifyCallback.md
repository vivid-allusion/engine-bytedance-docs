---
title: "CheckinStatusModifyCallback"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/CheckinStatusModifyCallback-zh-TW"
---

當發生簽到事件（如簽到創建、刪除、發送或截止時間到達）時，BytePlus Live 會向你的自定義 URL 發送 POST 請求，並在請求正文中傳遞直播間 ID 及更新後的簽到狀態。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">你必須先聯繫 BytePlus Live 的銷售代表，並提供自定義 URL 以接收回調通知。</div>


* <div data-tips="true" data-tips-type="tip">若 BytePlus Live 的回調伺服器在請求發送後五秒內未收到你的伺服器回應，則請求視為失敗。BytePlus Live 會以五秒為間隔，對失敗的請求再重試兩次。</div>



請求範例

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...
{
    "ActivityId": "1840847565136997",
    "CheckInId": "checkIn1853040247525505",
    "EventType": "CheckinStatusModifyCallback",
    "RequestUuid": "CheckinStatusModifyCallback-1853040247354881",
    "Sign": "c26ca0fe5c09f56222d22e9525bd3739",
    "Status": "Init",
    "SubAccountName": "admin@example.com",
    "Timestamp": "1774933967"
}
```



|名稱 |資料型別 |說明 |
|---|---|---|
|ActivityId |String |直播間的活動 ID。 |
|CheckInId |String |簽到 ID。 |
|EventType |String |回調通知的事件類型，固定值為 `CheckinStatusModifyCallback`。 |
|RequestUuid |String |回調請求的唯一標識符。 |
|Sign |String |用於驗證的簽名。<br><br>要獲取 `Sign` 的值，需完成以下步驟：<br><br><br>1. 將字串按 `AccountSecretActivityIdCheckInIdEventTypeStatusTimestamp` 格式拼接。聯繫你的銷售代表以獲取 `AccountSecret` 的值。<br><br>2. 使用 MD5（32 位小寫）對拼接後的字串進行雜湊。 |
|Status |String |簽到狀態。有效值如下：<br><br><br>* `Init`：已創建<br><br>* `Export`：已發送<br><br>* `Deadline`：已結束<br><br>* `Delete`：已刪除<br><br>* `Retract`：已撤回 |
|SubAccountName |String |用於創建直播間的帳號。參數值 `admin@bytedance.com` 表示該直播間由 BytePlus 帳號創建。 |
|Timestamp |String |回調請求發送的時間，Unix 時間戳格式。單位：秒。 |
