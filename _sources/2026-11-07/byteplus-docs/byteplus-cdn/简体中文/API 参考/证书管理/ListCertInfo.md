---
title: "ListCertInfo"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-listcertinfo-cn"
---

获取符合过滤条件的证书信息。该 API 获取的证书是保存在 BytePlus 证书中心，并且能与或者已经与您账号下的域名关联的证书。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=ListCertInfo&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果您不指定 Body 中的某个非必填的参数，表示不使用该参数对证书进行过滤。</div>


<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `ListCertInfo`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Source |String |是 |表示证书存放的位置。当前该参数值只能是 `cert_center`，指 BytePlus 证书中心。 |`cert-center` |
|CertId |String |否 |表示一个证书 ID，获取该 ID 的证书。 |`cert-602fc4eb6cbf4b9351b54bedf2bc5dc5` |
|ConfiguredDomain |String |否 |表示一个域名列表，获取已与列表中任何一个域名绑定的证书。 |`www.example.com,www.test.com` |
|FuzzyMatch |Boolean |否 |当您指定了 `Name` 时，`FuzzyMatch` 表示在使用 `Name` 过滤证书时，CDN 使用的匹配方式。该参数有以下取值：<br><br><br>* `true`：表示模糊匹配。<br><br>* `false`：表示精确匹配。<br><br><br>如果您未指定 `Name`，`FuzzyMatch` 无效。<br><br>`FuzzyMatch` 的默认值是 `false`。 |`true` |
|Name |String |否 |表示一个域名，用于获取那些在 SAN 字段中包含该域名的证书。该域名可以是泛域名。例如，指定 `*.example.com` 表示获取 SAN 字段中包含 `img.example.com` 或 `www.example.com` 等匹配该泛域名的证书。 |`*.example.com` |
|PageNum |Long |否 |对于符合过滤条件的证书列表，该参数表示一个页码，该 API 实际展示的证书是该页码所指定的分页上的那些证书。<br><br>该 API 返回的证书是根据 `PageSize` 而分页的。假设该 API 返回的证书数量是 100，您指定的 `PageSize` 是 `10`，那么返回的证书是分布在 10 个页上。如果您指定的 `PageNum` 是 `2`，表示获取第 2 页上的那些证书。<br><br>如果您指定的分页上没有证书，则返回结果中 `CertInfo` 参数的值为 `null`。<br><br>`PageNum` 的默认值是 `1`。 |`1` |
|PageSize |Long |否 |表示每页包含的证书数量。<br><br>该参数的取值范围是 1\-100，默认值是 `10`。 |`10` |
|Status |String |否 |表示一个状态列表，获取处于列表中任意一个状态下的证书。多个状态之间使用逗号（,）分隔。该参数有以下取值：<br><br><br>* `running`：表示有效期大于 30 天的那些证书。<br><br>* `expired`：表示已过期的那些证书。<br><br>* `expiring_soon`：表示有效期小于等于 30 天但还未过期的那些证书。 |`expired,running` |
|SortRule |Object |否 |表示一个排序规则，对该 API 返回的证书进行排序。默认规则是按响应中的 `ExpireTime` 参数对返回的证书进行升序排序。 | |
|Asc |Boolean |否 |表示排序的方式。该参数有以下取值：<br><br><br>* `false`：表示对列表中的证书进行降序排列。<br><br>* `true`：表示对列表中的证书进行升序排列。<br><br><br>该参数的默认值是 `true`。 |`false` |
|OrderBy |String |否 |表示返回的证书按哪个字段进行排序。如果您指定了 SortRule，`OrderBy` 是必填。当前 `OrderBy` 的值必须是 `ExpireTime`，表示按证书的过期时间进行排序。 |`ExpireTime` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|PageNum |Long |表示您在请求参数中指定的 `PageNum`。 |`1` |
|PageSize |Long |表示您在请求参数中指定的 `PageSize`。 |`10` |
|Total |Long |表示符合过滤条件的证书数量。该参数值不受 `PageSize` 和 `PageNum` 的影响。 |`2` |
|CertInfo |Object[] |表示该 API 返回的证书列表。<br><br>需要留意的是，列表中的证书是请求参数 `PageNum` 所表示的分页上的那些证书，不一定是所有符合过滤条件的证书。 | |
|Source |String |对于返回的证书列表中的一个证书，该参数表示该证书存放的位置，有以下取值：<br><br><br>* `cert_center`：表示 BytePlus 证书中心。 |`cert_center` |
|CertId |String |表示该证书的 ID。 |`cert-602fc4eb6cbf4b9351b54bedf2bc5dc5` |
|CertName |String |表示该证书的 `Common Name (CN)` 字段中的内容。 |`*.example.com` |
|Status |String |表示该证书的状态。该参数有以下取值：<br><br><br>* `running`：表示该证书的有效期大于 30 天。<br><br>* `expired`：表示该证书已经过期。<br><br>* `expiring_soon`：表示该证书的有效期小于等于 30 天，但还未过期。 |`running` |
|EffectiveTime |Long |表示该证书的签发时间。单位是 Unix 时间戳。 |`1655856000` |
|ExpireTime |Long |表示该证书的过期时间。单位是 Unix 时间戳。 |`1687478399` |
|DnsName |String |表示该证书的 `SAN` 字段中包含的那些域名。多个域名之间使用逗号（,）分隔。 |`www.test.com,*.example.com` |
|Desc |String |表示该证书的备注。 |`Test` |
|ConfiguredDomain |String |表示已与该证书关联的域名列表。如果该证书还未与任何域名关联，该参数值为 `null`。 |`www.example.com, www.test.com` |
|CertFingerprint |Object |表示该证书的指纹信息。 | |
|Sha1 |String |表示一个基于 SHA\-1 加密算法的指纹，由 40 个十六进制字符组成。 |`4f6c4bd5402e8f848837bf1334740ece0671ae4d` |
|Sha256 |String |表示一个基于 SHA\-256 加密算法的指纹，由 64 个十六进制字符组成。 |`24e49e0888f91a25f1503b452aa7cf0cf30da637810eaee5309b0be6c3931c9d` |
|ExpiringCount |Long |表示在符合过滤条件的证书中，状态是 `expiring_soon` 的证书的数量。但是，当前该参数还未生效，因此该参数值始终是 `0`。 |`0` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=ListCertInfo&Version=2021-03-01
{
    "Source": "cert_center",
    "Name": "www.example.com",
    "Status": "running,expired",
    "SortRule": {
        "Asc": false,
        "OrderBy": "ExpireTime"
    }
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20240315094304D1302166C42C534627B0",
        "Action": "ListCertInfo",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertInfo": [
            {
                "CertId": "cert-7b94354335aa424993ce48fa355f1e5e",
                "CertName": "www.example.com",
                "ConfiguredDomain": "www.example.com",
                "Desc": "Test",
                "DnsName": "www.example.com",
                "EffectiveTime": 1708992000,
                "ExpireTime": 1740700799,
                "Source": "cert_center",
                "Status": "running"
            }
        ],
        "PageNum": 1,
        "PageSize": 10,
        "Total": 1
    }
}
```


&nbsp;
