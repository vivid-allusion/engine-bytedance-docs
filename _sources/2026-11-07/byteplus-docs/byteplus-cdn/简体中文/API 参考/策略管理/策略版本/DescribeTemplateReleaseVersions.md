---
title: "DescribeTemplateReleaseVersions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_zh-cn"
---

获取指定策略的版本列表。您可以额外指定参数对版本列表进行过滤和排序。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">每个策略最多记录 50 个已发布的版本。</div>


<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeTemplateReleaseVersions&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeTemplateReleaseVersions`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|TemplateId |String |是 |表示要获取版本列表的策略 ID。 |`tpl-s18ynd9` |
|Filters |Object[] |否 |表示一个过滤条件列表，最多包含 10 个条件。 | |
|Name |String |否 |表示过滤对象。该参数有以下取值：<br><br><br>* `Status`：表示指定策略状态对版本列表进行过滤。<br><br>* `Version`：表示指定版本号对版本列表进行过滤。 |`Status` |
|Value |String[] |否 |表示过滤值列表。<br><br><br>* 当 `Name` 是 `Status` 时，您可以指定以下过滤值中一个或者多个：<br><br>   * `stop`：表示状态是 "暂停"。<br><br>   * `running`：表示状态是 "运行中"。<br><br>   * `draft`：表示状态是 "草稿"。<br><br>* 当 `Name` 是 `Version` 时，您可以指定一个或者多个版本号，最多 10 个。 |`["stop","running"]` |
|Fuzzy |Boolean |否 |表示匹配方式。该参数值只能是 `false`，表示精确匹配。<br><br>该参数的默认值是 `false`。 |`false` |
|SortRule |Object |否 |表示排序规则。 | |
|OrderBy |String |否 |表示排序对象。该参数有以下取值：<br><br><br>* `CreateTime`：表示版本的创建时间。<br><br>* `ReleaseTime`：表示版本最近发布的时间。<br><br>* `Version`：表示版本号。 |`CreateTime` |
|Asc |Boolean |否 |表示排序顺序，该参数有以下取值：<br><br><br>* `false`：表示按降序排序。<br><br>* `true`：表示按升序排序。<br><br><br>该参数的默认值是 `false`。 |`false` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Total |Long |表示符合过滤条件的版本数量。 |`10` |
|Versions |Object[] |表示符合条件的版本列表。 | |
|Version |String |表示列表中一个版本的版本号。<br><br><br>* 如果 `Status` 为 `draft`，版本号为 `draft`。<br><br>* 如果 `Status` 不是 `draft`，版本号是一个字符串，命名规范是 `P-<first_publish_date>-<random_5_digits>`。 |`P-250414.89520` |
|CreateTime |Long |表示该版本的创建时间，格式为 Unix 时间戳。 |`1744610623` |
|Env |String |表示该版本的发布环境。<br><br><br>* 如果 `Status` 不是 `draft`，该参数值始终是 `prod`，表示线上环境。<br><br>* 如果 `Status` 是 `draft`，该参数值是空（""）。 |`prod` |
|Message |String |表示该版本的描述。 |`my desc` |
|ReleaseTime |Long |表示该版本最近一次的发布时间，格式为 Unix 时间戳。 |`1744610623` |
|Status |String |表示该版本的状态。<br><br><br>* `stop`：表示状态是 "暂停"。<br><br>* `running`：表示状态是 "运行中"。<br><br>* `draft`：表示状态是 "草稿"。 |`stop` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplateReleaseVersions&Version=2021-03-01
{
    "TemplateId": "tpl-s18ynd9",
    "Filters": [
        {
            "Name": "Status",
            "Value": [
                "stop",
                "running",
                "draft"
            ]
        }
    ],
    "SortRule": {
        "OrderBy": "CreateTime",
        "Asc": true
    }
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202504140728216B5EA730EF294C000118",
        "Action": "DescribeTemplateReleaseVersions",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Total": 3,
        "Versions": [
            {
                "CreateTime": 1744361302,
                "Env": "prod",
                "Message": "aaa",
                "ReleaseTime": 1744613891,
                "Status": "running",
                "Version": "P-250411.16282"
            },
            {
                "CreateTime": 1744364788,
                "Env": "prod",
                "Message": "sdfgh",
                "ReleaseTime": 1744599039,
                "Status": "stop",
                "Version": "P-250414.89520"
            },
            {
                "CreateTime": 1744610623,
                "Env": "",
                "Message": "",
                "ReleaseTime": 1744610623,
                "Status": "draft",
                "Version": "draft"
            }
        ]
    }
}
```


&nbsp;
