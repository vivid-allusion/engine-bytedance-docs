---
title: "DescribeCipherTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeCipherTemplate_zh-tw"
---

取得一個加密策略的配置詳情。


* 如果該策略已發布，API 預設返回的是該策略下已發布，也就是狀態為 `running` 的版本設定詳情。

* 如果該策略未發布，API 預設返回的是該策略下狀態為 `draft` 的版本設定詳情。


您也可以指定該策略下的某個版本，取得該版本的設定詳情。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeCipherTemplate&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeCipherTemplate`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|TemplateId |String |是 |表示您要查詢的加密策略的 ID。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeTemplates_zh-tw) 取得您想要查詢的加密策略的 ID。 |`tpl-c2PRDW` |
|TemplateVersion |String |否 |表示該策略下的一個版本，API 返回該版本的設定詳情。<br><br>該參數的預設值如下：<br><br><br>* 如果該策略已發布，該參數的預設值是策略下已發布，也就是狀態為 `running` 的版本。<br><br>* 如果該策略未發布，該參數的預設值為 `draft`。<br><br><br>您可以呼叫 [DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_zh-tw) 取得該策略下的所有版本。 |`P-250414.89520` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|BoundDomains |Object[] |對於 `TemplateId` 所指定的加密策略，該參數表示一個與該加密策略綁定的網域名稱列表。<br><br>如果該策略未與任何網域名稱綁定，該參數值為 `null`。 | |
|BoundTime |Long |表示該加密策略與 `Domain` 所指定的網域名稱綁定的時間，格式是 Unix 時間戳。 |`1709174039` |
|Domain |String |表示一個與該加密策略綁定的網域名稱。 |`www.example.com` |
|CreateTime |Long |表示該網域名稱的建立時間，格式是 Unix 時間標記。 |`1636612244` |
|HTTPS |Object |表示 HTTPS 加密服務的設定。 | |
|DisableHttp |Boolean |表示是否允許請求 URL 中 Scheme 是 `HTTP` 的請求。該參數有以下取值：<br><br><br>* `true`：表示允許 Scheme 是 `HTTP` 的請求。<br><br>* `false`：表示不允許 Scheme 是 `HTTP` 的請求。 |`false` |
|ForcedRedirect |Object |表示 "HTTP 強制重新導向到 HTTPS" 特性的設定。<br><br>说明<br><br>CDN 提供了兩種協定重新導向的特性。<br><br><br>* HTTP 重新導向到 HTTPS，也就是 `ForcedRedirect` 特性。<br><br>* HTTPS 重新導向到 HTTP，也就是 `HttpForcedRedirect` 特性。<br><br><br>這兩個協定重新導向特性是互斥的。也就是說，其中一個特性啟用了，另一個就不能啟用。 | |
|EnableForcedRedirect |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。啟用後，CDN 會將收到的 HTTP 請求重新導向到 HTTPS 請求。<br><br>* `false`：表示禁用該特性。禁用後，CDN 不會將 HTTP 請求重新導向到 HTTPS 請求。 |`true` |
|StatusCode |String |表示當收到 HTTPS 請求時 CDN 的重新導向回應狀態碼。該參數有以下取值：<br><br><br>* `301`：表示返回的狀態碼是 301。<br><br>* `302`：表示返回的狀態碼是 302。 |`301` |
|HTTP2 |Boolean |表示是否為使用者請求啟用 HTTP/2 支援。該參數有以下取值：<br><br><br>* `true`：表示啟用 HTTP/2。<br><br>* `false`：表示禁用 HTTP/2。 |`true` |
|Hsts |Object |表示 HSTS 特性的設定。 | |
|Subdomain |String |表示 HSTS 設定是否也應用於網域名稱的子網域名稱。該參數有以下取值：<br><br><br>* `include`：表示 HSTS 設定應用於子網域名稱網站。<br><br>* `exclude`：表示 HSTS 設定不應用於子網域名稱網站。 |`include` |
|Switch |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |
|Ttl |Long |表示 `Strict-Transport-Security` 回應標頭在瀏覽器中的快取過期時間，單位是秒。<br><br>如果該參數值為 `0`，其效果等同於禁用 HSTS 設定。 |`300` |
|OCSP |Boolean |表示是否啟用 "OCSP 裝訂" 特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |
|TlsVersion |String[] |表示 "TLS 版本" 特性的設定。該參數指定使用者請求可以使用的 TLS 版本，有以下取值：<br><br><br>* `tlsv1.0`：表示 TLS 1.0。<br><br>* `tlsv1.1`：表示 TLS 1.1。<br><br>* `tlsv1.2`：表示 TLS 1.2。<br><br>* `tlsv1.3`：表示 TLS 1.3。 |`["tlsv1.1","tlsv1.2"]` |
|HttpForcedRedirect |Object |表示 "HTTPS 強制重新導向到 HTTP" 特性的設定。 | |
|EnableForcedRedirect |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。啟用後，CDN 會將收到的 HTTPS 請求重新導向到 HTTP 請求。<br><br>* `false`：表示禁用該特性。CDN 不會將 HTTPS 請求重新導向到 HTTP 請求。 |`true` |
|StatusCode |String |表示當收到 HTTPS 請求時，CDN 返回的重新導向狀態碼。該參數有以下取值：**301**、**302**、**303**、**307**、**308**。<br><br>需要留意的是：<br><br><br>* 對於 301 和 302，如果原請求使用的方法不是GET，那麼用戶端向新的URL傳送請求時，新請求使用的方法可能變成 GET。<br><br>* 對於 303，新請求使用的方法是 GET。<br><br>* 對於 307 和 308，新請求使用的方法與原請求相同，不會被改變。 |`302` |
|Message |String |表示該加密策略的描述。 |`Test` |
|Quic |Object |表示 QUIC 設定。 | |
|Switch |Boolean |表示是否為使用者請求啟用 QUIC。該參數有以下取值：<br><br><br>* `true`：表示啟用 QUIC。<br><br>* `false`：表示停用 QUIC。 |`true` |
|Status |String |表示 `ProdVersion` 的狀態，該參數有以下取值：<br><br><br>* `editing`：表示狀態為 "草稿"。此時， `ProdVersion` 的值為空（""）。<br><br>* `locked`：表示狀態為 "已發布"。 |`editing` |
|TemplateId |String |表示該加密策略的 ID。 |`tpl-c2PRDW` |
|Title |String |表示該加密策略的名稱。 |`Standard` |
|Type |String |表示該加密策略的類型。該參數值始終是 `cipher`。 |`cipher` |
|UpdateTime |Long |表示該網域名稱設定的最近更新時間，格式是 Unix 時間標記。如果該網域名稱設定在建立後未被更新，該參數值與 `CreateTime` 的值相同。 |`1639621409` |
|Exception |Boolean |表示該加密策略是否包含特殊配置。特殊配置指的是那些不由使用者，而是由 BytePlus 工程師操作的配置。該參數有以下取值：<br><br><br>* `true`：表示包含特殊配置。<br><br>* `false`：表示不包含特殊配置。 |`false` |
|Project |String |表示該網域名稱歸屬的專案。 |`default` |
|ProdVersion |String |表示該策略下已發布，也就是狀態為 `running` 的版本。如果不存在狀態為 `running` 的版本，該參數值為空（""）。 |`P-250414.89520` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCipherTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-c57pd62"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20250825065108DF9658839E53B0AEB207",
        "Action": "DescribeCipherTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "BoundDomains": [
            {
                "BoundTime": 1755585664,
                "Domain": "www.example.com"
            }
        ],
        "CreateTime": 1755585663,
        "Exception": false,
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
        "Message": "This is a test message",
        "ProdVersion": "P-250819.88575",
        "Project": "default",
        "Quic": {
            "Switch": true
        },
        "Status": "locked",
        "TemplateId": "tpl-c57pd62",
        "Title": "My Policy",
        "Type": "cipher",
        "UpdateTime": 1755585664
    }
}
```


&nbsp;
