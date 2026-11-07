---
title: "ListVersions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListVersions"
---

该接口用于根据函数ID检索已发布的所有代码版本。

<span id="使用说明"></span>
## 使用说明

请求限流：每秒最多可发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListVersions&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `ListVersions`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |
|FunctionId |String |是 |您希望查看所有代码版本列表的函数ID。您可以通过调用接口[ListSparrow](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSparrow)来获取函数ID。 |
|Page |Integer |否 |页码。 |
|Limit |Integer |否 |每页记录数。<br><br>&nbsp;<br><br>&nbsp;<br><br>目前，一次最多可获取50条记录。 |
|OrderBy |Integer |否 |该参数指定数据查询的顺序。它接受以下值：<br><br><br>* 1：降序排列数据。<br><br>* 2（默认）：升序排列数据。 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Revisions |Object[] |代码版本列表 |`See below` |
|Id |Long |ID |`1` |
|VersionTag |String |该版本的版本号。 |`1.0.1` |
|Description |String |该版本的描述。 |`this is a sparrow` |
|Creator |String |创建者 |`zhangsan` |
|TotalCount |Long |代码版本总数 |`1` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
GET  https://cdn.byteplusapi.com?Action=ListVersions&Version=2021-03-01&FunctionId=3gyz993****&Page=1&Limit=10&OrderBy=2
```


<span id="返回示例"></span>
### 返回示例

```json

{
    "ResponseMetadata": {
        "RequestId": "2022011310282201022524312506*******",
        "Action": "ListVersions",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Revisions": [
            {
                "Id": 133,
                "VersionTag": "1.0.1",
                "Description": "test publish",
                "Creator": "*****"
            }
        ],
        "TotalCount": 1
    }
}
```


&nbsp;
