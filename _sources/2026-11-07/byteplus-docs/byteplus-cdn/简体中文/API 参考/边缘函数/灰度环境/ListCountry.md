---
title: "ListCountry"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCountry-cn"
---

对于指定的函数，获取可用的边缘节点所在的国家或地区列表。

<span id="使用说明"></span>
## 使用说明

请求限流：每秒最多可发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListCountry&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `ListCountry`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |
|FunctionId |String |是 |函数 ID。您可以调用[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-cn)获取函数 ID。 |
|Continents |String |否 |一个或多个大洲。多个大洲用逗号分隔。 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Countries |String[] |边缘节点所在的国家或地区。 |`["Singapore"]` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListCountry&Version=2021-03-01&FunctionId=3gyz993****&Continents=\["Asia"\]
```


<span id="返回示例"></span>
### 返回示例

```json

{
    "ResponseMetadata": {
        "RequestId": "2022011310531001022511001100*****",
        "Action": "ListCountry",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Countries": [
            "Singapore"
        ]
    }
}
```


&nbsp;
