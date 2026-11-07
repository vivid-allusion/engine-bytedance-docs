---
title: "ActivityExplainProductCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activityexplainproductcallBack-zh-TW"
---

當你的直播間中的商品處於以下任一情況時，BytePlus Live 會向你的自定義 URL 發送 POST 請求，並在請求體中傳遞資訊，例如直播間的活動 ID 及商品資訊：


* 被釘選至菜單頂部，並在觀看頁面以浮窗形式展示。

* 恢復至菜單下方的原始位置，且不再於觀看頁面以浮窗形式展示。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">若已停用多商品置頂功能，請使用此回調。如需瞭解此功能的更多資訊，請參閱<a href="https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-chan-pin-ka-pian-zh-TW">管理商品卡片</a>。</div>


* <div data-tips="true" data-tips-type="tip">你必須先聯繫 BytePlus Live 的業務代表，並提供自定義 URL 以接收回調通知。</div>


* <div data-tips="true" data-tips-type="tip">若 BytePlus Live 的回調伺服器在請求發送後五秒內未收到你的伺服器回應，則請求將視為失敗。BytePlus Live 會對失敗的請求額外重試兩次，每次間隔五秒。</div>



請求範例

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...
{
     "AccountId": "3000123487",
     "ActivityId": "1823745212348678",
     "CancelExplainExternalProductId": "120056",
     "CancelExplainProductId": "500067",
     "CancelExplainProductName": "Eggs",
     "EventType": "ActivityExplainProductCallBack",
     "ExplainExternalProductId": "780012",
     "ExplainProductId": "500028",
     "ExplainProductName": "Cake",
     "RequestUuid": "ActivityExplainProductCallBack - 1823712342538389",
     "Sign": "e11de95caf53091963fc92092dce9450",
     "Timestamp": "1739273121"
}
```



|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|AccountId |String |`3000123487` |你的 BytePlus 帳戶的帳戶 ID。你可於[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)右上角點擊個人頭像取得該 ID。 |
|ActivityId |String |`1823745212348678` |直播間的活動 ID。 |
|EventType |String |`ActivityExplainProductCallBack` |回調事件類型。該值始終為`ActivityExplainProductCallBack`。 |
|Timestamp |String |`1739273121` |回調請求發送時間，Unix 時間戳格式。單位：秒。 |
|Sign |String |`e11de95caf53091963fc92092dce9450` |用於驗證的簽名。<br><br>要取得`Sign`的值，需完成以下步驟：<br><br><br>1. 依序串接 AccountSecret、AccountId、ActivityId、EventType 與 Timestamp 參數的值。請聯繫你的業務代表以取得`AccountSecret`值。<br><br>2. 對串接後的字串生成 32 位小寫 MD5 雜湊值。<br><br><br>本範例假設`AccountSecret`值為`abc`。則串接後的字串為`abc30001234871823745212348678ActivityExplainProductCallBack1739273121`，`Sign`值為`e11de95caf53091963fc92092dce9450`。 |
|ExplainProductName |String |`Cake` |被釘選至菜單頂部並在浮窗展示的商品名稱。 |
|ExplainProductId |String |`500028` |被釘選至菜單頂部並在浮窗展示的商品（商品卡片）ID。 |
|ExplainExternalProductId |String |`780012` |被釘選至菜單頂部並在浮窗展示的商品外部 ID。 |
|CancelExplainProductName |String |`Eggs` |恢復至菜單下方原始位置且不再浮窗展示的商品名稱。 |
|CancelExplainProductId |String |`500067` |恢復至菜單下方原始位置且不再浮窗展示的商品（商品卡片）ID。 |
|CancelExplainExternalProductId |String |`120056` |恢復至菜單下方原始位置且不再浮窗展示的商品外部 ID。 |
|RequestUuid |String |`ActivityExplainProductCallBack - 1823712342538389` |回調請求的唯一識別碼。 |
