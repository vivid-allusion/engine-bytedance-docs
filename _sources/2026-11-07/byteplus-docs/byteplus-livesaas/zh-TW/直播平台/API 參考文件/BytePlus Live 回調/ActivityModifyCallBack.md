---
title: "ActivityModifyCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activitymodifycallBack-zh-TW"
---

當直播間被建立或刪除時，BytePlus Live 會向你的自定義 URL 發送 GET 請求，並在查詢字串中傳遞活動 ID 及對直播間執行的操作。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">你必須先聯繫你的 BytePlus Live 業務代表，並提供自定義 URL 以接收回調。</div>


* <div data-tips="true" data-tips-type="tip">若你的伺服器在五秒內未回應，請求將會失敗。BytePlus Live 會以五秒間隔再重試該請求兩次。</div>



請求範例

```Plain
http://abc.com/test.do?ActivityID=123&EventType=ActivityModifyCallBack&Type=1&Timestamp=1582518318&Sign=xxxx
```



|參數 |資料型別 |說明 |
|---|---|---|
|ActivityID |String |直播間的活動 ID。 |
|EventType |String |ActivityModifyCallBack |
|Timestamp |String |回調請求發送的時間，以 Unix 秒級時間戳表示。 |
|Type |String |表示直播間是被建立還是被刪除。<br><br>有效值：<br><br><br>* `1`：建立<br><br>* `2`：刪除 |
|Sign |String |用於驗證的加密字串。<br><br>要取得 `Sign` 值，必須完成以下步驟：<br><br><br>1. 以 `AccountSecretActivityIDEventTypeStatusTimestamp` 格式串接字串。聯繫你的業務代表以取得 `AccountSecret` 值。<br><br>2. 將串接後的字串生成 32 字元的小寫 MD5 雜湊值。<br><br><br>本範例假設 `AccountSecret` 值為 `abc`。串接後的字串即為 `abc123ActivityModifyCallBack11582518318`，產生的 `Sign` 值為 `3d5fc13702c89c3c34c811ba8ac8fbbc`。 |
