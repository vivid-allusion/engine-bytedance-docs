---
title: "UpdateCipherTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-updateciphertemplate-ac087-cn"
---

在 BytePlus CDN 中修改一个加密策略的配置。

在 BytePlus CDN 中，如果您需要修改一个域名的配置，可以使用以下任意方法：


* 方法一：直接修改该域名的配置。

* 方法二：修改该域名所绑定的策略配置。


本文介绍的是通过 API 来实现方法二中对加密发策略的更新。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">关于这两种方法的区别，参见 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn">域名配置</a>。</div>


* <div data-tips="true" data-tips-type="tip">关于如何通过 API 来实现方法二中对分发策略的更新，参见 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-updateservicetemplate-cn">UpdateServiceTemplate</a>。</div>


* <div data-tips="true" data-tips-type="tip">关于如何通过 API 来实现方法一，参见 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateCdnConfig_zh-cn">UpdateCdnConfig</a>。</div>



除了 `Title` 和 `Message`，其他参数的更新需要您在调用 `UpdateCipherTemplate` 时指定 `TemplateVersion` 为 `draft`。也就是说，待更新的策略已存在 Draft 版本。要确保待更新的策略已存在 Draft 版本，参照以下步骤：


1. 对该策略调用 `DescribeTemplateReleaseVersions` API。

2. 在 API 返回的版本列表中，查看 Draft 版本（`"Version": "draft"`）是否存在。

* 如果 Draft 版本存在，您可以对该策略调用 `UpdateCipherTemplate`。

* 否则，您需要先对该策略调用 `CreateTemplateVersion` 以创建 Draft 版本，然后再调用 `UpdateCipherTemplate`。


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">该 API 在域名级别对配置模块进行覆盖式修改，说明如下：</div>



* <div data-tips="true" data-tips-type="warning">在您创建一个 API 请求时，如果未指定某个模块，在您提交 API 请求后，该模块的已有配置不会发生改变。</div>


* <div data-tips="true" data-tips-type="warning">如果您指定了某个模块，但没有指定该模块下的某个可选参数，则该参数会使用默认值。在您提交 API 请求后，该参数的已有值就会被默认值覆盖。</div>



<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=UpdateCipherTemplate&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `UpdateCipherTemplate`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="request-body"></span>
### Request Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|TemplateId |String |是 |表示您要修改的加密策略的 ID。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-describetemplates-cn) 获取您想要修改的加密策略的 ID。 |`tpl-c2vy7q` |
|HTTPS |Object |否 |表示 HTTPS 加密服务的配置。 | |
|DisableHttp |Boolean |否 |表示是否允许请求 URL 中 Scheme 是 `HTTP` 的请求。该参数有以下取值：<br><br><br>* `true`：表示允许 Scheme 是 `HTTP` 的请求。<br><br>* `false`：表示不允许 Scheme 是 `HTTP` 的请求。<br><br><br>该参数的默认值是 `false`。 |`false` |
|ForcedRedirect |Object |否 |表示 "HTTP 强制跳转到 HTTPS" 特性的配置。<br><br>说明<br><br>CDN 提供了两种协议重定向的特性。<br><br><br>* HTTP 重定向到 HTTPS，也就是 `ForcedRedirect` 特性。<br><br>* HTTPS 重定向到 HTTP，也就是 `HttpForcedRedirect` 特性。<br><br><br>这两个协议重定向特性是互斥的。也就是说，如果您启用了其中任意一个特性，就不能启用另一个。 | |
|EnableForcedRedirect |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。启用后，CDN 会将收到的 HTTP 请求重定向到 HTTPS 请求。<br><br>* `false`：表示禁用该特性。禁用后，CDN 不会将 HTTP 请求重定向到 HTTPS 请求。<br><br><br>要启用该特性，您的域名必须已启用 HTTPS。 |`true` |
|StatusCode |String |是 |表示当收到 HTTPS 请求时 CDN 的重定向响应状态码。该参数有以下取值：<br><br><br>* `301`：表示返回的状态码是 301。<br><br>* `302`：表示返回的状态码是 302。<br><br><br>该参数的默认值是 `301`。 |`301` |
|HTTP2 |Boolean |否 |表示是否为用户请求启用 HTTP/2 支持。该参数有以下取值：<br><br><br>* `true`：表示启用 HTTP/2。<br><br>* `false`：表示禁用 HTTP/2。<br><br><br>要启用该特性，您的域名必须已经启用了 HTTPS 加密服务。<br><br>该参数的默认值是 `false`。 |`true` |
|Hsts |Object |否 |表示 HSTS 特性的配置。 | |
|Subdomain |String |否 |表示 HSTS 配置是否也应用于域名的子域名。该参数有以下取值：<br><br><br>* `include`：表示 HSTS 配置应用于子域名站点。<br><br>* `exclude`：表示 HSTS 配置不应用于子域名站点。<br><br><br>该参数的默认值是 `exclude`。 |`include` |
|Switch |Boolean |否 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。<br><br><br>该参数的默认值是 `false`。 |`true` |
|Ttl |Long |否 |表示 `Strict-Transport-Security` 响应头在浏览器中的缓存过期时间，单位是秒。如果 `Switch` 是 `true`，该参数为必填。该参数的取值范围是 0 \- 31,536,000。31,536,000 秒表示 365 天。如果该参数值为 `0`，其效果等同于禁用 HSTS 设置。 |`300` |
|OCSP |Boolean |否 |表示是否启用 "OCSP 装订" 特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。<br><br><br>要启用该特性，您的域名必须启用了 HTTPS。该参数的默认值是 `false`。 |`true` |
|TlsVersion |String[] |否 |表示 "TLS 版本" 特性的配置。该参数指定用户请求可以使用的 TLS 版本，有以下取值：<br><br><br>* `tlsv1.0`：表示 TLS 1.0。<br><br>* `tlsv1.1`：表示 TLS 1.1。<br><br>* `tlsv1.2`：表示 TLS 1.2。<br><br>* `tlsv1.3`：表示 TLS 1.3。<br><br><br>该参数的默认值是 `["tlsv1.1", "tlsv1.2", "tlsv1.3"]` |`["tlsv1.1","tlsv1.2"]` |
|CertCheck |Object |否 |表示 "访问双向认证" 特性的配置。 | |
|CertInfoList |Object[] |否 |表示一个 CA 证书列表。列表中最多包含两个 CA 证书。这些 CA 证书必须是已经托管在 CDN 的。CA 证书使用的加密算法可以是 RSA 或者 ECC。<br><br>如果要关联的证书还未上传，您可以先调用 [AddCertificate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-cn-addcertificate) 将该证书上传到 CDN。 | |
|CertId |String |否 |表示一个 CA 证书的 ID。ID 是以 `cert_hosting-` 开头的。<br><br>您可以调用 [ListCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-listcertinfo-cn) 获取您需要关联的证书的 ID。 |`cert_hosting-31869` |
|Switch |Boolean |否 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。<br><br><br>该参数的默认值是 `false`。 |`true` |
|HttpForcedRedirect |Object |否 |表示 "HTTPS 强制跳转到 HTTP" 特性的配置。 | |
|EnableForcedRedirect |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。启用后，CDN 会将收到的 HTTPS 请求重定向到 HTTP 请求。<br><br>* `false`：表示禁用该特性。CDN 不会将 HTTPS 请求重定向到 HTTP 请求。<br><br><br>要启用该特性，您的域名必须已启用 HTTPS。 |`true` |
|StatusCode |String |是 |表示当收到 HTTPS 请求时，CDN 返回的重定向状态码。该参数有以下取值：**301**、**302**、**303**、**307**、**308**。<br><br>该参数的默认值是 `301`。<br><br>需要留意的是：<br><br><br>* 对于 301 和 302，如果原请求使用的方法不是GET，那么客户端向新的URL发送请求时，新请求使用的方法可能变成 GET。<br><br>* 对于 303，新请求使用的方法是 GET。<br><br>* 对于 307 和 308，新请求使用的方法与原请求相同，不会被改变。 |`302` |
|Message |String |否 |表示一个新的策略描述，长度不能超过 120 个字符。 |`This is a test.` |
|Quic |Object |否 |表示 QUIC 配置。 | |
|Switch |Boolean |是 |表示是否为用户请求启用 QUIC。该参数有以下取值：<br><br><br>* `true`：表示启用 QUIC。<br><br>* `false`：表示禁用 QUIC。<br><br><br>要启用该特性，您的域名必须已启用 HTTPS。 |`true` |
|Title |String |否 |表示一个新的策略名称，长度不能超过 100 个字符。 |`Test-Policy` |
|TemplateVersion |String |否 |表示待更新的策略版本。<br><br><br>* 如果待更新的参数是 `Title` 或 `Message`，您无需指定该参数。这两个参数与策略版本无关。<br><br>* 如果待更新的参数是不是 `Title` 和 `Message`，您必须指定该参数为 `draft`。参见文档开头的描述。 |`draft` |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

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
    "CertCheck": {
        "Switch": true,
        "CertInfoList": [
            {
                "CertId": "cert_hosting-1000034057"
            },
            {
                "CertId": "cert_hosting-1000009760"
            }
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


<span id="返回示例"></span>
### 返回示例

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
