---
title: "GetWebPushLiveClientAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getwebpushliveclientapi-zh-TW"
---

取得直播間直播頁面的 URL，允許主持人從網頁瀏覽器啟動直播，無需登入。

<span id="d1ad3925"></span>
## 需求

配額：每個帳戶每分鐘最多 120 次查詢

<span id="a61cce88"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=GetWebPushLiveClientAPI&Version=2020-06-01`

* 方法：GET


<span id="11dd5e64"></span>
## 請求參數

下表未包含所有共用請求參數。完整列表請參見 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="4e52a872"></span>
### 查詢


|名稱 |資料型別 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`GetWebPushLiveClientAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218312****` |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得 ID。 |


<span id="c917226e"></span>
## 回應參數


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|Url |String |`http://livesaas.example.com/***` |直播頁面的 URL。主持人可在網頁瀏覽器開啟此 URL 以啟動直播，無需登入。 |


<span id="7d9b305a"></span>
## 範例

<span id="2c69e10f"></span>
### 範例請求

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetWebPushLiveClientAPI&Version=2020-06-01&ActivityId=17218312****
```


<span id="59f3352f"></span>
### 範例回應

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "GetWebPushLiveClientAPI", 
        "Version": "2020-06-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1656067132 
    }, 
    "Result": {
        "Url": "http://livesaas.example.com/***"
    }
}
```


<span id="cb06ddde"></span>
## 錯誤碼

共用錯誤碼列表請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
