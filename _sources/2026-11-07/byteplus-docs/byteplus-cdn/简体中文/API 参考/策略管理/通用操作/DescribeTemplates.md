---
title: "DescribeTemplates"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-describetemplates-cn"
---

获取符合过滤条件的策略列表。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeTemplates&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeTemplates`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="request-body"></span>
### Request Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Filters |Object[] |否 |表示一组过滤条件，用于获取符合条件的策略列表。如果您不指定任何过滤条件，该 API 则返回所有您账号下的策略。<br><br>多个过滤条件之间是 “与” 的关系，即只有满足所有过滤条件，一个策略才会包含在该 API 返回的策略列表中。<br><br>在该 API 的响应中，实际返回的策略受 `PageNum` 和 `PageSize` 的影响。 | |
|Fuzzy |Boolean |否 |表示匹配方式。该参数有以下取值：<br><br><br>* `true`：表示模糊匹配。在策略的匹配过程中，如果 `Name` 的对应值包含 `Value` 数组中的任意值，该策略就被认为是符合过滤条件。<br><br>* `false`：表示精确匹配。如果 `Name` 的对应值与 `Value` 数组中的值相同，该策略就被认为是符合过滤条件。<br><br><br>同时，您可以指定的 `Fuzzy` 值会受到 `Name` 值的影响。 参见 `Name` 的描述。<br><br>该参数的默认值是 `false`。<br><br>需要留意的是，匹配过程是大小写敏感的。 |`true` |
|Name |String |否 |表示过滤类型。该参数有以下取值：<br><br><br>* `Title`：表示按名称对策略进行过滤。<br><br>* `Id`：表示按 ID 对策略进行过滤。对于该参数值，`Fuzzy` 的值只能是 `false`。<br><br>* `Domain`：表示按域名对绑定该域名的策略进行过滤。<br><br>* `Type`：表示按类型对策略进行过滤。对于该参数值，`Fuzzy` 的值只能是 `false`。<br><br>* `Status`：表示按状态对策略进行过滤。对于该参数值，`Fuzzy` 的值只能是 `false`。<br><br><br>您可以同时指定多个过滤条件，但是不同过滤条件中的 `Name` 不能相同。 |`Title` |
|Value |String[] |否 |表示 `Name` 对应的值，是一个数组。<br><br><br>* 当 `Name` 是 `Title`、`Id` 或 `Domain` 时，`Value` 数组中每个值的长度不能超过 100 个字符。<br><br>* 当 `Name` 是 `Type` 时，`Value` 数组中可以包含以下一个或者多个值：<br><br>   * `cipher`：表示加密策略。<br><br>   * `service`：表示分发策略。<br><br>   * `rule`：表示规则引擎策略。<br><br>* 当 `Name` 是 `Status` 时，`Value` 数组中可以包含以下一个或者多个值：<br><br>   * `locked`：表示状态是 "已发布"。<br><br>   * `editing`：表示状态是 "草稿"。<br><br><br>说明<br><br><br>* 当 `Fuzzy` 是 `false` 时，您可以在数组中指定多个值。<br><br>* 当 `Fuzzy` 是 `true` 时，您只能在数组中指定一个值。 |`["NetTVWeb001","NetTV003"]` |
|PageNum |Long |否 |对于 API 返回的策略列表，该参数表示一个页码。该 API 实际返回的策略是该页码所指定的分页上的那些策略。<br><br>该 API 返回的策略是根据 `PageSize` 而分页的。假设该 API 返回的策略数量是 100，您指定的 `PageSize` 是 `10`，那么返回的策略是分布在 10 个页上。如果您指定的 `PageNum` 是 `2`，表示获取第 2 页上的那些策略。<br><br>如果您指定的分页上没有策略，则返回结果中 `Templates` 参数的值为 `null`。<br><br>`PageNum` 的默认值是 `1`。 |`1` |
|PageSize |Long |否 |表示每个分页包含的策略数量。<br><br>该参数的取值范围是 1\-200，默认值是 `10`。 |`10` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Templates |Object[] |表示该 API 返回的策略列表。<br><br>需要留意的是，列表中的策略是请求参数 `PageNum` 所表示的分页上的那些策略，不一定是所有符合过滤条件的策略。 | |
|BoundDomains |Object[] |表示一个与 `TemplateId` 所指定的策略绑定的域名列表。<br><br>如果该策略未与任何域名绑定，该参数值为 `null`。 | |
|BoundTime |Long |表示该策略与 `Domain` 所指定的域名绑定的时间，格式是 Unix 时间戳。 |`1709174039` |
|Domain |String |表示一个与该策略绑定的域名。 |`www.example.com` |
|CreateTime |Long |表示该策略的创建时间，格式是 Unix 时间戳。 |`1709173909` |
|Message |String |表示该策略的描述。 |`This is a test` |
|Status |String |表示 `ProdVersion` 的状态，该参数有以下取值：<br><br><br>* `editing`：表示状态是 "草稿"。此时，`ProdVersion` 的值为空（""）。<br><br>* `locked`：表示状态是 "已发布"。 |`locked` |
|TemplateId |String |表示 API 返回的策略列表中一个策略的 ID。 |`tpl-sZRpwq` |
|Title |String |表示该策略的名称。 |`NetTVWeb001` |
|Type |String |表示该策略的类型。该参数有以下取值：<br><br><br>* `cipher`：表示加密策略。<br><br>* `service`：表示分发策略。<br><br>* `rule`：表示规则引擎策略。 |`cipher` |
|UpdateTime |Long |表示该策略的最近修改时间，格式是 Unix 时间戳。<br><br>如果该策略自创建后未被更新，该参数值与 `CreateTime` 的值相同。 |`1709174039` |
|Exception |Boolean |表示该策略是否包含特殊配置。特殊配置指的是那些不由用户，而是由 BytePlus 工程师操作的配置。该参数有以下取值：<br><br><br>* `true`：表示包含特殊配置。<br><br>* `false`：表示不包含特殊配置。 |`false` |
|Project |String |表示该策略所归属的项目。 |`default` |
|ProdVersion |String |表示该策略下已发布，也就是状态为 `running` 的版本。如果不存在状态为 `running` 的版本，该参数值为空（""）。 |`P-250411.32717` |
|DomainCount |Long |域名数量 | |
|TotalCount |Long |表示符合过滤条件的策略数量。该参数值不受 `PageSize` 和 `PageNum` 的影响。 |`2` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplates&Version=2021-03-01
{
    "Filters": [
        {
            "Name": "Title",
            "Fuzzy": false,
            "Value": [
                "NetTVWeb001",
                "NetTV003"
            ]
        },
        {
            "Name": "Id",
            "Fuzzy": false,
            "Value": [
                "tpl-sZRpwq",
                "tpl-sWm5EW"
            ]
        },
        {
            "Name": "Domain",
            "Fuzzy": true,
            "Value": [
                "example.com"
            ]
        },
        {
            "Name": "Type",
            "Fuzzy": false,
            "Value": [
                "cipher",
                "service"
            ]
        },
        {
            "Name": "Status",
            "Fuzzy": false,
            "Value": [
                "locked",
                "editing"
            ]
        }
    ]
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202403030536061418EF0E947E85EC76B6",
        "Action": "DescribeTemplates",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Templates": [
            {
                "BoundDomains": [
                    {
                        "BoundTime": 1709174039,
                        "Domain": "www.example.com"
                    }
                ],
                "CreateTime": 1709173909,
                "Exception": false,
                "Message": "",
                "Project": "default",
                "Status": "locked",
                "TemplateId": "tpl-sZRpwq",
                "Title": "NetTVWeb001",
                "Type": "service",
                "UpdateTime": 1709174039,
                "ProdVersion": "P-250411.32717"
            },
            {
                "BoundDomains": null,
                "CreateTime": 1709018409,
                "Exception": false,
                "Message": "Rewrite",
                "Project": "default",
                "Status": "editing",
                "TemplateId": "tpl-sWm5EW",
                "Title": "NetTV003",
                "Type": "service",
                "UpdateTime": 1709018409,
                "ProdVersion": ""
            }
        ],
        "TotalCount": 2
    }
}
```


&nbsp;
