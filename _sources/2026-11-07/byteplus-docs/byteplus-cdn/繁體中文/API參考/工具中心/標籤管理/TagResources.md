---
title: "TagResources"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-TagResources_zh-tw"
---

為一個或者多個網域名稱添加標籤。

<span id="使用限制"></span>
## 使用限制

節流限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=TagResources&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `TagResources`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|ResourceIds |String[] |是 |表示一個需要添加標籤的網域名稱清單。清單中最多可以包含 50 個網域名稱。 |`["www.example.com","img.example.com"]` |
|ResourceType |String |是 |該參數值必須是 `domain`。 |`domain` |
|Tags |Object[] |是 |表示一個標籤清單。清單中最多可以包含 50 個標籤。每個標籤是一個鍵值對。 | |
|Key |String |否 |表示清單中一個標籤的 Key，長度範圍是 1\-128 個字元。<br><br>Key 是大小寫敏感的，可以包含字母、數字、空格以及以下任意字元：<br><br><br>* _./=+\-@ |`myKey` |
|Value |String |否 |表示該標籤的 Value，長度範圍是 1\-256 個字元。其他輸入要求與 `Key` 相同。 |`myValue` |


<span id="回應"></span>
## 回應

<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

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
