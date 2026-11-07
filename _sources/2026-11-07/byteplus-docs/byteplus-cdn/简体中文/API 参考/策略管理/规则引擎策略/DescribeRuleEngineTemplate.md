---
title: "DescribeRuleEngineTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeRuleEngineTemplate_zh-cn"
---

获取一个规则引擎策略的配置详情。


* 如果该策略已发布，API 默认返回的是该策略下已发布，也就是状态为 `running` 的版本配置详情。

* 如果该策略未发布，API 默认返回的是该策略下状态为 `draft` 的版本配置详情。


您也可以指定该策略下的某个版本，获取该版本的配置详情。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeRuleEngineTemplate&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeRuleEngineTemplate`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|TemplateId |String |是 |表示您要查询的规则引擎策略的 ID。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-describetemplates-cn) 获取您想要查询的规则引擎策略的 ID。 |`tpl-sZRpwq` |
|TemplateVersion |String |否 |表示该策略下的一个版本，API 返回该版本的配置详情。<br><br>该参数的默认值如下：<br><br><br>* 如果该策略已发布，该参数的默认值是策略下已发布，也就是状态为 `running` 的版本。<br><br>* 如果该策略未发布，该参数的默认值为 `draft`。<br><br><br>您可以调用 [DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_zh-cn) 获取该策略下的所有版本。 |`P-250414.89520` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|BoundDomains |Object[] |对于 `TemplateId` 所指定的规则引擎策略，该参数表示与该策略绑定的域名列表。<br><br>如果该规则引擎策略未与任何域名绑定，该参数值为 `null`。 | |
|BoundTime |Long |表示该规则引擎策略与 `Domain` 所指定的域名绑定的时间，格式是 Unix 时间戳。 |`1709174039` |
|Domain |String |表示一个与该规则引擎策略绑定的域名。 |`www.example.com` |
|CreateTime |Long |表示该规则引擎策略的创建时间，格式是 Unix 时间戳。 |`1709173909` |
|Exception |Boolean |表示该规则引擎策略中是否存在特殊配置。如果特殊配置存在，您无法将该策略与域名绑定，请 [提交工单](https://console.byteplus.com/workorder/create)。<br><br>该参数有以下取值：<br><br><br>* `true`：表示存在特殊配置。<br><br>* `false`：表示不存在特殊配置。 |`false` |
|Message |String |表示该规则引擎策略的描述。 |`This is a test` |
|ProdVersion |String |表示该规则引擎策略下已发布，也就是状态为 `running` 的版本。如果不存在状态为 `running` 的版本，该参数值为空（""）。 |`P-250414.89520` |
|Project |String |表示该规则引擎策略所属的项目。 |`default` |
|Rule |String |表示规则的内容。您需要反序列化规则内容以提取规则配置。关于规则配置的描述，参见 [UpdateRuleEngineTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateRuleEngineTemplate_zh-cn) 中 `Rule` 参数的描述。 | |
|Status |String |表示该规则引擎策略的状态。该参数有以下取值：<br><br><br>* `locked`：表示状态是 "已发布"。对于已发布的规则引擎策略，您无法修改其配置。<br><br>* `editing`：表示状态是 "草稿"。 |`locked` |
|TemplateId |String |表示该规则引擎策略的 ID。 |`tpl-sZRpwq` |
|Title |String |表示该规则引擎策略的名称。 |`NetTVWeb001` |
|Type |String |表示该规则引擎策略的类型。该参数值始终是 `rule`。 |`rule` |
|UpdateTime |Long |表示该规则引擎策略的最近修改时间，格式是 Unix 时间戳。<br><br>如果该规则引擎策略自创建后未被修改，该参数值与 `CreateTime` 的值相同。 |`1709173909` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeRuleEngineTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-rejjo23",
    "TemplateVersion": "draft"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "2025053003420680999F0B12D54B0FB5C8",
        "Action": "DescribeRuleEngineTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "BoundDomains": null,
        "CreateTime": 1748241181,
        "Exception": false,
        "Message": "test",
        "ProdVersion": "",
        "Project": "default",
        "Rule": "{\"IfBlock\":{\"Condition\":{\"IsGroup\":true,\"Connective\":\"and\",\"ConditionGroups\":[{\"IsGroup\":true,\"Connective\":\"and\",\"ConditionGroups\":[{\"IsGroup\":false,\"Connective\":\"and\",\"Condition\":{\"Object\":\"always\"}}]}]},\"Actions\":[{\"Action\":\"redirect_request\",\"Stage\":\"client_request\",\"Phase\":1,\"Module\":1,\"Groups\":[{\"Dimension\":\"redirect_request\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"source_path\",\"Values\":[\"^/docs/file1$\"]},{\"Name\":\"status_code\",\"Values\":[\"301\"]},{\"Name\":\"protocol\",\"Values\":[\"follow_client\"]},{\"Name\":\"target_host\",\"Values\":[\"www.example.com\"]},{\"Name\":\"target_path\",\"Values\":[\"^/cos1/file2$\"]},{\"Name\":\"target_query_action\",\"Values\":[\"include_all\"]}]}]}]},{\"Action\":\"allow_access\",\"Stage\":\"client_request\",\"Phase\":1,\"Module\":1,\"Groups\":[{\"Dimension\":\"allow_access\",\"GroupParameters\":[{}]}]},{\"Action\":\"download_speed_limit\",\"Stage\":\"client_request\",\"Phase\":1,\"Module\":1,\"Groups\":[{\"Dimension\":\"download_speed_limit\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"rate\",\"Values\":[\"100\"]},{\"Name\":\"rate_unit\",\"Values\":[\"B/s\"]},{\"Name\":\"after_size\",\"Values\":[\"15\"]},{\"Name\":\"after_size_unit\",\"Values\":[\"MB\"]}]}]}]},{\"Action\":\"request_header\",\"Stage\":\"client_request\",\"Phase\":1,\"Module\":1,\"Groups\":[{\"Dimension\":\"request_header\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"action\",\"Values\":[\"set\"]},{\"Name\":\"header_name\",\"Values\":[\"myheader\"]},{\"Name\":\"header_value\",\"Values\":[\"myvalue\"]}]},{\"Parameters\":[{\"Name\":\"action\",\"Values\":[\"delete\"]},{\"Name\":\"header_name\",\"Values\":[\"myheader\"]}]}]}]},{\"Action\":\"deny_access\",\"Stage\":\"client_request\",\"Phase\":1,\"Module\":1,\"Groups\":[{\"Dimension\":\"deny_access\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"status_code\",\"Values\":[\"465\"]}]}]}]},{\"Action\":\"cache_key\",\"Stage\":\"cache\",\"Phase\":5,\"Module\":2,\"Groups\":[{\"Dimension\":\"query_string\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"query_action\",\"Values\":[\"exclude_part\"]},{\"Name\":\"query_names\",\"Values\":[\"myparam1\",\"myparam2\"]},{\"Name\":\"ignore_case\",\"Values\":[\"true\"]}]},{\"Parameters\":[{\"Name\":\"query_action\",\"Values\":[\"include_part\"]},{\"Name\":\"query_names\",\"Values\":[\"ff\"]},{\"Name\":\"ignore_case\",\"Values\":[\"true\"]}]},{\"Parameters\":[{\"Name\":\"query_action\",\"Values\":[\"include_all\"]},{\"Name\":\"ignore_case\",\"Values\":[\"true\"]}]},{\"Parameters\":[{\"Name\":\"query_action\",\"Values\":[\"exclude_all\"]}]}]},{\"Dimension\":\"request_header\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"header_names\",\"Values\":[\"myheader\",\"myheader2\"]},{\"Name\":\"ignore_case\",\"Values\":[\"true\"]}]}]},{\"Dimension\":\"request_path\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"source_path\",\"Values\":[\"^/path1/$\"]},{\"Name\":\"target_path\",\"Values\":[\"^/path2/$\"]}]}]},{\"Dimension\":\"path_ignore_case\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"ignore_case\",\"Values\":[\"true\"]}]}]}]},{\"Action\":\"compression\",\"Stage\":\"cache\",\"Phase\":5,\"Module\":2,\"Groups\":[{\"Dimension\":\"compression\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"methods\",\"Values\":[\"gzip\",\"brotli\"]},{\"Name\":\"min_file_size\",\"Values\":[\"563\"]},{\"Name\":\"min_file_size_unit\",\"Values\":[\"KB\"]},{\"Name\":\"format\",\"Values\":[\"default\"]}]}]}]},{\"Action\":\"video_drag\",\"Stage\":\"cache\",\"Phase\":5,\"Module\":2,\"Groups\":[{\"Dimension\":\"video_drag\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"switch\",\"Values\":[\"true\"]}]}]}]},{\"Action\":\"cache_time\",\"Stage\":\"cache\",\"Phase\":5,\"Module\":2,\"Groups\":[{\"Dimension\":\"cache_time\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"ttl\",\"Values\":[\"56\"]},{\"Name\":\"ttl_unit\",\"Values\":[\"day\"]},{\"Name\":\"cache_policy\",\"Values\":[\"origin_first\"]},{\"Name\":\"replenish\",\"Values\":[\"true\"]}]}]}]},{\"Action\":\"origin_range\",\"Stage\":\"origin_request\",\"Phase\":2,\"Module\":2,\"Groups\":[{\"Dimension\":\"origin_range\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"switch\",\"Values\":[\"true\"]}]}]}]},{\"Action\":\"origin_follow\",\"Stage\":\"origin_request\",\"Phase\":2,\"Module\":2,\"Groups\":[{\"Dimension\":\"origin_follow\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"switch\",\"Values\":[\"true\"]}]}]}]},{\"Action\":\"origin_tcp_timeout\",\"Stage\":\"origin_request\",\"Phase\":2,\"Module\":2,\"Groups\":[{\"Dimension\":\"origin_tcp_timeout\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"connect_timeout\",\"Values\":[\"56\"]},{\"Name\":\"connect_timeout_unit\",\"Values\":[\"sec\"]}]}]}]},{\"Action\":\"origin_http_timeout\",\"Stage\":\"origin_request\",\"Phase\":2,\"Module\":2,\"Groups\":[{\"Dimension\":\"origin_http_timeout\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"read_timeout\",\"Values\":[\"58\"]},{\"Name\":\"read_timeout_unit\",\"Values\":[\"sec\"]}]}]}]}]},\"ElseBlock\":{\"Actions\":[{\"Action\":\"redirect_protocol\",\"Stage\":\"client_request\",\"Phase\":1,\"Module\":1,\"Groups\":[{\"Dimension\":\"redirect_protocol\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"status_code\",\"Values\":[\"301\"]},{\"Name\":\"protocol\",\"Values\":[\"https\"]}]}]}]}]}}",
        "Status": "editing",
        "TemplateId": "tpl-rejjo23",
        "Title": "rules-actions",
        "Type": "rule",
        "UpdateTime": 1748241181
    }
}
```


&nbsp;
