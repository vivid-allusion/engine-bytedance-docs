---
title: "UntagResources"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UntagResources_zh-tw"
---

從一個或者多個網域名稱刪除指定的標籤。

<span id="使用限制"></span>
## 使用限制

節流限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=UntagResources&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `UntagResources`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|ResourceIds |String[] |是 |表示需要刪除指定標籤的一個網域名稱清單。清單中最多可以包含 50 個網域名稱。 |`["www.example.com","img.example.com"]` |
|ResourceType |String |是 |該參數值必須是 `domain`。 |`domain` |
|TagKeys |String[] |是 |對於需要刪除的標籤，該參數表示這些標籤的 Key。清單中最多可以包含 50 個 Key。 |`["key1","key2"]` |


<span id="回應"></span>
## 回應

<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

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
