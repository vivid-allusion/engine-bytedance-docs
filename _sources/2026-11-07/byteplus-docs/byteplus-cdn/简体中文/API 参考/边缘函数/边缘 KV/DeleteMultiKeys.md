---
title: "DeleteMultiKeys"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/api-ref-delete-multikeys-cn"
---

批量删除键值对。

<span id="使用说明"></span>
## 使用说明

请求限制：每分钟最多发送6个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=DeleteMultiKeys&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DeleteMultiKeys`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Namespace |String |是 |存储空间的名称。您可以通过调用接口[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-cn)获取。 |`test-kv1` |
|NamespaceId |String |是 |存储空间的 ID。您可以通过调用接口[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-cn)获取。 |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|KeyList |Array of strings |是 |要删除的键值对的键。 |`["key1","key2"]` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|DeleteResult |Object |删除结果。 | |
|FailedKeys |Array of strings |删除失败的键。 |`["key1","key2"]` |
|SuccessfulCount |String |成功被删除的键的数量。 |`1` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST  https://cdn.byteplusapi.com?Action=DeleteMultiKeys&Version=2021-03-01
{
  "Namespace": "test-kv1",
  "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
  "KeyList": [
    "key1",
    "key2"
  ]
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230808095102CFDFA3280****",
        "Action": "DeleteMultiKeys",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
        "Result": {
            "DeleteResult": {
                "FailedKeys": [
                    "key2"
                ],
                "SuccessfulCount": 1
            }
        }
}        
```
