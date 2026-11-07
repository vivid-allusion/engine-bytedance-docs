---
title: "TagResources"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/TagResources"
---

为一个或者多个域名添加标签。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=TagResources&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `TagResources`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|ResourceIds |String[] |是 |表示一个需要添加标签的域名列表。列表中最多可以包含 50 个域名。 |`["www.example.com","img.example.com"]` |
|ResourceType |String |是 |该参数值必须是 `domain`。 |`domain` |
|Tags |Object[] |是 |表示一个标签列表。列表中最多可以包含 50 个标签。每个标签是一个键值对。 | |
|Key |String |否 |表示列表中一个标签的 Key，长度范围是 1\-128 个字符。<br><br>Key 是大小写敏感的，可以包含字母、数字、空格以及以下任意字符：<br><br><br>* _./=+\-@ |`myKey` |
|Value |String |否 |表示该标签的 Value，长度范围是 1\-256 个字符。其他输入要求与 `Key` 相同。 |`myValue` |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=TagResources&Version=2021-03-01
{
    "ResourceType": "domain",
    "ResourceIds": [
        "www.example.com",
        "img.example.com"
    ],
    "Tags": [
        {
            "Key": "myKey1",
            "Value": "myValue1"
        },
        {
            "Key": "myKey2",
            "Value": "myValue2"
        }
    ]
}
```


&nbsp;
