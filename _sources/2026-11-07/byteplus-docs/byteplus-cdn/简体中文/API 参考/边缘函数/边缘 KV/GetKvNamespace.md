---
title: "GetKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetKvNamespace-cn"
---

获取存储空间的详细信息。

<span id="使用说明"></span>
## 使用说明

请求限制：每秒最多发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetKvNamespace&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `GetKvNamespace`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |
|Namespace |String |是 |存储空间的名称。您可以通过调用接口[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-cn)获取。 |
|NamespaceId |String |是 |存储空间的 ID。您可以通过调用接口[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-cn)获取。 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Namespace |Object |存储空间详情。 | |
|Namespace |String |存储空间的名称。您可以通过调用接口[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-cn)获取。 |`test-kv1` |
|NamespaceId |String |存储空间的 ID。您可以通过调用接口[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-cn)获取。 |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|Description |String |存储空间的描述。 |`test` |
|Creator |String |存储空间的创建者。 |`testuser` |
|CreateTime |Long |创建时间。格式为 Unix 时间戳（秒）。 |`1661864175` |
|UpdateTime |Long |更新时间。格式为 Unix 时间戳（秒）。 |`1678288603` |
|ProjectName |String |存储空间所属的项目的名称。 |`default` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```HTTP
GET  https://cdn.byteplusapi.com?Action=GetKvNamespace&Version=2021-03-01&Namespace=test-kv1&NamespaceId=46d79a9944ae2fd81f2643e2fe5ef42d****
```


<span id="返回示例"></span>
### 返回示例

```json

{
    "ResponseMetadata": {
        "RequestId": "202308080952004CD21902****",
        "Action": "GetKvNamespace",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Namespace": {
            "Namespace": "test-kv1",
            "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
            "Description": "test",
            "Creator": "testuser",
            "ProjectName": "default",
            "CreateTime": 1661864175,
            "UpdateTime": 1678288603
        }
    }
}
```
