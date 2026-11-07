---
title: "EditEnv"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/EditEnv"
---

该接口用于基于函数ID更新函数的环境变量。

<span id="使用说明"></span>
## 使用说明

请求限流：每秒最多可发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=EditEnv&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `EditEnv`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|FunctionId |String |是 |函数ID |`23455331245` |
|Envs |Object[] |是 |配置内容 |`[{"Key": "abc","Value": "123"}]` |
|Key |String |是 |环境变量的键 |`a` |
|Value |String |是 |环境变量的值 |`a` |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST  https://cdn.byteplusapi.com?Action=EditEnv&Version=2021-03-01
{
    "FunctionId": "23455331245",
    "Envs": [
        {
            "Key": "abc",
            "Value": "123"
        }
    ]
}
```
