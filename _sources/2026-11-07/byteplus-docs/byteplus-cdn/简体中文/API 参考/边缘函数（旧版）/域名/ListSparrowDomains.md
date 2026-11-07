---
title: "ListSparrowDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListSparrowDomains"
---

该接口用于获取指定函数可以绑定的CDN域名列表。

<span id="使用说明"></span>
## 使用说明

请求限流：每秒最多可发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListSparrowDomains&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `ListSparrowDomains`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |
|FunctionId |String |是 |输入您希望绑定到域的函数的ID。 |
|Page |Integer |是 |页码 |
|Limit |Integer |是 |每页记录数。<br><br>&nbsp;<br><br>&nbsp;<br><br>目前，一次最多可获取50条记录。 |
|OrderBy |Integer |否 |该参数指定数据查询的顺序。它接受以下值：<br><br><br>* 1：降序排列数据。<br><br>* 2（默认）：升序排列数据。 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Domains |Object[] |域名列表 |`See the explanation below.` |
|Domain |String |域名 |`test.sparrow1.com` |
|BindStatus |Integer |域名与指定函数之间的绑定状态：<br><br><br>* 1：已绑定<br><br>* 2：可绑定<br><br>* 3：无法绑定 |`2` |
|TotalCount |Long |函数总数 |`1` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
GET  https://cdn.byteplusapi.com?Action=ListSparrowDomains&Version=2021-03-01&FunctionId=b21f19d28c7f4fbbb8b8bc799f28****&Page=1&Limit=10
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "2023050920020063355B94DB6C32617243",
        "Action": "ListSparrowDomains",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domains": [
            {
                "BindStatus": 2,
                "Domain": "test.sparrow1.com"
            },
            {
                "Domain": "test.com",
                "BindStatus": 2
            },
            {
                "Domain": "example.com",
                "BindStatus": 2
            }
        ],
        "TotalCount": 3
    }
}
```


&nbsp;
