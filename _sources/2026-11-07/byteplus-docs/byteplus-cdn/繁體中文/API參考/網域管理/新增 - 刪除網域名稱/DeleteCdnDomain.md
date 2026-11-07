---
title: "DeleteCdnDomain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DeleteCdnDomain_zh-tw"
---

刪除指定的網域名稱。網域名稱刪除後，您將無法查看該網域名稱的設定以及該網域名稱的歷史資料。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DeleteCdnDomain&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DeleteCdnDomain`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Domain |String |是 |表示一個要刪除的網域名稱。 |`www.example.com` |


<span id="回應"></span>
## 回應

<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DeleteCdnDomain&Version=2021-03-01
{
    "Domain": "www.example.com"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202109152017370101941000541800CE83",
        "Action": "DeleteCdnDomain",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
