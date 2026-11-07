---
title: "CreateKeyValue"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateKeyValue-cn"
---

在存储空间中添加键值对。

<span id="使用说明"></span>
## 使用说明

请求限制：每秒最多发送20个请求。


* 添加键值对成功后，Key不可修改。

* 同一存储空间中的Key不能相同。Key不区分大小写，即`Key`和`KEY`被视为相同。


<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=CreateKeyValue&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `CreateKeyValue`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Namespace |String |是 |存储空间的名称。您可以通过调用接口[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-cn)获取。 |`test-kv1` |
|NamespaceId |String |是 |存储空间的 ID。您可以通过调用接口[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-cn)获取。 |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|Key |String |是 |键。输入要求如下：<br><br><br>* 只能包含英文字母、数字、短横线（\-）和下划线（_）。<br><br>* 不超过512字节。 |`testkey` |
|Value |String |是 |值。输入要求如下：<br><br><br>* 只能输入Base64编码格式。<br><br>* 不超过128KB。 |`dGVzdHZhbHVlMTIz` |
|TTL |Long |否 |设置键值对的有效时长。单位：秒。键值对过期后，边缘函数将无法读取 Key 的 Value。<br><br><br>* 如果未指定此参数或参数值为0，则永不过期。<br><br>* 有效时长不得少于60s。 |`0` |


<span id="返回参数"></span>
## 返回参数

无

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST   https://cdn.byteplusapi.com?Action=CreateKeyValue&Version=2021-03-01
{
    "Namespace": "test-kv1",
    "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
    "Key": "testkey",
    "Value": "dGVzdHZhbHVlMTIz",
    "TTL": 0
}
```


&nbsp;
