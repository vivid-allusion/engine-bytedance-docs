---
title: "CreateCipherTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-CreateCipherTemplate_zh-tw"
---

在 BytePlus CDN 建立一個加密策略。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=CreateCipherTemplate&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `CreateCipherTemplate`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Title |String |是 |表示您要建立的加密策略的名稱，長度不能超過 100 個字元。 |`TestPolicy` |
|HTTPS |Object |否 |表示 HTTPS 加密服務的設定。 | |
|DisableHttp |Boolean |否 |表示是否允許請求 URL 中 Scheme 是 `HTTP` 的請求。該參數有以下取值：<br><br><br>* `true`：表示允許 Scheme 是 `HTTP` 的請求。<br><br>* `false`：表示不允許 Scheme 是 `HTTP` 的請求。<br><br><br>該參數的預設值是 `false`。 |`false` |
|ForcedRedirect |Object |否 |表示 "HTTP 強制跳轉到 HTTPS" 特性的設定。<br><br>说明<br><br>CDN 提供了兩種通訊協定重定向的特性。<br><br><br>* HTTP 重定向到 HTTPS，也就是 `ForcedRedirect` 特性。<br><br>* HTTPS 重定向到 HTTP，也就是 `HttpForcedRedirect` 特性。<br><br><br>這兩個通訊協定重定向特性是互斥的。也就是說，如果您啟用了其中任意一個特性，就不能啟用另一個。 | |
|EnableForcedRedirect |Boolean |是 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。啟用後，CDN 會將收到的 HTTP 請求重定向到 HTTPS 請求。<br><br>* `false`：表示停用該特性。停用後，CDN 不會將 HTTP 請求重定向到 HTTPS 請求。<br><br><br>要啟用該特性，您的網域名稱必須已啟用 HTTPS。 |`true` |
|StatusCode |String |是 |表示當收到 HTTPS 請求時 CDN 的重定向回應狀態碼。該參數有以下取值：<br><br><br>* `301`：表示返回的狀態碼是 301。<br><br>* `302`：表示返回的狀態碼是 302。<br><br><br>該參數的預設值是 `301`。 |`301` |
|HTTP2 |Boolean |否 |表示是否為使用者請求啟用 HTTP/2 支援。該參數有以下取值：<br><br><br>* `true`：表示啟用 HTTP/2。<br><br>* `false`：表示停用 HTTP/2。<br><br><br>要啟用該特性，您的網域名稱必須已經啟用了 HTTPS 加密服務。<br><br>該參數的預設值是 `false`。 |`true` |
|Hsts |Object |否 |表示 HSTS 特性的設定。 | |
|Subdomain |String |否 |表示 HSTS 設定是否也應用於網域名稱的子網域名稱。該參數有以下取值：<br><br><br>* `include`：表示 HSTS 設定應用於子網域名稱網站。<br><br>* `exclude`：表示 HSTS 設定不應用於子網域名稱網站。<br><br><br>該參數的預設值是 `exclude`。 |`include` |
|Switch |Boolean |否 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。<br><br><br>該參數的預設值是 `false`。 |`true` |
|Ttl |Long |否 |表示 `Strict-Transport-Security` 回應標頭在瀏覽器中的快取過期時間，單位是秒。如果 `Switch` 是 `true`，該參數為必填。該參數的取值範圍是 0 \- 31,536,000。31,536,000 秒表示 365 天。如果該參數值為 `0`，其效果等同於停用 HSTS 設定。 |`300` |
|OCSP |Boolean |否 |表示是否啟用 "OCSP 裝訂" 特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。<br><br><br>要啟用該特性，您的網域名稱必須啟用了 HTTPS。該參數的預設值是 `false`。 |`true` |
|TlsVersion |String[] |否 |表示 "TLS 版本" 特性的設定。該參數指定使用者請求可以使用的 TLS 版本，有以下取值：<br><br><br>* `tlsv1.0`：表示 TLS 1.0。<br><br>* `tlsv1.1`：表示 TLS 1.1。<br><br>* `tlsv1.2`：表示 TLS 1.2。<br><br>* `tlsv1.3`：表示 TLS 1.3。<br><br><br>該參數的預設值是 `["tlsv1.1", "tlsv1.2", "tlsv1.3"]` |`["tlsv1.1","tlsv1.2"]` |
|HttpForcedRedirect |Object |否 |表示 "HTTPS 強制跳轉到 HTTP" 特性的設定。 | |
|EnableForcedRedirect |Boolean |是 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。啟用後，CDN 會將收到的 HTTPS 請求重定向到 HTTP 請求。<br><br>* `false`：表示停用該特性。CDN 不會將 HTTPS 請求重定向到 HTTP 請求。<br><br><br>要啟用該特性，您的網域名稱必須已啟用 HTTPS。 |`true` |
|StatusCode |String |是 |表示當收到 HTTPS 請求時，CDN 返回的重定向狀態碼。該參數有以下取值：**301**、**302**、**303**、**307**、**308**。<br><br>該參數的預設值是 `301`。<br><br>需要留意的是：<br><br><br>* 對於 301 和 302，如果原請求使用的方法不是GET，那麼客戶端向新的URL傳送請求時，新請求使用的方法可能變成 GET。<br><br>* 對於 303，新請求使用的方法是 GET。<br><br>* 對於 307 和 308，新請求使用的方法與原請求相同，不會被改變。 |`302` |
|Message |String |否 |表示該加密策略的描述，長度不能超過 120 個字元。 |`This is a test.` |
|Quic |Object |否 |表示 QUIC 設定。 | |
|Switch |Boolean |是 |表示是否為使用者請求啟用 QUIC。該參數有以下取值：<br><br><br>* `true`：表示啟用 QUIC。<br><br>* `false`：表示停用 QUIC。<br><br><br>要啟用該特性，您的網域名稱必須已啟用 HTTPS。 |`true` |
|Project |String |否 |表示該加密策略所歸屬的專案。該參數的預設值是 `default`，表示 Default 專案。 |`default` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|TemplateId |String |表示建立的加密策略的 ID。 |`tpl-cqwYjZ` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=CreateCipherTemplate&Version=2021-03-01
{
    "Title": "My Policy",
    "Message": "This is a test.",
    "Project": "default",
    "HTTPS": {
        "DisableHttp": false,
        "ForcedRedirect": {
            "EnableForcedRedirect": true,
            "StatusCode": "303"
        },
        "HTTP2": true,
        "Hsts": {
            "Subdomain": "include",
            "Switch": true,
            "Ttl": 50
        },
        "OCSP": true,
        "TlsVersion": [
            "tlsv1.1",
            "tlsv1.2"
        ]
    },
    "HttpForcedRedirect": {
        "EnableForcedRedirect": false,
        "StatusCode": "301"
    },
    "Quic": {
        "Switch": true
    }
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "2025082506361220B64EDF1EC3CBBB1ADE",
        "Action": "CreateCipherTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TemplateId": "tpl-ceg0x7z"
    }
}
```


&nbsp;
