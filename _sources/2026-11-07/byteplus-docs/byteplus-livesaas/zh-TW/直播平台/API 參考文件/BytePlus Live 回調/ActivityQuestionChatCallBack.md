---
title: "ActivityQuestionChatCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activityquestionchatcallback-zh-TW"
---

當用戶在問答選單下發送問題時，BytePlus Live 會向你的自訂 URL 發送一個 POST 請求，並將問題資料放在請求主體中。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">你必須先聯繫你的 BytePlus Live 銷售代表，並提供自訂 URL 以接收回調。</div>


* <div data-tips="true" data-tips-type="tip">如果你的伺服器在五秒內未回應，該請求將失敗。BytePlus Live 會以五秒為間隔，最多再重試兩次該請求。</div>



請求範例

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...

{
 "ActivityId": "172183121234",
 "EventType": "ActivityQuestionChatCallBack",
 "CreateTime": "1716795991",
 "QuestionMsgId": "5941305",
 "UserNickName": "Viewer A",
 "UserExternalId": "123874041231234",
 "Content": "Question A",
 "Sign": "5ad620fab18b8c78ab90f277aea8c562"
}
```



|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|ActivityId |String |`172183121234` |直播間的活動 ID。 |
|EventType |String |`ActivityQuestionChatCallBack` |事件類型。 |
|CreateTime |String |`1716795991` |問題發送時間，Unix 時間戳格式。單位：秒。 |
|QuestionMsgId |String |`5941305` |問題 ID。 |
|UserNickName |String |`Viewer A` |發送問題用戶的暱稱。 |
|UserExternalId |String |`123874041231234` |用戶在第三方平台上的唯一識別碼。你可以使用此 ID 在你的組織內識別用戶，以進行洞察與數據分析。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅在用戶登入直播間時才會填充。僅以暱稱加入的用戶無法取得此參數。</div><br> |
|Content |String |`Question A` |問題內容。 |
|Sign |String |`5ad620fab18b8c78ab90f277aea8c562` |用於驗證的簽名。<br><br>要計算`Sign`值，必須完成以下步驟：<br><br><br>1. 依序連接以下參數的值：`AccountSecret`、ActivityId、CreateTime、EventType、QuestionMsgId、UserExternalId 和 UserNickName。請聯繫你的銷售代表以取得`AccountSecret`值。<br><br>2. 使用 MD5 演算法（32 位元小寫）加密連接後的字串。<br><br><br>例如，若`AccountSecret`為`abc`，連接後的字串為`abc1721831212341716795991ActivityQuestionChatCallBack5941305123874041231234Viewer A`，最終產生的`Sign`值為`5ad620fab18b8c78ab90f277aea8c562`。 |
