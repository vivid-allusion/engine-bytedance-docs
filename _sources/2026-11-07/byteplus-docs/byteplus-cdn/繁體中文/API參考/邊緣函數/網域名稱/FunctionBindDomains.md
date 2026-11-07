---
title: "FunctionBindDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-FunctionBindDomainList-zh-tw"
---

將函數與網域名稱關聯。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多可傳送 20 個請求。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">邊緣函數僅綁定已在當前 BytePlus 帳戶中新增到 BytePlus CDN 的網域名稱。</div>


<span id="請求說明"></span>
## 請求說明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=FunctionBindDomains&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `FunctionBindDomains`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |是否必選 |描述 |範例值 |
|---|---|---|---|---|
|Domains |String[] |是 |輸入您希望與函數關聯的網域名稱。您可以透過呼叫 [ListFunctionDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCDNDomain-cn) 獲取可用的 CDN 網域名稱列表。 |`["test1.example.com","test2.example.com"]` |
|FunctionId |String |是 |輸入您希望關聯網域名稱的函數ID。您可以透過呼叫 [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-zh-tw) 獲取 FunctionId。 |`3gyz993****` |


<span id="返回參數"></span>
## 返回參數

無

<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```json
POST  https://cdn.byteplusapi.com?Action=FunctionBindDomains&Version=2021-03-01
{
  "FunctionId": "b21f19d28c7f4fbbb8b8bc799f28****",
  "Domains":[
    "a.example.com",
    "b.example.com"
    ]
}
```
