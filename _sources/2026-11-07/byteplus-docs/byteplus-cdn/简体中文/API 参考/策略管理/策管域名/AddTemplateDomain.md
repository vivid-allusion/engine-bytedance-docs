---
title: "AddTemplateDomain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-addtemplatedomain-cn"
---

在 BytePlus CDN 中添加一个或者多个域名。在添加域名时，您必须指定一个已发布的分发策略，可选指定一个已发布的加密策略和规则引擎策略。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=AddTemplateDomain&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `AddTemplateDomain`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Domain |String |是 |表示一个或者多个要添加的域名。您最多可以指定 50 个域名，多个域名之间使用逗号（,）分隔。您添加的域名必须满足以下所有条件：<br><br><br>* 长度不超过 100 个字符。<br><br>* 不能包含大写字母。<br><br>* 不包含任意这些后缀：`zjgslb.com`，`yangyi19.com`，`volcgslb.com`，`veew-alb-cn1.com`，`bplgslb.com`，`bplslb.com`，`ttgslb.com`。<br><br><br>说明<br><br>需要留意的是，当您将您的域名与一个分发策略绑定时，策略中指定的回源地址不能与您的域名相同。 |`www.example.com,img.example.com` |
|ServiceTemplateId |String |是 |表示需要与该域名绑定的一个分发策略。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/describetemplates) 获取您想要绑定的分发策略的 ID。 |`tpl-s2Q4mq` |
|CertId |String |否 |表示一个证书的 ID。该证书是存放在 BytePlus 证书中心的，将与该域名关联。<br><br><br>* 如果 `HTTPSSwitch` 是 `on`，该参数必填。在使用该 API 前，您需要先授予 CDN 访问证书中心的权限，然后将您的证书上传到 BytePlus 证书中心以获取该证书的 ID。推荐您使用主账号授权 CDN 访问证书中心。<br><br>   您可以使用 [ListCertInfo](https://docs.byteplus.com/byteplus-cdn/reference/listcertinfo) 获取您想要关联的证书的 ID。<br><br>* 如果 `HTTPSSwitch` 是 `off`，该参数无效。 |`cert-044833503b2349b4b42c2e80b0aa8c23` |
|CipherTemplateId |String |否 |表示需要与该域名绑定的一个加密策略。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/describetemplates) 获取您想要绑定的加密策略的 ID。<br><br>如果不指定该参数，表示当前不会将该域名与任何加密策略绑定。 |`tpl-cqgRvW` |
|HTTPSSwitch |String |否 |表示是否为该域名启用 "HTTPS加密服务"。该参数有以下取值：<br><br><br>* `on`：表示启用该服务。<br><br>* `off`：表示不启用该服务。<br><br><br>该参数的默认值是 `off`。 |`on` |
|Project |String |否 |表示该域名所归属的项目，默认值是 `default`。 |`default` |
|ServiceRegion |String |否 |表示为该域名启用的服务区域。该参数有以下取值：<br><br><br>* `outside_chinese_mainland`：表示 "全球（不包含中国内地）"。<br><br>* `chinese_mainland`：表示 "中国内地"。<br><br>* `global`：表示 "全球"。<br><br><br>该参数的默认值是 `outside_chinese_mainland`。<br><br>需要留意的是，默认情况下 `chinese_mainland` 和 `global` 是不可用的。要使这两个服务区域可用，请 [提交工单](https://console.byteplus.com/workorder/create)。同时，由于这两个区域包含中国内地，您必须额外完成以下操作：<br><br><br>* 对您的 BytePlus 账号进行 [实名认证](https://docs.byteplus.com/en/byteplus-platform/docs/real-name-registration)<br><br>* 为您的域名进行 ICP 备案。 |`global` |
|Tags |Object[] |否 |表示一个标签列表。这些标签会被添加到 `Domain`。列表中最多可以包含 10 个标签。标签是一个键值对。 | |
|Key |String |否 |表示列表中一个标签的 key，长度范围是 1\-128 个字符。Key 是大小写敏感的，可以包含 Unicode 字母、Unicode 数字、空格以及以下任意字符：<br><br><br>* _./=+\-@ |`myKey` |
|Value |String |否 |表示该标签的值，长度范围是 1\-256 个字符。该参数也是大小写敏感的，可以包含 Unicode 字母、Unicode 数字、空格以及以下任意字符：<br><br><br>* _./=+\-@ |`myValue` |
|RuleTemplateIds |String[] |否 |表示需要与该域名绑定的一个规则引擎策略。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/describetemplates) 获取您想要绑定的规则引擎策略的 ID。<br><br>如果不指定该参数，表示当前不会将该域名与任何规则引擎策略绑定。 |`tpl-re9gvl6` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|ResourceIds |String[] |表示已添加的域名列表。 |`["www.example.com","img.example.com"]` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=AddTemplateDomain&Version=2021-03-01
{
    "Domain": "www.example.com,img.example.com",
    "CipherTemplateId": "tpl-cqgRvW",
    "HTTPSSwitch": "on",
    "ServiceRegion": "outside_chinese_mainland",
    "ServiceTemplateId": "tpl-s2Q4mq",
    "CertId": "cert-044833503b2349b4b42c2e80b0aa8c23",
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
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "2025082209311384D275C0D56FB6A17884",
        "Action": "AddTemplateDomain",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ResourceIds": [
            "www.example.com",
            "img.example.com"
        ]
    }
}
```


&nbsp;
