---
title: "SparrowBindDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/SparrowBindDomains"
---

该接口用于将域名绑定到函数。

<span id="使用说明"></span>
## 使用说明

请求限流：每秒最多可发送20个请求。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">边缘函数仅绑定已在账户中添加到CDN的域名。</div>



* 一个函数最多可以关联100个域名。

* 一个域名最多可以关联50个函数。


<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=SparrowBindDomains&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `SparrowBindDomains`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Domains |String[] |是 |输入您希望与函数绑定的域名。您可以通过调用接口[ListSparrowDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSparrowDomains)获取可用的CDN域名列表。 |`["test.sparrow1.com","test.sparrow2.com"]` |
|FunctionId |String |是 |输入您希望绑定域名的函数ID。您可以通过调用接口[ListSparrow](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSparrow)获取FunctionId。 |`3gyz993****` |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST  https://cdn.byteplusapi.com?Action=SparrowBindDomains&Version=2021-03-01
{
  "FunctionId": "b21f19d28c7f4fbbb8b8bc799f28****",
  "Domains":[
    "test.com",
    "example.com"
    ]
}
```
