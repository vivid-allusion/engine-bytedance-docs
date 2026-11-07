---
title: "ListKvKey"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvKey"
---

该接口用于获取命名空间中的数据列表。

<span id="使用说明"></span>
## 使用说明

请求限制：每秒最多发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListKvKey&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `ListKvKey`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |
|Namespace |String |是 |数据所属的命名空间的名称。 |
|NamespaceId |String |是 |数据所属的命名空间的ID。您可以通过调用接口[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace)<br><br>&nbsp;<br><br>获取namespaceId。 |
|Page |Integer |否 |页码 |
|Limit |Integer |否 |每页记录数。<br><br>&nbsp;<br><br>目前一次最多可获取50条记录。 |
|OrderBy |Integer |否 |该参数指定查询数据的顺序，接受以下值：<br><br><br>* 1：降序排列数据。<br><br>* 2（默认）：升序排列数据。 |
|OrderType |String |否 |可用的排序类型有：<br><br><br>* create_time（默认）：根据创建时间排序数据。<br><br>* update_time：根据最后更新时间排序数据。 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|NamespaceKeys |Object |命名空间中的数据详情。 |`See explanation below` |
|Namespace |String |数据所属的命名空间的名称。 |`test-kv1` |
|NamespaceId |String |数据所属的命名空间的ID。 |`14776510402228****` |
|Key |String |键。 |`testkey` |
|KeyStatus |Integer |数据状态。<br><br><br>* 100：已过期<br><br>* 200：正常 |`200` |
|DDL |Long |数据的过期时间。数据过期后，Key中的Value将无法访问。<br><br><br>* 以UNIX时间戳格式显示。<br><br>* 0：永久存储。 |`0` |
|CreateTime |Long |数据的创建时间。以UNIX时间戳格式显示。 |`1662005890` |
|UpdateTime |Long |数据的更新时间。以UNIX时间戳格式显示。 |`1664337001` |
|TotalCount |Long |命名空间中的数据总数。 |`2` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
GET  https://cdn.byteplusapi.com?Action=ListKvKey&Version=2021-03-01&Namespace=test-kv1&NamespaceId=46d79a9944ae2fd81f2643e2fe5ef42d****&Page=1&Limit=10&OrderBy=2&OrderType=create\_time
```


<span id="返回示例"></span>
### 返回示例

```json

{
    "ResponseMetadata": {
        "RequestId": "20230810210051741B321D8****",
        "Action": "ListKvKey",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "NamespaceKeys": [
            {
                "Namespace": "test-kv1",
                "NamespaceId": "14776510402****",
                "Key": "testkey",
                "KeyStatus": 200, // 100 Expired; 200 Normal
                "DDL": 0,
                "CreateTime": 1678085786,
                "UpdateTime": 1678085786
            },
            {
                "Namespace": "test-kv1",
                "NamespaceId": "14776510402****",
                "Key": "key",
                "KeyStatus": 100,
                "DDL": 1678259532,
                "CreateTime": 1678092385,
                "UpdateTime": 1682327035
            },
        ],
        "TotalCount": 2
    }
}
```


&nbsp;
