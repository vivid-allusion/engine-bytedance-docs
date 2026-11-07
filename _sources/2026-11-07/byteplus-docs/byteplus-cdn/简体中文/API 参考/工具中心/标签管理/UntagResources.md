---
title: "UntagResources"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UntagResources"
---

从一个或者多个域名删除指定的标签。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=UntagResources&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `UntagResources`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|ResourceIds |String[] |是 |表示需要删除指定标签的一个域名列表。列表中最多可以包含 50 个域名。 |`["www.example.com","img.example.com"]` |
|ResourceType |String |是 |该参数值必须是 `domain`。 |`domain` |
|TagKeys |String[] |是 |对于需要删除的标签，该参数表示这些标签的 Key。列表中最多可以包含 50 个 Key。 |`["key1","key2"]` |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=UntagResources&Version=2021-03-01
{
        "ResourceType": "domain",
        "ResourceIds": ["www.example.com","img.example.com"],
    "TagKeys": [
        {
            "myKey1",
            "myKey2"
        }
    ]
}
```


&nbsp;
