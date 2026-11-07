---
title: "GetSDKTokenAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW"
---

呼叫此 API 以取得授權令牌，該令牌用於允許觀眾透過整合 Viewer SDK 的網頁或應用程式進入直播間。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">為防止惡意攻擊，請在呼叫此 API 操作前，確保驗證所有請求參數。</div>


<span id="61e03047"></span>
## 需求

配額：每個帳戶每分鐘 5,000 次查詢

<span id="8fc08545"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=GetSDKTokenAPI&Version=2020-06-01`

* 方法：POST


<span id="06d777a9"></span>
## 請求參數

下表未包含所有共用請求參數。完整列表請參見 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="513dbfbc"></span>
### 查詢


|名稱 |資料型別 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`GetSDKTokenAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### Body


|名稱 |資料型別 |必填 |範例值 |說明 |
|---|---|---|---|---|
|ActivityId |Long |是 |`179758233282****` |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得此 ID。 |
|Mode |Integer |是 |`2` |直播間的驗證模式。<br><br>有效值：<br><br><br>* `1`：公開模式。觀眾可在未登入的情況下進入直播間。但在需要用戶資訊的場景（如點擊評論文字框或按讚評論）時，觀眾需先輸入暱稱。<br><br>* `2`：自訂模式。觀眾登入您的帳戶系統後，您必須將其暱稱與用戶 ID 傳遞給此 API 操作。觀眾將使用您的帳戶系統憑證進入直播間。因此，觀眾可直接執行發送評論、按讚評論等操作。 |
|Nickname |String |否 |`Viewer A` |觀眾的暱稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若 <code>Mode</code> 的值為 <code>2</code>，此參數為必填。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">為防止個人資訊洩漏，建議不要將電話號碼等資訊作為觀眾暱稱。</div><br> |
|UserIdStr |String |否 |`57584` |觀眾的用戶 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若 <code>Mode</code> 的值為 <code>2</code>，此參數為必填。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">為防止個人資訊洩漏，建議不要將電話號碼等資訊作為觀眾用戶 ID。</div><br> |
|InviteToken |String |否 |`abcd` |若觀眾從整合 Web Viewer SDK 的頁面分享直播間，此值為分享網址中的 `inviter_token`。例如，若路徑為 `https://test.live.com/123/456?inviter_token=abcd`，則參數值為 `abcd`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當 <code>Mode</code> 的值為 <code>2</code> 時，此參數才會生效。</div><br> |
|AvatarUrl |String |否 |`http://xxx.example` |觀眾頭像的 URL。此頭像僅在整合 Viewer SDK 的 iOS 或 Android 觀看頁面顯示。 |
|CustomComment |String |否 |`Singapore` |指定自訂資訊（如得獎者所在地），將顯示於得獎者列表中觀眾暱稱右側。此值最多可為 50 個字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅在 <code>Mode</code> 的值為 <code>2</code> 時生效。</div><br> |


<span id="f9131aea"></span>
## 回應參數


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|Token |String |`ENYVfBwV6kdV14QDnGO****teQmSYmeHiiGOJcIxdII%3D` |授權令牌，用於允許觀眾透過整合 Viewer SDK 的網頁或應用程式進入直播間。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若 <code>Mode</code> 的值為 <code>2</code>，系統會產生經 URL 編碼的權杖，且必須在傳遞給 Viewer SDK 前先進行 URL 解碼。否則，Viewer SDK 將無法驗證該權杖。</div><br> |


<span id="eebe5d33"></span>
## 範例

<span id="5e5b0957"></span>
### 請求範例

```JSON
POST https://livesaas.byteplusapi.com/?Action=GetSDKTokenAPI&Version=2020-06-01
{
     "ActivityId": 179758233282****,
     "Mode": 2,
     "Nickname": "Viewer A",
     "UserIdStr": "57584"
}
```


<span id="Sample response"></span>
### 回應範例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "GetSDKTokenAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1714572349
    },
    "Result": {
        "Token": "ENYVfBwV6kdV14QDnGO****teQmSYmeHiiGOJcIxdII%3D"
    }
}
```


<span id="6e0e0a4d"></span>
## 錯誤碼

共用錯誤碼列表請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
