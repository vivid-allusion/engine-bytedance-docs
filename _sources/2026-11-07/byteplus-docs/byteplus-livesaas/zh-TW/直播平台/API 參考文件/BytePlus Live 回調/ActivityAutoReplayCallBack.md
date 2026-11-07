---
title: "ActivityAutoReplayCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activityautoreplaycallback-zh-TW"
---

當一個影片被生成為直播間的回放時，BytePlus Live 會向你的自定義 URL 發送 POST 請求，並在請求體中傳遞活動 ID 與影片 ID。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">你必須先聯繫你的 BytePlus Live 業務代表，並提供自定義 URL 以接收回調。</div>


* <div data-tips="true" data-tips-type="tip">若 BytePlus Live 的回調伺服器在五秒內未收到你的伺服器回應，該請求將會逾時。BytePlus Live 會以五秒間隔再重試失敗的請求兩次。</div>



範例請求

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...

{
 "ActivityID": "123",
 "EventType": "ActivityAutoReplayCallBack",
 "Sign": "xxxx",
 "Timestamp": "1582518318",
 "LiveStartTime": "1751520600",
 "LiveEndTime": "1751526000",
 "Vid": "v0c251g7007abc1"
}
```



|參數 |資料型別 |說明 |
|---|---|---|
|ActivityID |String |直播間的活動 ID。 |
|EventType |String |ActivityAutoReplayCallBack |
|Vid |String |生成影片的 ID。 |
|Timestamp |String |回調請求發送的時間，採用 Unix 時間戳格式。單位：秒。 |
|LiveStartTime |String |對應回放影片的直播開始時間，採用 Unix 時間戳格式。單位：秒。<br><br>例如，若直播於 2025\-07\-03 13:30:00 開始，並於 2025\-07\-03 15:00:00 結束，此參數的值為 `1751520600`。 |
|LiveEndTime |String |對應回放影片的直播結束時間，採用 Unix 時間戳格式。單位：秒。<br><br>例如，若直播於 2025\-07\-03 13:30:00 開始，並於 2025\-07\-03 15:00:00 結束，此參數的值為 `1751526000`。 |
|Sign |String |用於驗證的加密字串。<br><br>要取得 `Sign` 值，必須完成以下步驟：<br><br><br>1. 將 `AccountSecret`、`ActivityID`、`Timestamp` 與 `Vid` 的值串接為一個字串。請聯繫你的業務代表以取得 AccountSecret 值。<br><br>2. 使用 MD5 演算法（32 位小寫）加密串接後的字串。<br><br><br>例如，若 `AccountSecret` 為 abc，串接後的字串為 `abc1231582518318v0c251g7007abc1`，最終產生的 `Sign` 值為 `884c08f1458e39888fb9ba4f51406c7a`。 |
