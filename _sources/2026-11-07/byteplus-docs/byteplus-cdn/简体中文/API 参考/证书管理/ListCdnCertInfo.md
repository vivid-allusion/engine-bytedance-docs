---
title: "ListCdnCertInfo"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-listcdncertinfo-cn"
---

获取符合过滤条件的证书列表以及这些证书所关联的域名列表。

如果是子用户调用该 API，列表中的域名是该子用户有权限访问的。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=ListCdnCertInfo&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `ListCdnCertInfo`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|CertId |String |否 |表示一个证书的 ID，获取该 ID 的证书。<br><br>您可以使用 [ListCertInfo](https://docs.byteplus.com/zh-CN/byteplus-cdn/reference/listcertinfo) 获取您想要指定的证书的 ID。 |`cert-602fc4eb6cbf4b9351b54bedf2bc5dc5` |
|ConfiguredDomain |String |否 |表示一个域名列表，用于获取列表中每个域名所关联的证书。多个域名之间使用逗号（,）分隔。<br><br>列表中可以包含泛域名。但是需要留意的是，对于泛域名，只有当一个证书所关联域名中包含该泛域名，该证书才算符合 `ConfiguredDomain` 这个过滤条件。例如，您指定的 `ConfiguredDomain` 是 `*.example.com`。如果一个证书所关联的域名中有 `www.example.com`，但没有 `*.example.com`，那么该证书不符合这个过滤条件。 |`www.example.com,*.test.com` |
|DnsName |String |否 |表示一个域名列表，获取 SAN 字段中包含列表中任一域名的证书。多个域名之间使用逗号（,）分隔。<br><br>列表中可以包含泛域名。但是需要留意的是，对于泛域名，只有当一个证书的 SAN 字段中包含该泛域名，该证书才算符合 `DnsName` 这个过滤条件。例如，您指定的 `DnsName` 是 `*.example.com`。如果一个证书的 SAN 字段中有 `www.example.com`，但没有 `*.example.com`，那么该证书不符合这个过滤条件。 |`*.example.com,www.test.com` |
|PageNum |Long |否 |对于 API 返回的证书列表，该参数表示一个页码。该 API 实际返回的证书列表是该页码所指定的分页上的那些证书。<br><br>该 API 返回的证书是根据 `PageSize` 而分页的。假设该 API 返回的证书数量是 100，您指定的 `PageSize` 是 `10`，那么返回的证书是分布在 10 个页上。如果您指定的 `PageNum` 是 `2`，表示获取第 2 页上的那些证书。<br><br>如果您指定的分页上没有证书，则返回结果中 `CertInfo` 参数的值为 `null`。<br><br>`PageNum` 的默认值是 `1`。 |`1` |
|PageSize |Long |否 |表示每个分页包含的证书数量。<br><br>该参数的取值范围是 1\-100，默认值是 `10`。 |`10` |
|Source |String |否 |表示证书的存放位置，获取存放在该位置的证书。当前，该参数值只能是 `cert_center`，表示 BytePlus 证书中心。 |`cert_center` |
|Status |String |否 |表示一个证书状态的列表，获取处于列表中任一状态下的证书。该参数有以下取值：<br><br><br>* `running`：表示该证书的有效期大于 30 天。<br><br>* `expired`：表示该证书已经过期。<br><br>* `expiring_soon`：表示该证书的有效期小于等于 30 天，但还未过期。<br><br><br>多个证书状态使用逗号（,）分隔。 |`running,expird` |
|Configured |Boolean |否 |表示在该 API 返回的 `CertInfo` 中，是否移除未与任何域名关联的证书。该参数有以下取值：<br><br><br>* `true`：表示移除未与任何域名关联的证书。<br><br>* `false`：表示保留未与任何域名关联的证书。<br><br><br>该参数的默认值是 `true`。 |`true` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|PageNum |Long |表示请求参数中 `PageNum` 的值。 |`1` |
|PageSize |Long |表示请求参数中 `PageSize` 的值。 |`10` |
|Total |Long |表示符合过滤条件的证书数量。该参数值不受 `PageNum` 和 `PageSize` 的影响。 |`8` |
|CertInfo |Object[] |表示符合过滤条件的证书列表。如果没有符合过滤条件的证书，该参数值为 `null`。 | |
|Source |String |对于返回的证书列表中的一个证书，该参数表示该证书的存放位置。当前，该参数值是 `cert_center`，表示 BytePlus 证书中心。 |`cert_center` |
|CertId |String |表示该证书的 ID。 |`cert-602fc4eb6cbf4b9351b54bedf2bc5dc5` |
|CertName |String |表示该证书的 `Common Name (CN)` 字段中的内容。 |`*.example.com` |
|Status |String |表示该证书的状态。该参数有以下取值：<br><br><br>* `running`：表示该证书的有效期大于 30 天。<br><br>* `expired`：表示该证书已经过期。<br><br>* `expiring_soon`：表示该证书的有效期小于等于 30 天，但还未过期。 |`running` |
|EffectiveTime |Long |表示该证书的签发时间。单位是 Unix 时间戳。 |`1655856000` |
|ExpireTime |Long |表示该证书的过期时间。单位是 Unix 时间戳。 |`1687478399` |
|DnsName |String |表示该证书的 SAN 字段中的那些域名，多个域名之间使用逗号（,）分隔。 |`*.example.com,www.test.com` |
|ConfiguredDomain |String |表示已与该证书关联的域名列表。多个域名之间使用逗号（,）分隔。<br><br>如果请求参数 `Configured` 是 `false` 并且该证书未关联任何域名，那么该参数值为 `null`。 |`www.example.com,abc.example.com,img.example.com` |
|Desc |String |表示该证书的备注。 |`Test` |
|CertFingerprint |Object |表示该证书的指纹信息。 | |
|Sha1 |String |表示一个基于 SHA\-1 加密算法的指纹，由 40 个十六进制字符组成。 |`4f6c4bd5402e8f848837bf1334740ece0671ae4d` |
|Sha256 |String |表示一个基于 SHA\-256 加密算法的指纹，由 64 个十六进制字符组成。 |`24e49e0888f91a25f1503b452aa7cf0cf30da637810eaee5309b0be6c3931c9d` |
|ExpiringCount |Long |表示在符合过滤条件的证书中，状态是 `expiring_soon` 的证书的数量。但是，当前该参数还未生效，因此该参数值始终是 `0`。 |`0` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=ListCdnCertInfo&Version=2021-03-01
{
    "CertId": "cert-602fc4eb6cbf4b9351b54bedf2bc5dc5",
    "ConfiguredDomain": "www.example.com,*.test.com",
    "DnsName": "*.example.com,www.test.com",
    "Status": "running,expiring_soon",
    "Configured": true
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "2024031811030837EB957CFE06970AC404",
        "Action": "ListCdnCertInfo",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertInfo": [
            {
                "CertId": "cert-602fc4eb6cbf4b9351b54bedf2bc5dc5",
                "CertName": "*.example.com",
                "ConfiguredDomain": "*.example.com",
                "Desc": "Test",
                "DnsName": "*.example.com",
                "EffectiveTime": 1694415266,
                "ExpireTime": 1725951266,
                "Source": "cert_center",
                "Status": "running"
            }
        ],
        "ExpiringCount": 0,
        "PageNum": 1,
        "PageSize": 10,
        "Total": 1
    }
}
```
