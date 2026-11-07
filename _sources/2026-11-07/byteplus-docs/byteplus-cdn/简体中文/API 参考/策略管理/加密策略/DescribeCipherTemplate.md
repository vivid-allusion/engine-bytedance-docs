---
title: "DescribeCipherTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-describeciphertemplate-f8c12-cn"
---

获取一个加密策略的配置详情。


* 如果该策略已发布，API 默认返回的是该策略下已发布，也就是状态为 `running` 的版本配置详情。

* 如果该策略未发布，API 默认返回的是该策略下状态为 `draft` 的版本配置详情。


您也可以指定该策略下的某个版本，获取该版本的配置详情。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeCipherTemplate&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeCipherTemplate`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="request-body"></span>
### Request Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|TemplateId |String |是 |表示您要查询的加密策略的 ID。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-describetemplates-cn) 获取您想要查询的加密策略的 ID。 |`tpl-c2PRDW` |
|TemplateVersion |String |否 |表示该策略下的一个版本，API 返回该版本的配置详情。<br><br>该参数的默认值如下：<br><br><br>* 如果该策略已发布，该参数的默认值是策略下已发布，也就是状态为 `running` 的版本。<br><br>* 如果该策略未发布，该参数的默认值为 `draft`。<br><br><br>您可以调用 [DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_zh-cn) 获取该策略下的所有版本。 |`P-250414.89520` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|BoundDomains |Object[] |对于 `TemplateId` 所指定的加密策略，该参数表示一个与该加密策略绑定的域名列表。<br><br>如果该策略未与任何域名绑定，该参数值为 `null`。 | |
|BoundTime |Long |表示该加密策略与 `Domain` 所指定的域名绑定的时间，格式是 Unix 时间戳。 |`1709174039` |
|Domain |String |表示一个与该加密策略绑定的域名。 |`www.example.com` |
|CreateTime |Long |表示该域名的创建时间，格式是 Unix 时间戳。 |`1636612244` |
|HTTPS |Object |表示 HTTPS 加密服务的配置。 | |
|DisableHttp |Boolean |表示是否允许请求 URL 中 Scheme 是 `HTTP` 的请求。该参数有以下取值：<br><br><br>* `true`：表示允许 Scheme 是 `HTTP` 的请求。<br><br>* `false`：表示不允许 Scheme 是 `HTTP` 的请求。 |`false` |
|ForcedRedirect |Object |表示 "HTTP 强制跳转到 HTTPS" 特性的配置。<br><br>说明<br><br>CDN 提供了两种协议重定向的特性。<br><br><br>* HTTP 重定向到 HTTPS，也就是 `ForcedRedirect` 特性。<br><br>* HTTPS 重定向到 HTTP，也就是 `HttpForcedRedirect` 特性。<br><br><br>这两个协议重定向特性是互斥的。也就是说，其中一个特性启用了，另一个就不能启用。 | |
|EnableForcedRedirect |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。启用后，CDN 会将收到的 HTTP 请求重定向到 HTTPS 请求。<br><br>* `false`：表示禁用该特性。禁用后，CDN 不会将 HTTP 请求重定向到 HTTPS 请求。 |`true` |
|StatusCode |String |表示当收到 HTTPS 请求时 CDN 的重定向响应状态码。该参数有以下取值：<br><br><br>* `301`：表示返回的状态码是 301。<br><br>* `302`：表示返回的状态码是 302。 |`301` |
|HTTP2 |Boolean |表示是否为用户请求启用 HTTP/2 支持。该参数有以下取值：<br><br><br>* `true`：表示启用 HTTP/2。<br><br>* `false`：表示禁用 HTTP/2。 |`true` |
|Hsts |Object |表示 HSTS 特性的配置。 | |
|Subdomain |String |表示 HSTS 配置是否也应用于域名的子域名。该参数有以下取值：<br><br><br>* `include`：表示 HSTS 配置应用于子域名站点。<br><br>* `exclude`：表示 HSTS 配置不应用于子域名站点。 |`include` |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|Ttl |Long |表示 `Strict-Transport-Security` 响应头在浏览器中的缓存过期时间，单位是秒。<br><br>如果该参数值为 `0`，其效果等同于禁用 HSTS 设置。 |`300` |
|OCSP |Boolean |表示是否启用 "OCSP 装订" 特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|TlsVersion |String[] |表示 "TLS 版本" 特性的配置。该参数指定用户请求可以使用的 TLS 版本，有以下取值：<br><br><br>* `tlsv1.0`：表示 TLS 1.0。<br><br>* `tlsv1.1`：表示 TLS 1.1。<br><br>* `tlsv1.2`：表示 TLS 1.2。<br><br>* `tlsv1.3`：表示 TLS 1.3。、 |`["tlsv1.1","tlsv1.2"]` |
|CertCheck |Object |表示 "访问双向认证" 特性的配置。 | |
|CertInfoList |Object[] |表示一个 CA 证书列表。列表中最多包含两个 CA 证书。这些 CA 证书必须是已经托管在 CDN 的。CA 证书使用的加密算法可以是 RSA 或者 ECC。 | |
|CertId |String |表示一个 CA 证书的 ID。ID 是以 `cert_hosting-` 开头的。 |`cert_hosting-31869` |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。<br><br><br>该参数的默认值是 `false`。 |`true` |
|HttpForcedRedirect |Object |表示 "HTTPS 强制跳转到 HTTP" 特性的配置。 | |
|EnableForcedRedirect |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。启用后，CDN 会将收到的 HTTPS 请求重定向到 HTTP 请求。<br><br>* `false`：表示禁用该特性。CDN 不会将 HTTPS 请求重定向到 HTTP 请求。 |`true` |
|StatusCode |String |表示当收到 HTTPS 请求时，CDN 返回的重定向状态码。该参数有以下取值：**301**、**302**、**303**、**307**、**308**。<br><br>需要留意的是：<br><br><br>* 对于 301 和 302，如果原请求使用的方法不是GET，那么客户端向新的URL发送请求时，新请求使用的方法可能变成 GET。<br><br>* 对于 303，新请求使用的方法是 GET。<br><br>* 对于 307 和 308，新请求使用的方法与原请求相同，不会被改变。 |`302` |
|Message |String |表示该加密策略的描述。 |`Test` |
|Quic |Object |表示 QUIC 配置。 | |
|Switch |Boolean |表示是否为用户请求启用 QUIC。该参数有以下取值：<br><br><br>* `true`：表示启用 QUIC。<br><br>* `false`：表示禁用 QUIC。 |`true` |
|Status |String |表示该域名的状态。该参数有以下取值：<br><br><br>* `online`：表示状态是 正常运行。<br><br>* `configuring`：表示状态是 配置中。<br><br>* `offline`：表示状态是 已下线。 |`offline` |
|TemplateId |String |表示该加密策略的 ID。 |`tpl-c2PRDW` |
|Title |String |表示该加密策略的名称。 |`Standard` |
|Type |String |表示该加密策略的类型。该参数值始终是 `cipher`。 |`cipher` |
|UpdateTime |Long |表示该域名配置的最近更新时间，格式是 Unix 时间戳。如果该域名配置在创建后未被更新，该参数值与 `CreateTime` 的值相同。 |`1639621409` |
|Exception |Boolean |表示该加密策略是否包含特殊配置。特殊配置指的是那些不由用户，而是由 BytePlus 工程师操作的配置。该参数有以下取值：<br><br><br>* `true`：表示包含特殊配置。<br><br>* `false`：表示不包含特殊配置。 |`false` |
|Project |String |表示该域名归属的项目。 |`default` |
|ProdVersion |String |表示该策略下已发布，也就是状态为 `running` 的版本。如果不存在状态为 `running` 的版本，该参数值为空（""）。 |`P-250414.89520` |
|DomainCount |Long |域名数量 | |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCipherTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-c57pd62"
}
```


<span id="返回示例"></span>
### 返回示例

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
