---
title: "ActivityAwardInfoCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ActivityAwardInfoCallBack-zh-TW"
---

當舉辦即時抽獎時，BytePlus Live 會向你的自訂 URL 發送 POST 請求，並在請求內容中傳遞直播間 ID、獎品資訊及中獎者資訊等資料。

若即時抽獎包含多個獎品，BytePlus Live 會為每個獎品分別發送回調訊息。每次回調最多可包含 2,000 名中獎者的資訊。若某個獎品的中獎者資訊超過此限制，BytePlus Live 會分多次發送回調訊息。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">你必須先聯絡 BytePlus Live 業務代表，並提供自訂 URL 以接收回調通知。</div>


* <div data-tips="true" data-tips-type="tip">若 BytePlus Live 的回調伺服器在請求發送後五秒內未收到你的伺服器回應，則請求會失敗。BytePlus Live 會以五秒間隔再重試失敗的請求兩次。</div>



請求範例

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...
{
    "AccountID": "200000****",
    "ActivityID": "182573526550****",
    "ActivityName": "Live Room A",
    "AwardItemAmounts": "",
    "AwardItemId": "10****",
    "AwardItemNum": "",
    "AwardItemType": "2",
    "AwardName": "Prize A",
    "DeliveryMethod": "",
    "EventType": "ActivityAwardInfoCallBack",
    "RequestUuid": "ActivityAwardInfoCallBack-182572318444****",
    "Sign": "c7594afe578431086bf1c56eff54****",
    "Timestamp": "1741158904",
    "UserInfos": [
        {
            "ExternalID": "78989827691****",
            "Extra": "",
            "IsPriorityUser": "0",
            "NickName": "Audience A",
            "Telephone": "1803738****",
            "UserAccessIP": "fdbd:dc0********",
            "UserAgent": "Windows 10",
            "UserID": "182137188********"
        }
    ]
}
```



|參數 |型別 |說明 |
|---|---|---|
|AccountID |String |你的 BytePlus 帳戶的帳戶 ID。你可點擊 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)右上角頭像取得該 ID。 |
|ActivityID |String |直播間的活動 ID。 |
|EventType |String |回調通知的事件類型，固定值為 `ActivityAwardInfoCallBack`。 |
|Timestamp |String |回調請求發送的時間，採 Unix timestamp 格式。單位：秒。 |
|Sign |String |驗證用的簽名。<br><br>要取得 `Sign` 的值，必須完成以下步驟：<br><br><br>1. 將對應參數值依 `AccountSecretAccountIDEventTypeTimestamp` 格式串接。請聯絡你的業務代表取得 `AccountSecret` 值。<br><br>2. 將串接後的字串以 MD5（32 位小寫）加密。<br><br><br>本範例假設 AccountSecret 值為 abc。串接後的字串為 abc30001234871823745212348678ActivityAwardInfoCallBack1739273121，Sign 值即為對應的 MD5 雜湊值。 |
|ActivityName |String |直播間名稱。 |
|AwardItemId |String |獎品 ID。 |
|RequestUuid |String |回調請求的唯一識別碼。 |
|AwardName |String |獎品名稱。 |
|AwardItemType |String |獎品類型。有效值如下：<br><br><br>* `1`：實體獎品<br><br>* `2`：虛擬獎品<br><br>* `3`：自訂獎品<br><br>* `4`：兌換券獎品 |
|DeliveryMethod |String |自訂獎品的類別。值：<br><br><br>* `1`：優惠券<br><br>* `2`：積分<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當<code>AwardItemType</code>設為 3 時，此參數生效。</div><br> |
|AwardItemNum |String |積分獎品的批次號。長度範圍為 1 到 256 字元。你可利用此批次號辨識公司積分並發放給觀眾。 |
|AwardItemAmounts |String |每位中獎觀眾獲得的積分數。值範圍為 [0,99999]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當<code>AwardItemType</code>設為 3 且<code>DeliveryMethod</code>設為 2 時，此參數生效。</div><br> |
|UserInfos |Array of[UserAwardInfo](https://docs.byteplus.com/docs/byteplus-livesaas/ActivityAwardInfoCallBack-zh-TW#e727d716) |中獎者資訊。 |


<span id="e727d716"></span>
### UserAwardInfo


|名稱 |資料型別 |說明 |
|---|---|---|
|UserId |String |使用者 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若用戶未以暱稱或其他方式登入直播間，則用戶 ID 為 <code>0</code>。</div><br> |
|ExternalID |String |使用者在第三方平台的唯一識別碼。你可利用此 ID 在組織內辨識使用者，並依需求進行用戶洞察及資料分析。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅針對通過整合身份系統驗證的用戶填充，不適用於僅以暱稱登入的訪客用戶。</div><br> |
|Extra |String |額外參數，對應觀看頁面 URL 的 extra 參數。例如，`https://live.byteplus.com/6688/322****?extra=xxx`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">使用 iOS 或 Android 的 Viewer SDK 時，此參數不會填充。</div><br> |
|NickName |String |使用者暱稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當用戶登入直播間時，此參數才會填充。</div><br> |
|UserAccessIP |String |使用者的 IP 位址。 |
|UserAgent |String |使用者所用的裝置類型。 |
|Telephone |String |使用者登入直播間時所用的手機號碼。 |
|IsPriorityUser |String |使用者是否優先中獎。有效值如下：<br><br><br>* `0`：否<br><br>* `1`：是 |
