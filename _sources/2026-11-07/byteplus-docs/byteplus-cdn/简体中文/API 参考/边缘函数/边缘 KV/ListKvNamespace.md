---
title: "ListKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-cn"
---

获取存储空间列表。

<span id="使用说明"></span>
## 使用说明

请求限制：每秒最多发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListKvNamespace&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `ListKvNamespace`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |
|Page |Integer |否 |页码。默认为 1。 |
|Limit |Integer |否 |每页记录数。默认为 50 条记录。<br><br>最多为 50 条记录。 |
|OrderBy |Integer |否 |该参数指定查询数据的顺序，接受以下值：<br><br><br>* 1：降序排列存储空间。<br><br>* 2（默认）：升序排列存储空间。 |
|OrderType |String |否 |可用的排序类型有：<br><br><br>* create_time（默认）：根据创建时间排序存储空间。<br><br>* update_time：根据最后更新时间排序存储空间。 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Namespaces |Object |存储空间列表。 | |
|Namespace |String |存储空间的名称。 |`test-kv1` |
|NamespaceId |String |存储空间的ID。 |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|Description |String |存储空间的描述。 |`test` |
|Creator |String |存储空间的创建者。 |`testuser` |
|CreateTime |Long |创建时间。格式为 Unix 时间戳（秒）。 |`1661864175` |
|UpdateTime |Long |更新时间。格式为 Unix 时间戳（秒）。 |`1678288603` |
|TotalCount |Long |存储空间的总数量。 |`2` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListKvNamespace&Version=2021-03-01&Page=1&Limit=10&OrderBy=2&OrderType=create_time
```


<span id="返回示例"></span>
### 返回示例

```json

{
    "ResponseMetadata": {
        "RequestId": "20230808095102CFDFA3280****",
        "Action": "ListKvNamespace",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Namespaces": [
            {
                "Namespace": "test-kv1",
                "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
                "Description": "test",
                "Creator": "testuser",
                "CreateTime": 1661864175,
                "UpdateTime": 1678288603
            },
            {
                "Namespace": "asdJSJasdad",
                "NamespaceId": "510257916f6b5503b288d064b7154****",
                "Description": "",
                "Creator": "testuser",
                "CreateTime": 1662005890,
                "UpdateTime": 1664337001
            }
        ],
        "TotalCount": 2
    }
}
```


&nbsp;
