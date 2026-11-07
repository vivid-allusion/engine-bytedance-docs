---
title: "ListSharedConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_cn"
---

基于您指定的查询条件，获取符合条件的全局配置列表。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=ListSharedConfig&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `ListSharedConfig`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|ConfigName |String |否 |表示一个全局配置的名称，用来获取精确匹配该名称的全局配置。 |`my_list` |
|ConfigType |String |否 |表示一个全局配置的类型，用来获取该类型的全局配置列表。该参数有以下取值：<br><br><br>* `deny_ip_access_rule`：表示 IP 黑名单。<br><br>* `allow_ip_access_rule`：表示 IP 白名单。<br><br>* `4xx_error_page`: 表示自定义错误页面。<br><br>* `deny_referer_access_rule`：表示 Referer 黑名单。<br><br>* `allow_referer_access_rule`：表示 Referer 白名单。<br><br>* `common_match_list`：表示通用列表。 |`allow_ip_access_rule` |
|PageNum |Long |否 |表示一个页码。CDN 根据 `PageSize`，对符合查询条件的全局配置列表进行分页。假设该 API 返回的全局配置的数量是 100，`PageSize` 是 `10`，那么这些全局配置分布在 10 个页上。CDN 默认展示第 1 页上的全局配置。<br><br>该参数的默认值是 `1`。 |`1` |
|PageSize |Long |否 |表示每页包含的全局配置数量。<br><br>该参数的取值范围是 1\-1,000，默认值是 `10`。 |`10` |
|Project |String |否 |表示一个项目名称，用来获取归属该项目的全局配置列表。 |`default` |
|ConfigTypeList |String[] |否 |表示一个或多个全局配置的类型，用来获取这些类型的全局配置列表。该参数值可以是 `ConfigType` 可用值的组合。`ConfigType` 与 `ConfigTypeList` 不能同时指定。 |`["allow_ip_access_rule","deny_ip_access_rule"]` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|ConfigData |Object[] |表示符合查询条件的全局配置列表。 | |
|ConfigName |String |表示列表中的一个全局配置的名称。 |`my_list` |
|ConfigType |String |表示该全局配置的类型。该参数有以下取值：<br><br><br>* `deny_ip_access_rule`：表示 IP 黑名单。<br><br>* `allow_ip_access_rule`：表示 IP 白名单。<br><br>* `4xx_error_page`: 表示自定义错误页面。<br><br>* `deny_referer_access_rule`：表示 Referer 黑名单。<br><br>* `allow_referer_access_rule`：表示 Referer 白名单。<br><br>* `common_match_list`：表示通用列表。 |`deny_ip_access_rule` |
|DomainCount |Long |表示与该全局配置关联的域名数量。 |`2` |
|Project |String |表示该全局配置所归属的项目。 |`default` |
|UpdateTime |Long |表示该全局配置的最近修改时间，单位是 Unix 时间戳。 |`1655856000` |
|PageNum |Long |表示您在请求参数中指定的 `PageNum`。 |`1` |
|PageSize |Long |表示您在请求参数中指定的 `PageSize`。 |`10` |
|Total |Long |表示符合查询条件的全局配置总数。 |`20` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=ListSharedConfig&Version=2021-03-01
{
    "ConfigType": "allow_ip_access_rule"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20240117195639014D4059167D42B2C640",
        "Action": "ListSharedConfig",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ConfigData": [
            {
                "ConfigName": "deny_ip",
                "ConfigType": "deny_ip_access_rule",
                "DomainCount": 0,
                "Project": "default",
                "UpdateTime": 1705492181
            },
            {
                "ConfigName": "error_page",
                "ConfigType": "4xx_error_page",
                "DomainCount": 1,
                "Project": "default",
                "UpdateTime": 1705334019
            },
            {
                "ConfigName": "common_list",
                "ConfigType": "common_match_list",
                "DomainCount": 0,
                "Project": "default",
                "UpdateTime": 1705332721
            },
            {
                "ConfigName": "deny_referer",
                "ConfigType": "deny_referer_access_rule",
                "DomainCount": 3,
                "Project": "default",
                "UpdateTime": 1702484378
            }
        ],
        "PageNum": 1,
        "PageSize": 10,
        "Total": 34
    }
}
```


&nbsp;
