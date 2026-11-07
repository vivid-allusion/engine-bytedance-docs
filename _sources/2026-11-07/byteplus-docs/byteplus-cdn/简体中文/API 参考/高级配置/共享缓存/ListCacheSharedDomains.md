---
title: "ListCacheSharedDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListCacheSharedDomains_zh-cn"
---

获取已创建的共享缓存配置。您可以指定过滤条件对 API 返回的配置进行过滤。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=ListCacheSharedDomains&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `ListCacheSharedDomains`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|PrimaryDomain |String |否 |表示一个域名，获取以该域名作为目标域名的共享缓存配置。<br><br>如果不指定该参数，表示不指定该过滤条件。<br><br>`PrimaryDomain` 和 `SecondaryDomain` 只能指定其中一个。 |`example.com` |
|SecondaryDomain |String |否 |表示一个域名，获取共享缓存域名列表中包含该域名的共享缓存配置。<br><br>如果不指定该参数，表示不指定该过滤条件。 |`example.net` |
|ExactMatch |Boolean |否 |表示在将 `PrimaryDomain` 或 `SecondaryDomain` 与配置中的域名匹配时，CDN 是否使用精确匹配。该参数有以下取值：<br><br><br>* `true`：表示使用精确匹配。<br><br>* `false`：表示使用模糊匹配。<br><br><br>该参数的默认值是 `false`。 |`false` |
|PageSize |Long |否 |该 API 对获取的配置进行分页。该参数表示每页包含的配置数量。该参数的取值范围是 1\-100，默认值是 `10`。 |`10` |
|PageNum |Long |否 |表示展示哪个分页上的配置。该参数的默认值是 `1`。 |`1` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Data |Object[] |表示该 API 返回的共享缓存配置列表。 | |
|CacheSharedOn |String |表示一个配置域名列表。多个域名之间使用逗号（,）分隔。 |`www.example.com,abc.example.com` |
|TargetHost |String |表示目标域名。 |`www.example.com` |
|UpdateTime |Long |表示该配置的最近更新时间，格式是 Unix 时间戳，单位是秒。 |`1755831922` |
|PageNumber |Long |表示您指定的 `PageNumber`。 |`1` |
|PageSize |Long |表示您指定的 `PageSize`。 |`10` |
|Total |Long |表示符合过滤条件的配置数量。 |`3` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=ListCacheSharedDomains&Version=2021-03-01
{
    "ExactMatch": false,
    "PrimaryDomain": "example"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20250910102143FC1FDB61C3CFED0130C4",
        "Action": "ListCacheSharedDomains",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": [
            {
                "CacheSharedOn": "www.example.com,abc.example.com",
                "TargetHost": "www.example.net",
                "UpdateTime": 1755831922
            },
            {
                "CacheSharedOn": "docs.example.com",
                "TargetHost": "docs.example.net",
                "UpdateTime": 1749631703
            }
        ],
        "PageNumber": 1,
        "PageSize": 50,
        "Total": 2
    }
}
```


&nbsp;
