---
title: "UpdateCipherTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UpdateCipherTemplate_zh-tw"
---

在 BytePlus CDN 中修改一個加密策略的配置。

在 BytePlus CDN 中，如果您需要修改一個網域名稱的配置，可以使用以下任意方法：


* 方法一：直接修改該網域名稱的配置。

* 方法二：修改該網域名稱所綁定的策略配置。


本文介紹的是透過 API 來實現方法二中對加密發策略的更新。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">關於這兩種方法的區別，參見 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw">網域名稱設定</a>。</div>


* <div data-tips="true" data-tips-type="tip">關於如何透過 API 來實現方法二中對分發策略的更新，參見 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UpdateServiceTemplate_zh-tw">UpdateServiceTemplate</a>。</div>


* <div data-tips="true" data-tips-type="tip">關於如何透過 API 來實現方法一，參見 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/reference-global-catalog_zh-tw">全域設定</a>。</div>



除了 `Title` 和 `Message`，其他參數的更新需要您在呼叫 `UpdateCipherTemplate` 時指定 `TemplateVersion` 為 `draft`。也就是說，待更新的策略已存在 Draft 版本。要確保待更新的策略已存在 Draft 版本，參照以下步驟：


1. 對該策略呼叫 `DescribeTemplateReleaseVersions` API。

2. 在 API 返回的版本列表中，查看 Draft 版本（`"Version": "draft"`）是否存在。

* 如果 Draft 版本存在，您可以對該策略呼叫 `UpdateCipherTemplate`。

* 否則，您需要先對該策略呼叫 `CreateTemplateVersion` 以建立 Draft 版本，然後再呼叫 `UpdateCipherTemplate`。


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">該 API 在網域名稱級別對配置模組進行覆蓋式修改，說明如下：</div>



* <div data-tips="true" data-tips-type="warning">在您建立一個 API 請求時，如果未指定某個模組，在您提交 API 請求後，該模組的既有配置不會發生改變。</div>


* <div data-tips="true" data-tips-type="warning">如果您指定了某個模組，但沒有指定該模組下的某個可選參數，則該參數會使用預設值。在您提交 API 請求後，該參數的既有值就會被預設值覆蓋。</div>



<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=UpdateCipherTemplate&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `UpdateCipherTemplate`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|TemplateId |String |是 |表示您要修改的加密策略的 ID。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeTemplates_zh-tw) 獲取您想要修改的加密策略的 ID。 |`tpl-c2vy7q` |
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
|Message |String |否 |表示一個新的策略描述，長度不能超過 120 個字元。 |`This is a test.` |
|Quic |Object |否 |表示 QUIC 設定。 | |
|Switch |Boolean |是 |表示是否為使用者請求啟用 QUIC。該參數有以下取值：<br><br><br>* `true`：表示啟用 QUIC。<br><br>* `false`：表示停用 QUIC。<br><br><br>要啟用該特性，您的網域名稱必須已啟用 HTTPS。 |`true` |
|Title |String |否 |表示一個新的策略名稱，長度不能超過 100 個字元。 |`Test-Policy` |
|TemplateVersion |String |否 |表示待更新的策略版本。<br><br><br>* 如果待更新的參數是 `Title` 或 `Message`，您無需指定該參數。這兩個參數與策略版本無關。<br><br>* 如果待更新的參數不是 `Title` 和 `Message`，您必須指定該參數為 `draft`。參見文件開頭的描述。 |`draft` |


<span id="回應"></span>
## 回應

<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=UpdateCipherTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-c2vy7q",
    "TemplateVersion": "draft",
    "HTTPS": {
        "DisableHttp": false,
        "ForcedRedirect": {
            "EnableForcedRedirect": true,
            "StatusCode": "302"
        },
        "HTTP2": true,
        "Hsts": {
            "Subdomain": "include",
            "Switch": true,
            "Ttl": 1800
        },
        "OCSP": true,
        "TlsVersion": [
            "tlsv1.2",
            "tlsv1.3"
        ]
    },
    "HttpForcedRedirect": {
        "EnableForcedRedirect": false,
        "StatusCode": "302"
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
        "RequestId": "20210915182437010194100054410018B1",
        "Action": "UpdateCipherTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
