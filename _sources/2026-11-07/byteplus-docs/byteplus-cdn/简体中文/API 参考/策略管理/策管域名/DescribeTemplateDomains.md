---
title: "DescribeTemplateDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-describetemplatedomains-7f84f-cn"
---

获取符合过滤条件的域名列表。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeTemplateDomains&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeTemplateDomains`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Filters |Object[] |否 |表示一组过滤条件，用于获取符合条件的域名列表。如果您不指定任何过滤条件，该 API 则返回所有您账号下的域名。<br><br>多个过滤条件之间是 “与” 的关系，即只有满足所有过滤条件，一个域名才会包含在该 API 返回的域名列表中。<br><br>在该 API 的响应中，实际返回的域名列表受 `PageNum` 和 `PageSize` 的影响。 | |
|Fuzzy |Boolean |否 |表示匹配方式。该参数有以下取值：<br><br><br>* `true`：表示模糊匹配。在域名的匹配过程中，如果 `Name` 的对应值包含 `Value` 数组中的任意值，就域名就被认为是符合过滤条件。<br><br>* `false`：表示精确匹配。如果 `Name` 的对应值包含 `Value` 数组中值相同，该域名就被认为是符合过滤条件。<br><br><br>同时，您可以指定的 `Fuzzy` 值会受到 `Name` 值的影响。 参见 `Name` 的描述。<br><br>该参数的默认值是 `false`。 |`false` |
|Name |String |否 |表示过滤类型。该参数有以下取值：<br><br><br>* `TemplateTitle`：表示按绑定的策略的名称对域名进行过滤。<br><br>* `TemplateId`：表示按绑定的策略的 ID 对域名进行过滤。对于该参数值，`Fuzzy` 的值只能是 `false`。<br><br>* `TemplateType`：表示按绑定的策略的类型对域名进行过滤。对于该参数值，`Fuzzy` 的值只能是 `false`。<br><br>* `Domain`：表示按名称对域名进行过滤。<br><br>* `Status`：表示按状态对域名进行过滤。对于该参数值，`Fuzzy` 的值只能是 `false`。<br><br>* `HTTPSSwitch`：表示按 "HTTPS加密服务" 的状态对域名进行过滤。对于该参数值，`Fuzzy` 的值只能是 `false`。<br><br>* `WAFStatus`：表示按 "WAF防护" 的状态对域名进行过滤。对于该参数值，`Fuzzy` 的值只能是 `false`。<br><br><br>您可以同时指定多个过滤条件，但是不同过滤条件中的 `Name` 不能相同。 |`TemplateTitle` |
|Value |String[] |否 |表示 `Name` 对应的值，是一个数组。数组中的值用于与对象值匹配。如果对象值匹配数组中的任意值，就被认为是匹配。参数值在匹配时区分大小写。<br><br><br>* 当 `Name` 是 `TemplateTitle` 或 `Domain` 时，`Value` 中每个值的长度不能超过 100 个字符。另外，<br><br>   * 当 `Fuzzy` 是 `false` 时，`Value` 中可以包含多个值。<br><br>   * 当 `Fuzzy` 是 `true` 时，`Value` 中只能包含一个值。<br><br>* 当 `Name` 是 `TemplateId` 时，`Value` 中只能包含一个值。<br><br>* 当 `Name` 是 `TemplateType` 时，`Value` 中可以包含以下一个或者多个值：<br><br>   * `cipher`：表示加密策略。<br><br>   * `service`：表示分发策略。<br><br>* 当 `Name` 是 `Status` 时，`Value` 中可以包含以下某个值：<br><br>   * `online`：表示域名的状态是 "在线"。<br><br>   * `offline`：表示域名的状态是 "离线"。<br><br>   * `configuring`：表示域名的状态是 "配置中"。<br><br>* 当 `Name` 是 `HTTPSSwitch` 时，`Value` 中可以包含以下某个值：<br><br>   * `on`：表示 "HTTPS加密服务" 的状态是启用。<br><br>   * `off`：表示 "HTTPS加密服务" 的状态是禁用。<br><br>* 当 `Name` 是 `WAFStatus` 时，`Value` 中可以包含以某个值：<br><br>   * `on`：表示 "WAF防护" 的状态是启用。<br><br>   * `off`：表示 "WAF防护" 的状态是禁用。 |`["TestPolicy"]` |
|PageNum |Long |否 |对于返回的结果集，该参数表示一个页码，该 API 实际返回的域名是该页码所指定的分页上的那些域名。<br><br>该 API 返回的域名是根据 `PageSize` 而分页的。假设该 API 返回的域名数量是 100，您指定的 `PageSize` 是 `10`，那么返回的域名略是分布在 10 个页上。如果您指定的 `PageNum` 是 `2`，表示获取第 2 页上的那些域名。<br><br>如果您指定的分页上没有域名，则返回结果中 `Domains` 参数的值为 `null`。<br><br>`PageNum` 的默认值是 1。 |`1` |
|PageSize |Long |否 |表示每个分页包含的域名数量。<br><br>该参数的取值范围是 1\-200，默认值是 `10`。 |`10` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Domains |Object[] |表示该 API 返回的域名列表。<br><br>需要留意的是，列表中的域名是请求参数 `PageNum` 所表示的分页上的那些域名，不一定是所有符合过滤条件的域名。 | |
|CertInfo |Object |表示与 `Domain` 指定的域名关联的证书的信息。<br><br>如果 `HTTPSSwitch` 是 `off`，该参数值是 `null`。 | |
|CertId |String |表示与该域名关联的证书的 ID。该证书是托管在 BytePlus 证书中心的。 |`cert-044833503b2349b4b42a5e80b0aa8c23` |
|Source |String |证书来源。enums: cert_center、cdn_cert_hosting | |
|Cname |String |表示 CDN 分配给该域名的 CNAME。 |`www.example.com.bplslb.com` |
|Domain |String |表示 `Domains` 列表中的一个域名。 |`www.example.com` |
|HTTPSSwitch |String |表示该域名是否启用了 "HTTPS加密服务"。该参数有以下取值：<br><br><br>* `on`：表示该服务已启用。<br><br>* `off`：表示该服务已禁用。 |`off` |
|LockStatus |String |表示该域名是否被锁定。该参数有以下取值：<br><br><br>* `on`：表示该域名已被锁定。此时，您无法使用 [UpdateTemplateDomain](https://docs.byteplus.com/byteplus-cdn/reference/updatetemplatedomain-05d27) 修改该域名的配置。<br><br>* `off`：表示该域名未被锁定。 |`off` |
|Remark |String |表示该域名被锁定的原因。<br><br><br>* 如果 `LockStatus` 是 `on`，该参数表示锁定的原因。<br><br>* 如果 `LockStatus` 是 `off`，该参数值为空（""）。 |`This is a test.` |
|ServiceRegion |String |表示该域名启用的加速区域。该参数有以下取值<br><br><br>* `outside_chinese_mainland`：表示 "全球（不包含中国内地）"。<br><br>* `chinese_mainland`：表示 "中国内地"。<br><br>* `global`：表示 "全球"。 |`outside_chinese_mainland` |
|Status |String |表示该域名的状态。该参数有以下取值：<br><br><br>* `online`：表示状态是 "在线"。<br><br>* `offline`：表示状态是 "离线"。<br><br>* `configuring`：表示状态是 "配置中"。 |`online` |
|Templates |Object[] |表示与该域名绑定的策略列表。<br><br>一个域名必须也只能与一个分发策略绑定，可选与一个加密策略绑定。 | |
|TemplateId |String |表示一个策略的 ID。 |`tpl-s2DVaW` |
|Title |String |表示该策略的名称。 |`NetTVPlayer002` |
|Type |String |表示该策略的类型。该参数有以下取值：<br><br><br>* `cipher`：表示加密策略。<br><br>* `service`：表示分发策略。 |`service` |
|Exception |Boolean |表示该策略是否包含特殊配置。特殊配置指的是那些不由用户，而是由 BytePlus 工程师操作的配置。该参数有以下取值：<br><br><br>* `true`：表示包含特殊配置。<br><br>* `false`：表示不包含特殊配置。 |`false` |
|ProdVersion |String |表示该策略已发布版本的版本号。 |`P-250804.86120` |
|WAFStatus |String |表示该域名是否启用了 "WAF防护"。该参数有以下取值：<br><br><br>* `on`：表示 "WAF防护" 已启用。<br><br>* `off`：表示 "WAF防护" 已禁用。 |`off` |
|Project |String |表示该域名所归属的项目。 |`default` |
|Tags |Object[] |表示添加到 `Domain` 的标签列表。标签是一个键值对。如果 `Domain` 没有标签，该参数值是 `null`。 | |
|Key |String |表示列表中一个标签的 key。 |`myKey` |
|Value |String |表示该标签的值， |`myValue` |
|TotalCount |Long |表示符合过滤条件的域名的数量。该参数值不受 `PageSize` 和 `PageNum` 的影响。 |`1` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplateDomains&Version=2021-03-01
{
    "Filters": [
        {
            "Name": "Domain",
            "Value": [
                "example"
            ],
            "Fuzzy": true
        },
        {
            "Name": "TemplateTitle",
            "Value": [
                "NetTVPlayer"
            ],
            "Fuzzy": true
        },
        {
            "Name": "TemplateId",
            "Value": [
                "tpl-s2DVaW"
            ],
            "Fuzzy": false
        },
        {
            "Name": "TemplateType",
            "Value": [
                "service",
                "cipher"
            ],
            "Fuzzy": false
        },
        {
            "Name": "HTTPSSwitch",
            "Value": [
                "off"
            ],
            "Fuzzy": false
        },
        {
            "Name": "WAFStatus",
            "Value": [
                "off"
            ]
        },
        {
            "Name": "Status",
            "Value": [
                "online"
            ],
            "Fuzzy": false
        }
    ]
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20240305044725DD2386782EADAD775440",
        "Action": "DescribeTemplateDomains",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domains": [
            {
                "CertInfo": null,
                "Cname": "www.example.com.bplslb.com",
                "Domain": "www.example.com",
                "HTTPSSwitch": "off",
                "LockStatus": "off",
                "Project": "default",
                "Remark": "",
                "ServiceRegion": "outside_chinese_mainland",
                "Status": "online",
                "Templates": [
                    {
                        "Exception": false,
                        "TemplateId": "tpl-s2DVaW",
                        "Title": "NetTVPlayer002",
                        "Type": "service"
                    }
                ],
                "WAFStatus": "off",
                "Tags": [
                    {
                        "Key": "myKey1",
                        "Value": "myValue1"
                    },
                    {
                        "Key": "myKey2",
                        "Value": "myValue2"
                    }
                ]
            }
        ],
        "TotalCount": 1
    }
}
```


&nbsp;
