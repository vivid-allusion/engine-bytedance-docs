---
title: "DescribeCertConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-describecertconfig-9ea17-cn"
---

对于可与指定证书关联的域名，获取这些域名的证书配置。这些域名在指定证书的 SAN 字段中并且已添加到 CDN 中。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeCertConfig&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeCertConfig`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|CertId |String |是 |表示一个证书 ID，获取关联了该证书的域名的证书配置。<br><br>您可以调用 [ListCdnCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-listcdncertinfo-cn) 获取证书的 ID。 |`cert-5dc4bfa90c1048778abf036b03ffabf2` |
|Status |String |否 |表示域名的状态，用于对该 API 返回的域名进行过滤。您可以指定多个状态，状态之间使用逗号（,）分隔。<br><br>该参数有以下取值：<br><br><br>* `online`：表示状态是 "运行中"。<br><br>* `offline`：表示状态是 "已下线"。<br><br>* `configuring`：表示状态是 "配置中"。<br><br><br>如果不指定该参数，表示不对域名进行过滤。 |`online,configuring` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|CertNotConfig |Object[] |表示可与 `CertId` 关联，但尚未关联任何证书的域名列表。 | |
|Domain |String |表示列表中的一个域名。 |`img.example.com` |
|Status |String |表示该域名的状态，有以下取值：<br><br><br>* `online`：表示状态是 "运行中"。<br><br>* `offline`：表示状态是 "已下线"。<br><br>* `configuring`：表示状态是 "配置中"。 |`offline` |
|DomainLock |Object |表示该域名是否被锁定。如果一个域名被锁定了，您无法修改其配置。 | |
|Remark |String |表示域名被锁定的原因。<br><br><br>* 如果 `DomainLock` 结构体中的 `Status` 是 `on`，该参数表示该域名被锁定的原因。<br><br>* 如果 `Status` 是 `off`，该参数的值是空（""）。 |`some reason` |
|Status |String |表示该域名的锁定状态。该参数有以下取值：<br><br><br>* `on`：表示该域名已被锁定。<br><br>* `off`：表示该域名未被锁定。 |`off` |
|SpecifiedCertConfig |Object[] |表示已与 `CertId` 关联的域名列表。 | |
|Domain |String |表示列表中的一个域名。 |`abc.example.com` |
|Status |String |表示该域名的状态。该参数有以下取值：<br><br><br>* `online`：表示状态是 "运行中"。<br><br>* `offline`：表示状态是 "已下线"。<br><br>* `configuring`：表示状态是 "配置中"。 |`configuring` |
|CerStatus |String |表示该域名关联的证书的状态。该参数有以下取值：<br><br><br>* `running`：表示证书的有效期大于 30 天。<br><br>* `expired`：表示证书已经过期。<br><br>* `expiring_soon`：表示证书的有效期小于等于 30 天，但还未过期。 |`expiring_soon` |
|DomainLock |Object |表示该域名是否被锁定。如果一个域名被锁定了，您无法修改其配置。 | |
|Remark |String |表示域名被锁定的原因。<br><br><br>* 如果 `DomainLock` 结构体中的 `Status` 是 `on`，该参数表示该域名被锁定的原因。<br><br>* 如果 `Status` 是 `off`，该参数的值是空（""）。 |`some reason` |
|Status |String |表示该域名的锁定状态。该参数有以下取值：<br><br><br>* `on`：表示该域名已被锁定。<br><br>* `off`：表示该域名未被锁定。 |`on` |
|OtherCertConfig |Object[] |表示可与 `CertId` 关联，但已关联了其他证书的域名列表。 | |
|Domain |String |表示列表中的一个域名。 |`www.example.com` |
|Status |String |表示该域名的状态，有以下取值：<br><br><br>* `online`：表示状态是 "运行中"。<br><br>* `offline`：表示状态是 "已下线"。<br><br>* `configuring`：表示状态是 "配置中"。 |`online` |
|CerStatus |String |表示该域名关联的证书的状态。该参数有以下取值：<br><br><br>* `running`：表示证书的有效期大于 30 天。<br><br>* `expired`：表示证书已经过期。<br><br>* `expiring_soon`：表示证书的有效期小于等于 30 天，但还未过期。 |`running` |
|DomainLock |Object |表示该域名是否被锁定。如果一个域名被锁定了，您无法修改其配置。 | |
|Remark |String |表示该域名被锁定的原因。<br><br><br>* 如果 `DomainLock` 结构体中的 `Status` 是 `on`，该参数表示锁定的原因。<br><br>* 如果 `Status` 是 `off`，该参数的值是空（""）。 |`some reason` |
|Status |String |表示该域名的锁定状态。该参数有以下取值：<br><br><br>* `on`：表示该域名已被锁定。<br><br>* `off`：表示该域名未被锁定。 |`off` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCertConfig&Version=2021-03-01
{
    "CertId": "cert-5dc4bfa90c1048778abf036b03ffabf2",
    "Status": "online,configuring"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202403181420252BCF8FD4581E1A5AAA4E",
        "Action": "DescribeCertConfig",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertNotConfig": [
            {
                "Domain": "abc.example.com",
                "DomainLock": {
                    "Remark": "",
                    "Status": "off"
                },
                "Status": "online"
            },
            {
                "Domain": "img.example.com.com",
                "DomainLock": {
                    "Remark": "",
                    "Status": "off"
                },
                "Status": "online"
            }
        ],
        "OtherCertConfig": [
            {
                "CerStatus": "running",
                "Domain": "doc.example.com",
                "DomainLock": {
                    "Remark": "",
                    "Status": "off"
                },
                "Status": "online"
            }
        ],
        "SpecifiedCertConfig": [
            {
                "CerStatus": "expiring_soon",
                "Domain": "www.example.com",
                "DomainLock": {
                    "Remark": "Domain locked against unauthorized changes. Acting administration on behalf of customer",
                    "Status": "on"
                },
                "Status": "online"
            }
        ]
    }
}
```
