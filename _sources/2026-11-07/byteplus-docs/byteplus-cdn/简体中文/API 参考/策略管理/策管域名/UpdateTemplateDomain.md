---
title: "UpdateTemplateDomain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-updatetemplatedomain-05d27-cn"
---

指定一个域名列表，修改列表中的域名配置。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">对于 <code>HTTPSwitch</code> 为 <code>on</code> 的域名，您一次只能修改一个。也就是说，您指定的域名列表中只能包含一个域名。</div>


* <div data-tips="true" data-tips-type="tip">如果您要同时修改多个域名的配置，必须满足以下所有条件：</div>


   * <div data-tips="true" data-tips-type="tip">在这些域名的当前配置中，<code>HTTPSSwitch</code> 都为 <code>off</code>。</div>


   * <div data-tips="true" data-tips-type="tip">在修改时不指定 <code>HTTPSSwitch</code> 或者在修改后的配置中，<code>HTTPSSwitch</code> 必须为 <code>off</code>。</div>


* <div data-tips="true" data-tips-type="tip">在使用该 API 时，如果您没有指定某个参数，在您提交 API 请求后，该参数的已有配置不会改变。</div>



<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=UpdateTemplateDomain&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">对于 Body 列表中的参数，如果您不指定某个参数，表示不修改指定域名的相应配置。</div>


<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `UpdateTemplateDomain`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Domains |String[] |是 |表示一个域名列表，修改它们的配置。<br><br>如果满足以下任意条件，您在列表中只能指定一个域名。<br><br><br>* 待修改的域名中存在一个域名，其已有的 `HTTPSSwitch` 设置为 `on`。<br><br>* 在调用该 API 时，您不指定 `HTTPSSwitch` 参数或者指定 `HTTPSSwitch` 为 `on`。 |`["www.example.com","abc.test.com"]` |
|CertId |String |否 |表示需要与 `Domains` 中的那个域名关联的证书的信息。<br><br><br>* 如果 `HTTPSSwitch` 是 `on`，该参数必填，表示需要与 `Domains` 中的那个域名关联的证书的 ID。该证书是存放在 BytePlus 证书中心的。<br><br>&nbsp;<br><br>   您可以使用 [ListCertInfo](https://docs.byteplus.com/byteplus-cdn/reference/listcertinfo) 获取您想要关联的证书的 ID。<br><br>* 如果 `HTTPSSwitch` 是 `off`，该参数无效。 |`cert-044833503b2349b4b42c2e80b0aa8c23` |
|CipherTemplateId |String |否 |表示一个加密策略。该加密策略会与 `Domains` 中的域名绑定。如果在调用该 API 时，`Domains` 中的域名已经绑定了加密策略，那么这些域名会先与已绑定的加密策略解绑，然后再与 `CipherTemplateId` 指定的加密策略绑定。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/describetemplates) 获取您想要绑定的加密策略的 ID。 |`tpl-cqgRvW` |
|HTTPSSwitch |String |否 |表示是否对 `Domains` 中的域名启用 "HTTPS加密服务"。该参数有以下取值：<br><br><br>* `on`：表示该服务已启用。<br><br>* `off`：表示该服务已禁用。<br><br><br>如果 `Domains` 中包含多个域名，`HTTPSSwitch` 必须为 `off`。 |`on` |
|ServiceRegion |String |否 |表示对 `Domains` 中的域名启用的服务区域。该参数有以下取值：<br><br><br>* `outside_chinese_mainland`：表示 "全球（不包含中国内地）"。<br><br>* `chinese_mainland`：表示 "中国内地"。<br><br>* `global`："表示 "全球"。<br><br><br>需要留意的是，`chinese_mainland` 和 `global` 默认不可用。要使用这两个服务区域，请 [提交工单](https://console.byteplus.com/workorder/create) 。同时，由于这两个区域包含中国内地，您必须额外完成以下操作：<br><br><br>* 对您的 BytePlus 账号进行 [实名认证](https://docs.byteplus.com/en/byteplus-platform/docs/real-name-registration)<br><br>* 为您的域名进行 ICP 备案。 |`outside_chinese_mainland` |
|ServiceTemplateId |String |否 |表示一个分发策略。该分发策略会与 `Domains` 中的域名绑定。如果在调用该 API 时，`Domains` 中的域名已经绑定了某个分发策略，那么这些域名会先与已绑定的分发策略解绑，然后再与 `ServiceTemplateId` 指定的分发策略绑定。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/describetemplates) 获取您想要绑定的分发策略的 ID。 |`tpl-s2Q4mq` |
|SparrowRules |Object[] |否 |表示一组边缘函数的转发规则。每条规则包含过滤条件配置以及操作配置。 | |
|Condition |Object |否 |表示当前规则中的过滤条件配置。 | |
|ConditionRule |Object[] |是 |表示一组过滤条件，用于对用户请求进行过滤。当前，您只能指定一个过滤条件。 | |
|Object |String |是 |表示过滤类型。该参数有以下取值：<br><br><br>* `filetype`：表示请求 URL 中的扩展名。<br><br>* `Directory`：表示请求 URL 中的某个目录。<br><br>* `path`：表示完整的请求 URL。 |`path` |
|Operator |String |是 |表示对比类型。该参数的值只能是 `match`，表示如果 `Value` 与请求中的 `Object` 相同，这个请求就满足该过滤条件。 |`match` |
|Type |String |是 |表示 `Object` 所属的对象。当前，该参数值只能是 `url`，表示 "请求 URL"。 |`url` |
|Value |String |是 |表示一个或者多个过滤值，总长度不能超过 1,024 个字符。多个过滤值之间使用分号（;）分隔。过滤值不能包含以下字符：<br><br><br>* 连续斜杠（//）、空格、美元符号（$）、问号（?）、Delete（ASCII code 127）。<br><br><br>另外，<br><br><br>* 如果 `Object` 是 `filetype`，每个过滤值表示一个请求 URL 后缀，无需以句点（.）开头，只能包含字母和数字。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，每个过滤值表示一个目录路径，以斜杠（/）开头和结尾。例如 `/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，每个过滤值表示一个 URL 路径，以斜杠（/）开头。每个过滤值中可以包含通配符（\*）表示一个或者多个字符。例如 `/chs/foods/local*sets;/us/birds/chickadee`。 |`/chs/foods/local*sets;/us/birds/chickadee` |
|Connective |String |是 |表示 `ConditionRule` 中各过滤条件之间的逻辑关系。当前，由于您只能指定一个过滤条件，该参数没有实际意义。 |`OR` |
|SparrowAction |Object |否 |表示当用户请求满足 `Condition` 时，CDN 所执行的操作的配置。 | |
|Action |String |否 |表示 CDN 执行的操作。当前，该参数值只能是 `Bypass`，表示 CDN 将用户请求交给 `SparrowID` 所指定的函数来处理。<br><br>该参数的默认值是 `Bypass`。 |`Bypass` |
|IgnoreCase |Boolean |否 |表示 `ConditionRule` 中的 `Value` 是否是大小写敏感的。该参数有以下取值：<br><br><br>* `true`：表示 `Value` 是大小写不敏感的。<br><br>* `false`：表示 `Value` 是大小写敏感的。<br><br><br>该参数的默认值是 `true`。 |`true` |
|SparrowID |String |否 |表示处理用户请求的函数的 ID。您可以调用 [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-cn) 获取 ID。 |`96ec5429956c42f79a717a4649f3d455` |
|SparrowSwitch |String |否 |表示是否启用 "边缘函数" 功能。如果您设置该参数，您在 `Domains` 中只能指定一个域名。<br><br>该参数有以下取值：<br><br><br>* `on`：表示启用该功能。<br><br>* `off`：表示不启用该功能。<br><br><br>该参数的默认值是 `off`。 |`on` |
|RuleMode |String |否 |规则策略修改模式，enums, append/override/delete，append表示追加，override表示覆盖, unbind表示解绑 | |
|RuleTemplateIds |String[] |否 |规则策略模板id列表 | |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=UpdateTemplateDomain&Version=2021-03-01
{
    "Domains": [
        "www.example.com"
    ],
    "CipherTemplateId": "tpl-cqgRvW",
    "HTTPSSwitch": "on",
    "ServiceRegion": "outside_chinese_mainland",
    "ServiceTemplateId": "tpl-s2Q4mq",
    "CertId": "cert-044833503b2345b4b42c2e81z0aa5c23",
    "SparrowRules": [
        {
            "Condition": {
                "ConditionRule": [
                    {
                        "Object": "filetype",
                        "Operator": "match",
                        "Type": "url",
                        "Value": "asp;php;jsp;ashx;aspx;do"
                    }
                ],
                "Connective": "OR"
            },
            "SparrowAction": {
                "Action": "bypass",
                "IgnoreCase": true,
                "SparrowID": "96ec5429956c42f79a717a4649f3d455"
            }
        }
    ],
    "SparrowSwitch": "on"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20210915182437010194100054410018B1",
        "Action": "UpdateTemplateDomain",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
