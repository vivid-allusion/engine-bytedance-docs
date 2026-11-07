---
title: "DeleteCdnDomain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/deletecdndomain"
---

删除指定的域名。域名删除后，您将无法查看该域名的配置以及该域名的历史数据。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DeleteCdnDomain&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DeleteCdnDomain`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Domain |String |是 |表示一个要删除的域名。 |`www.example.com` |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DeleteCdnDomain&Version=2021-03-01
{
  "Domain": "www.example.com"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
  "ResponseMetadata": {
    "RequestId": "202109152017370101941000541800CE83",
    "Action": "DeleteCdnDomain",
    "Version": "2021-03-01",
    "Service": "CDN",
    "Region": "ap-singapore-1"
  }
}
```


&nbsp;
