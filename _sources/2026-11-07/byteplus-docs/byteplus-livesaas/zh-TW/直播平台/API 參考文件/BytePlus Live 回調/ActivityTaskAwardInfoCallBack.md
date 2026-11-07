---
title: "ActivityTaskAwardInfoCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ActivityTaskAwardInfoCallBack-zh-TW"
---

當用戶參與以觀看時長為基礎的抽獎活動並獲得獎品時，BytePlus Live 會向你的自定義 URL 發送 POST 請求，並在請求體中傳遞直播間 ID、獎品資訊及中獎者資訊。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">你必須先聯繫你的 BytePlus Live 業務代表，並提供自定義 URL 以接收回調通知。</div>


* <div data-tips="true" data-tips-type="tip">若 BytePlus Live 的回調伺服器在請求發送後五秒內未收到你的伺服器回應，則該請求會失敗。BytePlus Live 會以五秒間隔再次重試失敗的請求兩次。</div>


* <div data-tips="true" data-tips-type="tip">每次回調最多可包含 1,000 名中獎者的資訊。若某獎品的中獎者資訊超過此限制，BytePlus Live 會發送多條回調訊息。</div>



範例請求

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...
{
    "AccountId": "200000****",
    "ActivityId": "185304015484****",
    "ActivityName": "Live room A",
    "AwardItemAmounts": "99999",
    "AwardItemId": "17012",
    "AwardItemNum": "1323421123",
    "AwardItemType": "3",
    "AwardName": "Prize A",
    "DeliveryMethod": "2",
    "EventType": "ActivityTaskAwardInfoCallBack",
    "RequestUuid": "ActivityTaskAwardInfoCallBack-1853040247559201",
    "Sign": "5b81b108bee1e6aba81412a2e8802a3a",
    "Timestamp": "1774943600",
    "UserInfos": [
        {
            "ExternalID": "7613760946837832760",
            "Extra": "",
            "IsPriorityUser": "",
            "NickName": "User A",
            "Telephone": "185****3186",
            "UserAccessIP": "AwardItemAmounts",
            "UserAgent": "Intel Mac OS X 10_15_7",
            "UserID": "185304024682****"
        }
    ]
}
```



|參數 |類型 |說明 |
|---|---|---|
|AccountID |String |你的 BytePlus 帳戶的帳戶 ID。你可點擊 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)右上角頭像取得該 ID。 |
|ActivityId |String |直播間的活動 ID。 |
|ActivityName |String |直播間名稱。 |
|AwardItemAmounts |String |每位中獎觀眾所獲得的積分數。數值範圍為 [0,99999]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當<code>AwardItemType</code>設為3且<code>DeliveryMethod</code>設為2時，此參數才會生效。</div><br> |
|AwardItemId |String |獎品 ID。 |
|AwardItemNum |String |積分獎品的批次號。長度範圍為 1 至 256 字元。你可利用此批次號識別公司積分並分發給觀眾。 |
|AwardItemType |String |獎品類型。有效值如下：<br><br><br>* `1`: 實物獎品<br><br>* `2`: 虛擬獎品<br><br>* `3`: 自定義獎品<br><br>* `4`: 優惠券獎品 |
|AwardName |String |獎品名稱。 |
|DeliveryMethod |String |自定義獎品的類型。值：<br><br><br>* `1`: 優惠券<br><br>* `2`: 積分<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當<code>AwardItemType</code>設為3時，此參數才會生效。</div><br> |
|EventType |String |回調通知的事件類型，固定值為 `ActivityTaskAwardInfoCallBack`。 |
|RequestUuid |String |回調請求的唯一識別碼。 |
|Sign |String |驗證用的簽名。<br><br>要取得 `Sign` 的值，必須完成以下步驟：<br><br><br>1. 將對應參數值按 `AccountSecretAccountIdActivityIdEventTypeTimestamp` 格式串接。聯繫你的業務代表取得 `AccountSecret` 的值。<br><br>2. 將串接後的字串以 MD5（32 位小寫）加密。<br><br><br>本範例假設 AccountSecret 值為 abc。則串接字串為 abc30001234871823745212348678ActivityAwardInfoCallBack1739273121，Sign 值即為對應的 MD5 雜湊值。 |
|Timestamp |String |回調請求發送時間，Unix 時間戳格式。單位：秒。 |
|UserInfos |Array of[UserInfos](https://docs.byteplus.com/docs/byteplus-livesaas/ActivityTaskAwardInfoCallBack-zh-TW#fd57e72d) |中獎者資訊。 |


<span id="fd57e72d"></span>
## UserInfos


|Name |資料類型 |說明 |
|---|---|---|
|UserID |String |用戶 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">對於未登入即加入直播間的匿名用戶，使用者 ID 為<code>0</code>。</div><br> |
|ExternalID |String |用戶在第三方平台的唯一識別碼。你可利用此 ID 在組織內識別用戶，並根據需求進行用戶洞察及數據分析。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅會在透過整合身份系統驗證的用戶填入，不會在僅提供暱稱登入的訪客用戶填入。</div><br> |
|Extra |String |你的額外參數，對應觀看頁面地址中的 extra 參數。例如，`https://live.byteplus.com/6688/322****?extra=xxx`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">使用 iOS 或 Android 的 Viewer SDK 時，此參數不會填入。</div><br> |
|IsPriorityUser |String |用戶是否優先中獎。有效值如下：<br><br><br>* `0`: 否<br><br>* `1`: 是 |
|NickName |String |用戶暱稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">只有使用者登入直播間時，此參數才會有值。</div><br> |
|UserAccessIP |String |用戶的 IP 位址。 |
|UserAgent |String |用戶所使用的裝置類型。 |
|Telephone |String |預約直播所使用的電話號碼。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">使用 iOS 或 Android 的 Viewer SDK 時，此參數不會填入。</div><br> |
