---
title: "UpdateKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateKvNamespace"
---

该接口用于修改存储空间的名称或描述。

<span id="使用说明"></span>
## 使用说明

请求限制：每秒最多发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=UpdateKvNamespace&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `UpdateKvNamespace`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Namespace |String |是 |需要修改的存储空间的名称。您可以通过调用接口[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace)获得。 |`test-kv1` |
|NamespaceId |String |是 |需要修改的存储空间的ID。您可以通过调用接口[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace)获得。 |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|NewNamespace |String |是 |存储空间的新名称。如果您只希望修改存储空间的描述而不更改其名称，可以输入当前存储空间的名称作为此参数的值。输入要求如下：<br><br><br>* 新名称不能与当前BytePlus主账号中的其他存储空间名称相同。<br><br>* 长度应在2到64个字符之间。<br><br>* 只能包含英文字母、数字、连字符(\-)和下划线(_)。<br><br>* 不区分大小写，这意味着“NamespaceName”和“NAMESPACENAME”被认为是相同的。另外，边缘函数不会对大小写进行转换。 |`test-kv2` |
|Description |String |否 |存储空间的新描述信息，长度不得超过80个字符。如果未指定此参数，则保留原始描述。 |`test` |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST   https://cdn.byteplusapi.com?Action=UpdateKvNamespace&Version=2021-03-01
{
    "Namespace": "test-kv1",
    "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
    "NewNamespace": "test-kv2",
    "Description": "test"
}
```


&nbsp;
