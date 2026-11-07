---
title: "GetActivityMenuAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivitymenuapi-zh-TW"
---

此 API 用於獲取直播間的菜單列表。回應包含每個菜單的名稱、類型及顯示順序。

<span id="11f1c7f4"></span>
## 需求

配額：每個帳戶每分鐘 120 次查詢

<span id="efb823e7"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=GetActivityMenuAPI&Version=2020-06-01`

* 方法：GET


<span id="4436b24c"></span>
## 請求參數

下表未包含所有共用請求參數。完整列表請參見 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="Request"></span>
### 查詢


|名稱 |資料型別 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`GetActivityMenuAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`178398113630****` |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 獲取 ID。 |


<span id="37718e59"></span>
## 回應參數


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|菜單 |Array of[菜單](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitymenuapi-zh-TW#d6851f47) |`-` |菜單物件陣列。 |


<span id="d6851f47"></span>
### 菜單


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|名稱 |String |`Chat` |菜單名稱。 |
|類型 |Integer |`3` |菜單類型。<br><br><br>* `1`：圖文。<br><br>* `2`：商品卡片。<br><br>* `3`：聊天互動。<br><br>* `4`：互動工具。<br><br>* `5`：聚合直播。<br><br>* `6`：問答。<br><br>* `7`：嵌入連結。 |
|位置 |Integer |`1` |菜單的顯示順序。值從 `1` 開始。 |


<span id="abfcc133"></span>
## 範例

<span id="951902d9"></span>
### 範例請求

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetActivityMenuAPI&Version=2020-06-01&ActivityId=178398113630****
```


<span id="f7900aaf"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetActivityMenuAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1714653986
    },
    "Result": [
        {
            "Name": "Chat",
            "Type": 3,
            "Location": 1
        },
        {
            "Name": "Interactions",
            "Type": 4,
            "Location": 2
        }
    ]
}
```


<span id="9d6706a4"></span>
## 錯誤碼

共用錯誤碼列表請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
