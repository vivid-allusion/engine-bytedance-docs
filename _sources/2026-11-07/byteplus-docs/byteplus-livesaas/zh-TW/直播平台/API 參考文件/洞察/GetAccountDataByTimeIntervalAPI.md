---
title: "GetAccountDataByTimeIntervalAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getaccountdatabyTimeintervalapi-zh-TW"
---

呼叫此 API 以在指定的時間區間內，獲取您的 BytePlus 帳戶下所有直播間的彙總數據。返回的數據包含關鍵指標，例如直播間總數、累計觀看次數、唯一觀眾數，以及總觀看時長。

<span id="aa541d6f"></span>
## 需求


* 配額：每個帳戶每分鐘最多 20 次查詢

* 數據延遲：1\-3 小時


<span id="a564cbb1"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=GetAccountDataByTimeIntervalAPI&Version=2020-06-01`

* 方法：GET


<span id="8865ec2a"></span>
## 請求參數

下表未包含所有共用請求參數。完整列表請參見 [共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。

<span id="8578a4ac"></span>
### **查詢**


|**名稱** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`GetAccountDataByTimeIntervalAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |
|BeginTime |Long |是 |`1692339016` |時間區間的起始時間，採用 Unix 時戳格式。單位：秒。<br><br>將返回此時間區間的數據。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">時間區間不可超過 365 天（31,536,000 秒）。</div><br> |
|EndTime |Long |是 |`1700115016` |時間區間的結束時間，採用 Unix 時戳格式。單位：秒。<br><br>將返回此時間區間的數據。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">時間區間不可超過 365 天（31,536,000 秒）。</div><br> |


<span id="124cd05e"></span>
## **回應參數**


|**名稱** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|EventTimes |Integer |`55` |在所選時間區間內，您的 BytePlus 帳戶下創建的直播間總數。 |
|ViewTime |Integer |`390` |在所選時間區間內，您的 BytePlus 帳戶下所有直播間的累計觀看次數。<br><br>若觀眾刷新觀看頁面一次，觀看次數會增加 1。 |
|ViewPeople |Integer |`200` |在所選時間區間內，您的 BytePlus 帳戶下所有直播間的累計唯一觀眾數。使用同一裝置的觀眾會被計算為一位觀眾。 |
|ViewDuration |Integer |`6000` |在所選時間區間內，您的 BytePlus 帳戶下所有直播間的累計觀看時長。單位：分鐘。 |
|ViewEventTimesPerPeople |Double |`2` |在所選時間區間內，每位觀眾平均觀看的直播間數。此值是以所有直播間的唯一觀眾總和除以累計唯一觀眾數計算得出。<br><br>分子（所有直播間的唯一觀眾總和）會將每位觀眾加入的每個直播間都計算一次。分母（累計唯一觀眾數）無論觀眾加入多少直播間，都只計算一次。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">具有相同裝置 ID 的裝置會被視為同一裝置。</div><br> |
|ViewDurationPerPeople |Double |`30` |在所選時間區間內，每位觀眾的平均觀看時長。此值是以累計觀看時長除以累計唯一觀眾數計算得出。單位：分鐘。 |
|ViewTimesPerPeople |Double |`1.95` |在所選時間區間內，您的 BytePlus 帳戶下每位觀眾的平均觀看次數，此值是以累計觀看次數除以累計唯一觀眾數計算得出。 |


<span id="02d94806"></span>
## 範例

<span id="43bb91f0"></span>
### 範例請求

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetAccountDataByTimeIntervalAPI&Version=2020-06-01&BeginTime=1692339016&EndTime=1700115016
```


<span id="74b36b31"></span>
### **範例回應**

```JSON
{
    "ResponseMetadata": {
        "Action": "GetAccountDataByTimeIntervalAPI",
        "Region": "ap-singapore-1",
        "RequestId": "202201201826170101501312091D1C09D2",
        "Service": "livesaas",
        "SystemTime": 1700125016,
        "Version": "2020-06-01"
    },
    "Result": {
        "EventTimes": 55,
        "ViewTime ": 390,
        "ViewPeople": 200,
        "ViewDuration": 6000,
        "ViewEventTimesPerPeople": 2,
        "ViewDurationPerPeople": 30,
        "ViewTimesPerPeople": 1.95
  }
}
```


<span id="6fa7036e"></span>
## 錯誤碼

共用錯誤碼列表請參見 [共用錯誤與狀態碼](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
