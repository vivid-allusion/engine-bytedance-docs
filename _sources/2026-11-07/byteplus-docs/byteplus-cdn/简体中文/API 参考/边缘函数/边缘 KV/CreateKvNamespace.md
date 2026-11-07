---
title: "CreateKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateKvNamespace-cn"
---

创建存储空间。

<span id="使用说明"></span>
## 使用说明

请求限制：每秒最多发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=CreateKvNamespace&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `CreateKvNamespace`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Namespace |String |是 |为存储空间设置一个可识别的名称。输入要求如下：<br><br><br>* 长度应在2到64个字符之间。<br><br>* 只能包含英文字母、数字、连字符(\-)和下划线(_)。<br><br>* 不区分大小写，这意味着“Namespace”和“NAMESPACE”被认为是相同的。另外，边缘函数不会对大小写进行转换。 |`test-kv1` |
|Description |String |否 |为存储空间设置描述。长度不得超过80个字符。 |`test` |
|ProjectName |String |否 |存储空间所属的项目名称，默认为`default`。 |`default` |


<span id="返回参数"></span>
## 返回参数

无

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST   https://cdn.byteplusapi.com?Action=CreateKvNamespace&Version=2021-03-01
{
    "Namespace": "test-kv1",
    "Description": "test",
    "ProjectName": "default"
}
```


&nbsp;
