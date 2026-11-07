---
title: "GetTicket"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/GetTicket"
---

该接口用于根据函数ID和发布记录ID检索发布记录的详细信息。

<span id="使用说明"></span>
## 使用说明

请求限流：每秒最多可发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetTicket&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `GetTicket`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |
|FunctionId |String |是 |函数ID |
|TicketId |Long |是 |发布记录ID |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Ticket |Object |发布记录详情 | |
|Id |Long |发布记录ID |`1` |
|FunctionId |String |函数ID |`23455331245` |
|Content |String |发布记录的内容 |`{&quot;current_traffics&quot;:[{&quot;version_tag&quot;:&quot;1.0.1&quot;}],&quot;origin_traffics&quot;:[]}` |
|Status |Integer |发布状态。<br><br><br>* 100：灰度发布成功<br><br>* 200：全量发布成功 |`100` |
|Description |String |描述 |`this is a sparrow` |
|Creator |String |创建者 |`zhangsan` |
|CreateTime |Long |创建时间 |`1638326159` |
|UpdateTime |Long |更新时间 |`1638326159` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
GET  https://cdn.byteplusapi.com?Action=GetTicket&Version=2021-03-01&FunctionId=3gyz993****&TicketId=28
```


<span id="返回示例"></span>
### 返回示例

```json

{
    "ResponseMetadata": {
        "RequestId": "2022011310531001022511001100*****",
        "Action": "GetTicket",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Ticket":
         {
            "Id": 133,
            "FunctionId": "3gyz993****",
            "Content": "{\"current_traffics\":[{\"version_tag\":\"1.0.1\"}],\"origin_traffics\":[]}",
            "Description": "test publish",
            "Creator": "****",
            "CreateTime": 1640077698,
            "UpdateTime": 1640077759
        }
    }
}
```


&nbsp;
