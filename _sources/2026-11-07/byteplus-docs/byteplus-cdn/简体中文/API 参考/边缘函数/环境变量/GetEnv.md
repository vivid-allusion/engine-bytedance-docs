---
title: "GetEnv"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetEnv-cn"
---

获取函数的环境变量。

<span id="使用说明"></span>
## 使用说明

请求限流：每秒最多可发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetEnv&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `GetEnv`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |
|FunctionId |String |是 |函数 ID。您可以调用[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-cn)获取函数 ID。 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Envs |Object[] |环境变量列表。 | |
|Key |String |环境变量的键。 |`a` |
|Value |String |环境变量的值。 |`a` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```HTTP
GET  https://cdn.byteplusapi.com?Action=GetEnv&Version=2021-03-01&FunctionId=23455331245
```


<span id="返回示例"></span>
### 返回示例

```json

{
    "ResponseMetadata": {
        "RequestId": "20211207213413010225146063****",
        "Action": "GetEnv",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Envs": [
            {
                "Key": "abc",
                "Value": "123"
            }
        ]
    }
}
```


&nbsp;
