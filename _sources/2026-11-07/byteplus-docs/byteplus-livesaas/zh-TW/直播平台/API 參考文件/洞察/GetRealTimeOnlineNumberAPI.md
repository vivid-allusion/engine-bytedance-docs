---
title: "GetRealTimeOnlineNumberAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getrealtimeonlinenumberapi-zh-TW"
---

呼叫此 API 以取得指定直播間的線上觀眾數，包括虛擬人氣。資料每分鐘更新一次。

<span id="a5e47365"></span>
## 需求

配額：每個帳戶每分鐘最多 120 次請求

<span id="b64eac6a"></span>
## HTTP 請求


* 方法：GET

* 端點：`https://livesaas.byteplusapi.com/?Action=GetRealTimeOnlineNumberAPI&Version=2020-06-01`


<span id="3f1a15e7"></span>
## 請求參數

<span id="f6822206"></span>
### 通用參數

下表並未包含所有通用請求參數。完整列表請參見 [共用參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW)。

<span id="ce9592c2"></span>
### 查詢


|參數 |資料型別 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`GetRealTimeOnlineNumberAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`178398****301234` |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得此 ID。 |


<span id="21aa01c9"></span>
## 回應參數


|參數 |資料型別 |範例值 |說明 |
|---|---|---|---|
|RealPopularity |Integer |`1` |直播間的實際觀眾數。 |
|FakePopularity |Integer |`2` |直播間的虛擬人氣。 |


<span id="e910ff53"></span>
## 範例

<span id="9fe44dd6"></span>
### 範例請求

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetRealTimeOnlineNumberAPI&Version=2020-06-01&ActivityId=178398****301234
```


<span id="6ff71fa6"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetRealTimeOnlineNumberAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1681979936
    },
    "Result": {
        "RealPopularity": 1,
        "FakePopularity": 2
    }
}
```


<span id="9ccfe9d9"></span>
## 錯誤碼

常見錯誤碼列表請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
