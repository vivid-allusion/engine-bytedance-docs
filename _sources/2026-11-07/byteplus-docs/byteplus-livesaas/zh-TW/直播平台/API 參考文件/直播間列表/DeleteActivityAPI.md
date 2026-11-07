---
title: "DeleteActivityAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-deleteactivityapi-zh-TW"
---

刪除指定的直播間。

<span id="49f3eda3"></span>
## 需求

配額：每個帳戶每分鐘最多 120 次查詢

<span id="fb6bd457"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=DeleteActivityAPI&Version=2020-06-01`

* 方法：POST


<span id="bd8d722e"></span>
## 請求參數

以下表格未包含所有共用請求參數。完整列表請參見 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="b918969c"></span>
### 查詢


|名稱 |資料型別 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`DeleteActivityAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |API 版本。本次發佈的值為 `2020-06-01`。 |


<span id="5d1ac93d"></span>
### Body


|名稱 |資料型別 |必填 |範例值 |說明 |
|---|---|---|---|---|
|ActivityId |Long |是 |`17218312****` |欲刪除直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW) 取得 ID。 |


<span id="63eb7a98"></span>
## 回應參數


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|ActivityId |Long |`17218312****` |已刪除直播間的活動 ID。 |
|ActivityIdStr |String |`-` |已棄用。 |
|Status |Integer |`-` |已棄用。 |


<span id="eb9fbc1d"></span>
## 範例

<span id="03f5d9e6"></span>
### 範例請求

```JSON
POST https://livesaas.byteplusapi.com/?Action=DeleteActivityAPI&Version=2020-06-01
{
  "ActivityId": 17218312****
}
```


<span id="Response"></span>
### 範例回應

```JSON
{
  "ResponseMetadata": {
    "RequestId": "2018060411042001001002322800209D2",
    "Action": "DeleteActivityAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1656067132
  },
  "Result": {
    "ActivityId": 17218312****,
    "ActivityIdStr": "",
    "Status": 0
  }
}
```


<span id="9191ac59"></span>
## 錯誤碼

共用錯誤碼列表請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
