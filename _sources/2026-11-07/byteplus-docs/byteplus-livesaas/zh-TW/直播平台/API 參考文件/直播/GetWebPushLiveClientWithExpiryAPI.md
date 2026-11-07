---
title: "GetWebPushLiveClientWithExpiryAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/getwebpushliveclientwithexpiryapi-zh-TW"
---

呼叫此 API 以取得直播間的直播頁面 URL。此功能允許主持人在未登入的情況下，從網頁瀏覽器啟動直播。回傳的 URL 會在指定的時間後過期。

<span id="88078564"></span>
## 需求


* 配額：每個帳戶每分鐘最多 120 次查詢

* 前提條件：需有 BytePlus 帳戶或具備 Live 控制 \> 僅檢視或編輯權限的 IAM 使用者。欲了解更多資訊，請參閱 [管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-shi-yong-zhe-zu-zhi-yu-jue-se-zh-TW)。


<span id="d8d3af2c"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=GetWebPushLiveClientWithExpiryAPI&Version=2020-06-01`

* 方法：POST


<span id="82b326f4"></span>
## 請求參數

下表並未包含所有常用的請求參數。完整列表請參閱 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="3998820f"></span>
### 查詢


|名稱 |資料型態 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`GetWebPushLiveClientWithExpiryAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="763ef914"></span>
### Body


|名稱 |資料型態 |必填 |範例值 |說明 |
|---|---|---|---|---|
|ActivityId |Long |是 |`17218312****` |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得此 ID。 |
|ExpiredTime |Long |否 |`10` |URL 的過期時間。URL 在此期間後將失效。<br><br>單位：秒。<br><br>預設值：`10`。<br><br>數值範圍：[1,300] |


<span id="3bbf0ac3"></span>
## 回應參數


|名稱 |資料型態 |範例值 |說明 |
|---|---|---|---|
|ActivityId |Long |`17218312****` |直播間的活動 ID。 |
|Url |String |`https://byteplus-console.byteintl.net/livesaas/webpush/micromode/{activityId}?webpush_token=MXlRdjhuaUF0OGZUQmlMWFNTdFo3ZEZpMXQ3U0kwLzZrR2JpR1BnOUZ3Z253cWJyM0Zub3ZYVzIwdEYvSnh5QlFHSmpkVDJJT3lpcC9yK25vUFlrcXhmYkVSWFBTekNNbUhXNG5KcENvK092aTRhaG8xbHd6VkJZdHRLRWN5cjRvMz****RiSmE0SnE2WHM4MVkrWU9BPT0=` |直播頁面的 URL。主持人可使用此 URL 從網頁瀏覽器啟動直播，無需登入。URL 會在指定時長後過期。 |


<span id="29a8e2eb"></span>
## 範例

<span id="4bcaf942"></span>
### 範例請求

```JSON
POST https://livesaas.byteplusapi.com/?Action=GetWebPushLiveClientWithExpiryAPI&Version=2020-06-01
{
    "ActivityId": 17218312****,
    "ExpiredTime": 10  
}
```


<span id="57c6761e"></span>
### 範例回應

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "GetWebPushLiveClientWithExpiryAPI", 
        "Version": "2020-06-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1656067132 
    }, 
    "Result": {
        "ActivityId": 17218312****,
        "Url": "https://byteplus-console.byteintl.net/livesaas/webpush/micromode/{activityId}?webpush_token=MXlRdjhuaUF0OGZUQmlMWFNTdFo3ZEZpMXQ3U0kwLzZrR2JpR1BnOUZ3Z253cWJyM0Zub3ZYVzIwdEYvSnh5QlFHSmpkVDJJT3lpcC9yK25vUFlrcXhmYkVSWFBTekNNbUhXNG5KcENvK092aTRhaG8xbHd6VkJZdHRLRWN5cjRvMz****RiSmE0SnE2WHM4MVkrWU9BPT0="
    }
}
```


<span id="6e60f4b7"></span>
## 錯誤碼

常見錯誤碼列表請參閱 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
