---
title: "DeleteEnv"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-DeleteEnv-cn"
---

删除函数的环境变量。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您对环境变量的增删改操作在函数被再次发布后才会生效。</div>


<span id="使用说明"></span>
## 使用说明

请求限流：每秒最多可发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=DeleteEnv&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DeleteEnv`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|FunctionId |String |是 |函数 ID。您可以调用[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-cn)获取函数 ID。 |`23455331245` |
|EnvKeys |String[] |是 |您想要删除的环境变量的键。您可以一次性删除多个环境变量。 |`["abc","def"]` |


<span id="返回参数"></span>
## 返回参数

无

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST  https://cdn.byteplusapi.com?Action=DeleteEnv&Version=2021-03-01
{
    "FunctionId": "23455331245",
    "Envs": [
        "abc",
        "def"
    ]
}
```
