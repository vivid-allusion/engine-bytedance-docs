---
title: "CheckCdnDomain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CheckCdnDomain_zh-tw"
---

對指定網域名稱進行所有權校驗。在調用此 API 之前，請確保您已按照 CDN 控制台提示在網域名稱 DNS 服務提供商處建立了相應的 TXT 記錄。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=CheckCdnDomain&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `CheckCdnDomain`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Domain |String |是 |表示一個待校驗的網域名稱，可以是泛網域名稱。 |`www.example.com` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|Status |String |表示校驗結果。該參數有以下取值：<br><br><br>* `fail`：表示校驗未通過。<br><br>* `success`：表示校驗通過。 |`fail` |
|ErrorMsg |String |表示校驗未通過的原因。如果 `Status` 是 `success`，該參數值是空（""）。 |`some reason` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=CheckCdnDomain&Version=2021-03-01
{
    "Domain": "www.example.com"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20241206143123375BE43944CA95D1969A",
        "Action": "CheckCdnDomain",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ErrorMsg": "some error",
        "Status": "fail"
    }
}
```


&nbsp;
