---
title: "GetTemporaryLoginTokenAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-gettemporarylogintokenapi-zh-TW"
---

調用此 API 以獲取直播間的密鑰，用於啟動直播。

<span id="bac9c171"></span>
## 需求

配額：每個帳號每分鐘 120 次查詢

<span id="b63c37e0"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=GetTemporaryLoginTokenAPI&Version=2020-06-01`

* 方法：GET


<span id="576d363d"></span>
## 請求參數

下列表格未包含所有共用請求參數。如需完整列表，請參見[共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="64a0bda3"></span>
### 查詢


|名稱 |資料型別 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`GetTemporaryLoginTokenAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。當前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218312****` |直播間的活動 ID。可通過調用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)獲取該 ID。 |


<span id="a8e81e5f"></span>
## 回應參數


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|SecretKey |String |`0UmdWrZKAVWJJTxzCOJ****` |直播間的密鑰，用於啟動直播。 |
|ActivityId |Long |`17218312****` |直播間的活動 ID。 |


<span id="bf977fee"></span>
## 範例

<span id="875465ab"></span>
### 請求範例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetTemporaryLoginTokenAPI&Version=2020-06-01&ActivityId=17218312****
```


<span id="8d037a06"></span>
### 回應範例

```JSON
{
  "ResponseMetadata": {
    "RequestId": "201806041104200100100232280022D30",
    "Action": "GetTemporaryLoginTokenAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1656067132
  },
  "Result": {
      "SecretKey": "0UmdWrZKAVWJJTxzCOJ****",
      "ActivityId": 17218312****
  }
}
```


<span id="53f720b3"></span>
## 錯誤碼

如需共用錯誤碼列表，請參見[常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
