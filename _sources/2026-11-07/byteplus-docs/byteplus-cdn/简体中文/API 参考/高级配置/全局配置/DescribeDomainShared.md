---
title: "DescribeDomainShared"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDomainShared_cn"
---

指定一个全局配置，获取该全局配置所关联的域名。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeDomainShared&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeDomainShared`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|ConfigName |String |否 |表示一个全局配置的名称，查询与该全局配置关联的域名。 |`my_list` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|ConfigName |String |表示该全局配置的名称。 |`my_list` |
|Domain |String[] |表示一个与该全局配置关联的域名列表。如果该全局配置还未与任何域名关联，该参数值为一个空数组。<br><br>当调用该 API 时，如果子账号没有权限访问某个与该全局配置关联的域名，该域名不会出现在 `Domain` 列表中。 |`["example.com","www.example.com"]` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeDomainShared&Version=2021-03-01
{
    "ConfigName": "test11"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20241209063311CB50419F0326B7CA55A4",
        "Action": "DescribeDomainShared",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ConfigName": "test11",
        "Domain": [
            "www.example.com"
        ]
    }
}
```


&nbsp;
