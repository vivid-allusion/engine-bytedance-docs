---
title: "GetBusinessAccountInfoAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getbusinessaccountinfoapi-zh-TW"
---

呼叫此 API 以獲取特定直播間的主帳號資訊。

配額：每個帳號每分鐘最多 120 次查詢

<span id="106bf19e"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=GetBusinessAccountInfoAPI&Version=2023-08-01`

* 方法：GET


<span id="44564612"></span>
## 請求參數

以下表格未包含所有常用請求參數。完整列表請參見 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="1d297938"></span>
### 查詢


|名稱 |資料型別 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`GetBusinessAccountInfoAPI` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。目前版本：`2023-08-01`。 |
|ActivityId |Long |是 |`17218346****` |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得此 ID。 |


<span id="19c0a580"></span>
## 回應參數


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|IsBusinessAccountEnable |Integer |`1` |表示主帳號功能是否啟用。<br><br><br>* `0`：未啟用。<br><br>* `1`：已啟用。 |
|BusinessAccountInfo |[BusinessAccountInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getbusinessaccountinfoapi-zh-TW#1d108f6f) 的物件 |`-` |主帳號相關資訊。 |


<span id="1d108f6f"></span>
### BusinessAccountInfo


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|AccountName |String |`Host A` |主帳號名稱。 |
|HostAccountId |Integer |`112038` |主帳號 ID。 |
|AccountHeadImage |String |`https://example-image.image` |帳號頭像的 URL。 |
|AccountHeadRedirectUrl |String |`https://example.com` |主帳號的嵌入連結。觀眾點擊帳號頭像後可跳轉至此連結。 |
|ExternalPlatformId |String |`abc123` |外部平台 ID，僅包含大小寫字母及數字，且長度不超過 128 個字元。 |
|ExtraInfo |String |`abc` |與主帳號相關的附加資訊。 |


<span id="e5a3129b"></span>
## 範例

<span id="78aee2a5"></span>
### 範例請求

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetBusinessAccountInfoAPI&Version=2023-08-01&ActivityId=17218346****
```


<span id="e4dbc391"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetBusinessAccountInfoAPI",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1702896398
    },
    "Result": {
        "IsBusinessAccountEnable": 1,
        "BusinessAccountInfo": {
            "AccountName": "Host A",
            "HostAccountId": 112038,
            "AccountHeadImage": "https://example-image.image",
            "AccountHeadRedirectUrl": "https://example.com",
            "ExternalPlatformId": "abc123",
            "ExtraInfo": "abc"
        }
    }
}
```


<span id="55b7cc9a"></span>
## 錯誤碼

常見錯誤碼列表請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
