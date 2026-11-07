---
title: "ActivityStatusModifyCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activitystatusmodifycallback-zh-TW"
---

當直播間狀態發生變化時，BytePlus Live 會向你的自定義 URL 發送 GET 請求，並在查詢字串中傳遞活動 ID 及新狀態。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">你必須先聯繫 BytePlus Live 業務代表，並提供自定義 URL 以接收回調。</div>


* <div data-tips="true" data-tips-type="tip">若 BytePlus Live 的回調伺服器在請求發送後五秒內未收到你的伺服器回應，則該請求視為失敗。BytePlus Live 最多會以五秒間隔重試失敗的請求兩次。</div>



請求範例

```Plain
http://abc.com/test.do?ActivityID=123&EventType=ActivityStatusModifyCallBack&Status=1&Timestamp=1582518318&Sign=xxxx
```



|參數 |資料型別 |說明 |
|---|---|---|
|ActivityID |String |直播間的活動 ID。 |
|EventType |String |ActivityStatusModifyCallBack |
|Status |String |直播間的狀態。<br><br>有效值：<br><br><br>* `1`：直播<br><br>* `2`：預覽<br><br>* `3`：回放<br><br>* `4`：結束 |
|Timestamp |String |回調請求發送的時間，Unix 時間戳格式。單位：秒。 |
|Sign |String |用於驗證的加密字串。<br><br>要獲取 `Sign` 值，必須完成以下步驟：<br><br><br>1. 將字串以 `AccountSecretActivityIDEventTypeStatusTimestamp` 格式串接。聯繫你的業務代表以取得 `AccountSecret` 值。<br><br>2. 對串接後的字串生成 32 字元的小寫 MD5 雜湊值。<br><br><br>本範例假設 `AccountSecret` 值為 `abc`。則串接後的字串為 `abc123ActivityStatusModifyCallBack11582518318`，最終產生的 `Sign` 值為 `3d5fc13702c89c3c34c811ba8ac8fbbc`。 |
