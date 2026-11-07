---
title: "FullPublish"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/FullPublish"
---

该接口用于根据函数ID完全发布函数。

<span id="使用说明"></span>
## 使用说明

请求限流：每秒最多可发送20个请求。另外，对于每个函数，每秒最多可发送1个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=FullPublish&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `FullPublish`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|FunctionId |String |是 |您希望发布的函数的ID。您可以通过调用接口[ListSparrow](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSparrow)获取FunctionId。 |`3gyz993****` |
|Description |String |否 |填写此次发布的描述信息。 |`test publish` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|TicketId |Long |发布ID |`146023529142213****` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST  https://cdn.byteplusapi.com?Action=FullPublish&Version=2021-03-01
{
    "FunctionId": "3246574",
    "Description": "test publish"
}
```


<span id="返回示例"></span>
### 返回示例

```json

{
    "ResponseMetadata": {
        "RequestId": "202112072116030102251331430*****",
        "Action": "FullPublish",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TicketId": "146023529142213****"
    }
}
```


&nbsp;
