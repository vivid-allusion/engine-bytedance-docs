---
title: "GetKeyValue"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetKeyValue-cn"
---

查看键值对的值和过期时间。

<span id="使用说明"></span>
## 使用说明

请求限制：每秒最多发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetKeyValue&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `GetKeyValue`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |
|Namespace |String |是 |存储空间的名称。您可以通过调用接口[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-cn)获取。 |
|NamespaceId |String |是 |存储空间的 ID。您可以通过调用接口[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-cn)获取。 |
|Key |String |是 |您要查询值或过期时间的键。 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|DDL |Long |键值对的过期时间。键值对过期后，函数将无法访问Key的Value。<br><br><br>* 以秒级 Unix 时间戳格式显示。<br><br>* 0：永不过期。 |`0` |
|Key |String |查询的键。 |`testkey` |
|Value |String |查询的键的值。值为Base64编码格式。 |`dGVzdHZhbHVlMTIz` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```HTTP
GET   https://cdn.byteplusapi.com?Action=GetKeyValue&Version=2021-03-01&Namespace=test-kv1&NamespaceId=46d79a9944ae2fd81f2643e2fe5ef42d****&Key=testkey
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetKeyValue",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DDL": 0,
        "Key": "testkey",
        "Value": "dGVzdHZhbHVlMTIz"
    }
}
```


&nbsp;
