---
title: "GetActivityQualityDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivityqualitydataapi-zh-TW"
---

呼叫此 API 以取得指定直播間在特定時間範圍內的直播品質數據。API 會回傳關鍵績效指標，例如拉流成功率、每 100 秒卡頓時間，以及首幀平均時間。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">請注意，目前僅支援已整合 iOS 或 Android Viewer SDK 的應用程式之數據。</div>


<span id="e2298f63"></span>
## 需求條件


* 配額：每個帳戶每分鐘最多 120 次查詢

* 前置條件：需有 BytePlus 帳戶，或具備 Insights \> 檢視權限或編輯權限的 IAM 使用者。如需更多資訊，請參閱 [管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="7e4ac041"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=GetActivityQualityDataAPI&Version=2023-08-01`

* 方法：GET


<span id="ff444339"></span>
## 請求參數

下表未包含所有共用請求參數。完整列表請參閱 [共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。

<span id="ef12448c"></span>
### **查詢**


|**名稱** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`GetActivityQualityDataAPI` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。目前版本：`2023-08-01`。 |
|BeginTime |Long |是 |`1702263015` |查詢時間範圍的起始時間，Unix 時間戳格式。單位：秒。 |
|EndTime |Long |是 |`1702264015` |查詢時間範圍的結束時間，Unix 時間戳格式。單位：秒。 |
|ActivityId |Long |是 |`17218346****` |直播間的 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得 ID。 |


<span id="f6c01293"></span>
## **回應參數**


|**名稱** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|ActivityData |Object of[ActivityData](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityqualitydataapi-zh-TW#ActivityData) |`-` |指定時間範圍內直播間的直播品質數據。 |


<span id="2f22f87b"></span>
### ActivityData


|**名稱** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|PullSuccessRate |Double |`100` |拉流成功率，表示直播期間觀眾裝置成功播放流的百分比。可利用此指標衡量觀眾能否成功拉取直播流的機率。<br><br>計算方式：拉流成功率 = 直播間成功播放總次數 / 直播間播放總次數 x 100% |
|StallTimePer100Sec |Double |`0` |每 100 秒播放期間的平均影片卡頓（凍結）時長。單位：秒。<br><br>可利用此指標衡量觀眾觀看直播影片時的卡頓嚴重程度。<br><br>計算方式：100 秒內影片卡頓時長 = 直播間所有觀眾播放期間的總卡頓時長 / 直播間所有觀眾的總播放時長 x 100<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當渲染的視訊畫面與前一個渲染畫面之間的時間間隔超過 200 毫秒時，該間隔會被計入視訊凍結的持續時間。持續監控並優化此指標可提升播放流暢度並改善用戶體驗。</div><br> |
|FirstFrameTime |Double |`0` |觀眾啟動播放器到顯示首個影片畫面的平均時間。單位：毫秒。<br><br>可利用此指標衡量觀眾開始觀看直播影片時所需等待的時間。<br><br>計算方式：<br><br><br>* 單一觀眾首幀時間 = 首幀顯示時間戳 \- 播放器啟動時間戳<br><br>* 平均首幀時間 = 直播間所有觀眾的首幀總時長 / 直播間觀眾總人數 |


<span id="b6cee885"></span>
## 範例

<span id="46cbe5cf"></span>
### 範例請求

```JSON
Get https://livesaas.byteplusapi.com/?Action=GetActivityQualityDataAPI&Version=2023-08-01&BeginTime=1702263015&EndTime=1702264015&ActivityId=17218346****
```


<span id="94c93aa4"></span>
### **範例回應**

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "GetActivityQualityDataAPI", 
        "Version": "2023-08-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1703347287 
    }, 
    "Result": {
        "ActivityData": {
            "PullSuccessRate": 100,
            "StallTimePer100Sec": 0,
            "FirstFrameTime": 0
        }
    }
}
```


<span id="34b6ffdc"></span>
## 錯誤碼

共用錯誤碼列表請參閱 [共用錯誤與狀態碼](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。


|**名稱** |**訊息** |**解決方案** |
|---|---|---|
|100000 |內部錯誤。 |請聯絡技術支援尋求協助。 |
|100001 |指定的參數 ActivityId 無效。 |請更改 `ActivityId` 的值。 |
|100005 |指定的參數 BeginTime 無效。 |請更改 `BeginTime` 的值。 |
|100005 |EndTime 不可等於或早於 BeginTime。 |請更改 `EndTime` 的值。 |
|100005 |BeginTime 與 EndTime 之間的時間間隔不得少於 1 分鐘。 |請檢查並更改 `BeginTime` 和 `EndTime` 的值。 |
|100005 |BeginTime 與 EndTime 之間的時間間隔不得超過 365 天。 |請檢查並更改 `BeginTime` 和 `EndTime` 的值。 |
|100005 |BeginTime 與 EndTime 之間的時間間隔不可設定為超過 365 天前。 |請檢查並更改 `BeginTime` 和 `EndTime` 的值。 |
