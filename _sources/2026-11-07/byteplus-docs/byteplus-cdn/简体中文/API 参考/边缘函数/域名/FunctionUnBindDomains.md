---
title: "FunctionUnBindDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-FunctionUnBindDomains-cn"
---

将域名与函数解除关联。

<span id="使用说明"></span>
## 使用说明

请求限流：每秒最多可发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=FunctionUnBindDomains&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `FunctionUnBindDomains`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Domains |String[] |是 |输入需要解除关联的域名。您可以通过调用 [ListFunctionDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCDNDomain-cn) 获取可用的 CDN 域名列表。 |`["test1.example.com","test2.example.com"]` |
|FunctionId |String |是 |输入需要解除关联的函数 ID。您可以通过调用 [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-cn) 获取 FunctionId。 |`3gyz993****` |


<span id="返回参数"></span>
## 返回参数

无

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST  https://cdn.byteplusapi.com?Action=FunctionUnBindDomains&Version=2021-03-01
{
  "FunctionId": "b21f19d28c7f4fbbb8b8bc799f28****",
  "Domains":[
    "a.example.com",
    "b.example.com"
    ]
}
```
