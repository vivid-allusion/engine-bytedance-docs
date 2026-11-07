---
title: "ActivityClickReservationCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activityclickreservationcallBack-zh-TW"
---

當用戶在觀看頁面點擊**預約**以預約直播時，BytePlus Live 會向你的自定義 URL 發送 POST 請求，並在請求體中傳遞用戶資訊及直播間資訊。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">你必須先聯繫你的 BytePlus Live 業務代表，並提供自定義 URL 以接收回調通知。</div>


* <div data-tips="true" data-tips-type="tip">若 BytePlus Live 的回調伺服器在請求發送後五秒內未收到你的伺服器回應，則請求會失敗。BytePlus Live 會以五秒間隔再次重試失敗的請求兩次。</div>



請求範例

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...
{
     "AccountId": "200****914",
     "ActivityId": "1721****1234",
     "EventType": "ActivityClickReservationCallBack",
     "LiveTime": "1721099280",
     "ActivityName": "Live room A",
     "RequestUuid": "ActivityClickReservationCallBack-180469199****475",
     "ViewUrl": "https://live.byteplus.com/6688/322****",
     "Timestamp": "1721099426",
     "Sign": "b96c2ac3d6aed7557a****8bec3374fa",
     "UserInfo":{
        "ExternalId": "16057****",
        "Extra": "",
        "NickName": "Viewer A",
        "ReservationTel": "150****1345",
        "UserAccessIP": "43.*.*.143",
        "UserAgent": "Intel Mac OS X 10_15_7",
        "UserId": "17386867****4142"
                }
}
```



|名稱 |資料型別 |範例值 |描述 |
|---|---|---|---|
|AccountId |字串 |`200****914` |你的 BytePlus 帳戶 ID。你可以在 BytePlus Live 控制台右上角點擊個人頭像來查詢此 ID。 |
|ActivityId |字串 |`1721****1234` |直播間的活動 ID。 |
|EventType |字串 |`ActivityClickReservationCallBack` |事件類型。 |
|Timestamp |字串 |`1721099426` |發送回調請求的時間，Unix 時間戳格式。單位：秒。 |
|Sign |字串 |`b96c2ac3d6aed7557a****8bec3374fa` |用於驗證的簽名。<br><br>要取得`Sign`的值，必須完成以下步驟：<br><br><br>1. 依下列順序串接所需值：AccountSecret、AccountId、ActivityId、EventType 及 Timestamp。請聯繫你的業務代表以取得 AccountSecret 的值。<br><br>2. 將串接後的字串生成 32 位小寫 MD5 雜湊值。<br><br><br>本範例假設`AccountSecret`的值為`abc`。串接後的字串為`abc200****9141721****1234ActivityClickReservationCallBack1721099426`，`Sign`的值為`b96c2ac3d6aed7557a****8bec3374fa`。 |
|ActivityName |字串 |`直播間 A` |直播間名稱。 |
|ViewUrl |字串 |`https://live.byteplus.com/6688/322****` |直播間觀看頁面的 URL。 |
|LiveTime |字串 |`1721099426` |直播預定開始時間，Unix 時間戳格式。單位：秒。 |
|RequestUuid |字串 |`ActivityClickReservationCallBack-180469199****475` |回調請求的唯一識別碼。 |
|UserInfo |[UserReservationInfo](https://docs.byteplus.com/docs/byteplus-livesaas/activityclickreservationcallBack-zh-TW#30b07c7a) |`-` |點擊觀看頁面**預約**以預約直播的用戶資訊。 |


<span id="30b07c7a"></span>
### UserReservationInfo


|名稱 |資料型別 |範例值 |描述 |
|---|---|---|---|
|UserId |字串 |`17386867****4142` |用戶 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若用戶未以暱稱或其他方式登入直播間，則用戶 ID 為<code>0</code>。</div><br> |
|ExternalId |字串 |`16057****` |用戶在第三方平台上的唯一識別碼。你可以使用此 ID 在組織內識別用戶，以便進行用戶洞察及資料分析。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅針對通過整合身份系統驗證的用戶填寫，不適用於僅提供暱稱登入的訪客用戶。</div><br> |
|Extra |字串 |`abc` |你的額外參數，對應於觀看頁面地址中的 extra 參數。例如，`https://live.byteplus.com/6688/322****?extra=xxx`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">使用 iOS 或 Android Viewer SDK 時，此參數不會填寫。</div><br> |
|NickName |字串 |`觀眾 A` |用戶暱稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅在用戶登入直播間時才有值。</div><br> |
|UserAccessIP |字串 |`43.*.*.143` |用戶的 IP 位址。 |
|UserAgent |字串 |`Intel Mac OS X 10_15_7` |用戶所使用的裝置類型。 |
|ReservationTel |字串 |`150****1345` |用於預約直播的電話號碼。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當使用 iOS 或 Android 的 Viewer SDK 時，此參數不會被填入。</div><br> |
