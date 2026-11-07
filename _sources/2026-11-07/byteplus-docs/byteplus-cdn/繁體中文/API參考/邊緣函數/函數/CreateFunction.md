---
title: "CreateFunction"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateFunction-zh-tw"
---

建立一個函數。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多可傳送 20 個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=CreateFunction&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `CreateFunction`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |是否必選 |描述 |範例值 |
|---|---|---|---|---|
|Name |String |是 |函數名稱。以下為命名規則：<br><br><br>* 可以使用大寫字母、小寫字母、數字和連字元（\-）。<br><br>* 名稱不應長於128個字元。 |`test-Function` |
|ProjectName |String |否 |函數所屬專案的名稱，預設為`default`。 |`default` |
|Remark |String |否 |該函數的備註。輸入要求如下：<br><br><br>* 允許任何字元。<br><br>* 長度不應超過 128 個字元。 |`This is a test Function` |


<span id="返回參數"></span>
## 返回參數


|參數 |類型 |描述 |範例值 |
|---|---|---|---|
|FunctionId |String |函數的 ID。 |`3gyz993****` |


<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```HTTP
POST  https://cdn.byteplusapi.com?Action=CreateFunction&Version=2021-03-01
{
  "Name": "test-Function"
}
```


<span id="返回範例"></span>
### 返回範例

```json
{
  "ResponseMetadata": {
    "RequestId": "202404220916070BE49FB085D18E85BA26",
    "Action": "CreateFunction",
    "Version": "2021-03-01",
    "Service": "CDN",
    "Region": "ap-singapore-1"
  },
  "Result": {
    "FunctionId": "bc36dc7c58e942f0b9f125d186df****"
  }
}
```


&nbsp;
