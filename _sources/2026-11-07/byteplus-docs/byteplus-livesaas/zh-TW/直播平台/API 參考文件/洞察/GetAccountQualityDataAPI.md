---
title: "GetAccountQualityDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getaccountqualitydataapi-zh-TW"
---

呼叫此 API 以獲取指定時間範圍內，您 BytePlus 帳戶下所有直播間的直播品質數據。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">請注意，目前僅能獲取已整合 iOS/Android Viewer SDK 的應用程式數據。</div>


<span id="a5fecde7"></span>
## 需求


* 配額：每個帳戶每分鐘最多 120 次查詢

* 前置條件：需有 BytePlus 帳戶或具備超級管理員角色的 IAM 使用者。如需更多資訊，請參閱 [管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-shi-yong-zhe-zu-zhi-yu-jue-se-zh-TW)。


<span id="57b1847f"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=GetAccountQualityDataAPI&Version=2023-08-01`

* 方法：GET


<span id="0659ac9b"></span>
## 請求參數

下表未包含所有共用請求參數。完整列表請參閱 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="21812e6d"></span>
### 查詢


|名稱 |資料型別 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`GetAccountQualityDataAPI` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。目前版本：`2023-08-01`。 |
|BeginTime |Long |是 |`1702263015` |查詢時間範圍的起始時間，Unix 時間戳格式。單位：秒。 |
|EndTime |Long |是 |`1702264015` |查詢時間範圍的結束時間，Unix 時間戳格式。單位：秒。 |


<span id="154a269b"></span>
## 回應參數


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|AccountData |Object of[AccountData](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccountqualitydataapi-zh-TW#638706eb) |`-` |指定時間範圍內，您 BytePlus 帳戶下所有直播間的直播品質數據。 |


<span id="638706eb"></span>
### AccountData


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|PullSuccessRate |Double |`100` |拉流成功率。此指標為觀眾設備上成功播放直播流的百分比。此指標衡量觀眾成功拉取直播流的機率。<br><br>計算方式：拉流成功率 =（所有直播間的成功播放總次數 / 所有直播間的播放嘗試總次數）\* 100% |
|StallTimePer100Sec |Double |`0` |每 100 秒卡頓時間。此指標表示直播流播放過程中，每 100 秒播放時間的視頻卡頓時長。單位：秒。<br><br>此指標衡量播放過程中視頻卡頓的嚴重程度。<br><br>計算方式：每 100 秒卡頓時間 =（所有直播間的卡頓總時長 / 所有直播間的播放總時長）\* 100<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當渲染的影片畫面與上一個渲染的影片畫面之間的時間間隔超過 200 毫秒時，該間隔會被計入影片凍結的持續時間。持續監控並優化此指標可以提升影片播放的流暢度並改善用戶體驗。</div><br> |
|FirstFrameTime |Double |`0` |您 BytePlus 帳戶下每位觀眾的平均首幀時間，表示直播視頻播放器啟動到螢幕顯示首個視頻畫面的時間。單位：毫秒。<br><br>此指標衡量觀眾等待直播視頻開始播放的時間長度。<br><br>計算方法：<br><br><br>* 單一觀眾首幀時間 = 首幀顯示時間戳 \- 播放器啟動時間戳<br><br>* 平均首幀時間 = 您 BytePlus 帳戶下所有直播間所有觀眾的首幀總時間 / 您 BytePlus 帳戶下所有直播間的觀眾總數 |


<span id="276bff99"></span>
## 範例

<span id="0c1dde7c"></span>
### 範例請求

```JSON
Get https://livesaas.byteplusapi.com/?Action=GetAccountQualityDataAPI&Version=2023-08-01&BeginTime=1702263015&EndTime=1702264015
```


<span id="7238a117"></span>
### 範例回應

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "GetAccountQualityDataAPI", 
        "Version": "2023-08-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1703347287 
    }, 
   "Result": {
        "AccountData": {
            "PullSuccessRate": 100,
            "StallTimePer100Sec": 0,
            "FirstFrameTime": 0
        }
    }
}
```


<span id="63ff57ff"></span>
## 錯誤碼

共用錯誤碼列表請參閱 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。


|名稱 |訊息 |解決方案 |
|---|---|---|
|100000 |內部錯誤。 |請聯絡技術支援。 |
|100005 |指定的參數 BeginTime 無效。 |請更改 `BeginTime` 值。 |
|100005 |EndTime 不可等於或早於 BeginTime。 |請更改 `EndTime` 值。 |
|100005 |BeginTime 與 EndTime 之間的時間間隔不可少於 1 分鐘。 |請檢查並更改 `BeginTime` 和 `EndTime` 值。 |
|100005 |BeginTime 與 EndTime 之間的時間間隔不可超過 365 天。 |請檢查並修改 `BeginTime` 和 `EndTime` 的值。 |
|100005 |BeginTime 與 EndTime 之間的時間間隔不可設定為超過 365 天。 |請檢查並修改 `BeginTime` 和 `EndTime` 的值。 |
