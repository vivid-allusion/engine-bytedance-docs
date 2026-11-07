---
title: "ListFunctionDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCDNDomain-cn"
---

为指定函数获取可以关联的域名的列表。

<span id="使用说明"></span>
## 使用说明

请求限流：每秒最多可发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListFunctionDomains&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `ListFunctionDomains`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |
|FunctionId |String |是 |需要关联域名的函数的ID。 |
|Page |Integer |是 |页码 |
|Limit |Integer |是 |每页记录数。<br><br>&nbsp;<br><br>&nbsp;<br><br>目前，一次最多可获取50条记录。 |
|OrderBy |Integer |否 |该参数指定数据查询的顺序。它接受以下值：<br><br><br>* 1：降序排列数据。<br><br>* 2（默认）：升序排列数据。 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Domains |Object[] |域名列表。 |`["test.example.com"]` |
|Domain |String |域名。 |`test.example.com` |
|BindStatus |Integer |域名与指定函数之间的关联状态：<br><br><br>* 1：已关联<br><br>* 2：可关联<br><br>* 3：无法关联 |`2` |
|TotalCount |Long |函数总数。 |`1` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListFunctionDomains&Version=2021-03-01&FunctionId=b21f19d28c7f4fbbb8b8bc799f28****&Page=1&Limit=10
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "2023050920020063355B94DB6C32617243",
        "Action": "ListFunctionDomains",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domains": [
            {
                "Domain": "123.example.com",
                "BindStatus": 2
            },
            {
                "Domain": "test.example.com",
                "BindStatus": 2
            }
        ],
        "TotalCount": 3
    }
}
```


&nbsp;
