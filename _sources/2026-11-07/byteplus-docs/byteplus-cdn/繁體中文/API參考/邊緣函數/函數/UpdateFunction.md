---
title: "UpdateFunction"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateFunction-zh-tw"
---

更新函數的名稱或描述。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多可傳送 20 個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=UpdateFunction&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `UpdateFunction`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |是否必選 |描述 |範例值 |
|---|---|---|---|---|
|FunctionId |String |是 |函數 ID。您可以呼叫[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-zh-tw)取得函數 ID。 |`3gyz993****` |
|Name |String |是 |新的函數名稱。名稱必須滿足以下要求：<br><br><br>* 只能包含字母、數字和連字元（\-）。<br><br>* 長度不得超過128個字元。 |`test-Function2` |
|Remark |String |否 |該函數的備註。輸入要求如下：<br><br><br>* 允許任何字元。<br><br>* 長度不應超過80個字元。<br><br>* 如果不使用此欄位，將不進行修改。當此欄位值未填寫時，描述將修改為空。 |`This is a test Function` |


<span id="返回參數"></span>
## 返回參數

無

<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```json
POST  https://cdn.byteplusapi.com/?Action=UpdateFunction&Version=2021-03-01
{
  "FunctionId": "bc36dc7c58e942f0b9f125d186df54d9",
  "Name": "test-doc",
  "Remark": ""
}
```
