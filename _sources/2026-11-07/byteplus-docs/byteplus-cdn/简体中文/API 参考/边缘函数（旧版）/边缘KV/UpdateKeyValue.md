---
title: "UpdateKeyValue"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateKeyValue"
---

该接口用于修改键值对的值和存储时长。

<span id="使用说明"></span>
## 使用说明

请求限制：每秒最多发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=UpdateKeyValue&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `UpdateKeyValue`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Namespace |String |是 |键值对所属的存储空间的名称。您可以通过调用接口[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace)获取。 |`test-kv1` |
|NamespaceId |String |是 |键值对所属的存储空间的ID。您可以通过调用接口[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace)获取。 |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|Key |String |是 |您要修改值或存储时间的键。您可以通过调用接口[ListKvKey](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvKey)获取。 |`testkey` |
|Value |String |是 |输入新的值。如果不指定此参数，则保留原始值。输入要求如下：<br><br><br>* 只能输入Base64编码格式。<br><br>* 不超过128KB。 |`dGVzdDEyMw==` |
|TTL |Long |是 |输入新的存储时长。单位：秒。键值对过期后，函数将无法访问Key的Value。如果不指定此参数，则保留原始值。<br><br><br>* 0：永久存储。<br><br>* 存储时长不能少于60秒。 |`0` |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST  https://cdn.byteplusapi.com?Action=UpdateKeyValue&Version=2021-03-01
{
    "Namespace": "test-kv1",
    "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
    "Key": "testkey",
    "Value": "dGVzdDEyMw==",
    "TTL": 0
}
```


&nbsp;
