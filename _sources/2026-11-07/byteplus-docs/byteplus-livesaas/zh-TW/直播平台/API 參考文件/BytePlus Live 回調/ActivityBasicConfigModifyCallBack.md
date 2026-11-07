---
title: "ActivityBasicConfigModifyCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activitybasicconfigmodifycallback-zh-TW"
---

當直播間的基本配置發生變更時，BytePlus Live 會向你的自定義 URL 發送 POST 請求，並在請求體中傳遞活動 ID 及基本配置。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">你必須先聯繫你的 BytePlus Live 業務代表，並提供自定義 URL 以接收回調。</div>


* <div data-tips="true" data-tips-type="tip">若 BytePlus Live 的回調伺服器在請求發送後五秒內未收到你的伺服器回應，則該請求視為失敗。BytePlus Live 會對失敗的請求額外重試兩次，每次間隔五秒。</div>



請求範例

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...

{
 "ActivityID": "123",
 "EventType": "ActivityBasicConfigModifyCallBack",
 "Timestamp": "1582518318",
 "Sign": "xxxx",
 "Name": "Live Room A",
 "Announcement": "Live Room A",
 "CoverImage": "//gjr78lqtd0-image.image",
 "ViewUrl": "https://live.byteplus.com/7420/1234",
 "LiveTime": "1583070536"
}
```



|參數 |資料型別 |說明 |
|---|---|---|
|ActivityID |String |直播間的活動 ID。 |
|EventType |String |ActivityBasicConfigModifyCallBack |
|Timestamp |String |回調請求的時間戳，採用 Unix 格式。單位：秒。 |
|Sign |String |用於驗證的加密字串。<br><br>要取得 `Sign` 值，必須完成以下步驟：<br><br><br>1. 將字串按照 `AccountSecretActivityIDAnnouncementCoverImageEventTypeLiveTimeNameTimestampViewUrl` 格式串接。聯繫你的業務代表以取得 `AccountSecret` 值。<br><br>2. 對串接後的字串生成 32 字元的小寫 MD5 雜湊值。<br><br><br>本範例假設 `AccountSecret` 值為 `abc`。串接後的字串為 `abc123Live Room A//gjr78lqtd0-image.imageActivityBasicConfigModifyCallBack1583070536Live Room A1582518318 https://live.byteplus.com/7420/1234`，生成的 `Sign` 值為 `85c1ba868bf4e30b6055ccfbbdd7bc3a`。 |
|Name |String |直播間名稱。 |
|Announcement |String |直播間描述。 |
|CoverImage |String |直播間封面圖片的 URL。 |
|ViewUrl |String |直播間觀看頁面的 URL。 |
|LiveTime |String |直播開始時間，採用 Unix 時間戳格式。單位：秒。<br><br>此時間可能無法反映直播實際開始時間。 |
