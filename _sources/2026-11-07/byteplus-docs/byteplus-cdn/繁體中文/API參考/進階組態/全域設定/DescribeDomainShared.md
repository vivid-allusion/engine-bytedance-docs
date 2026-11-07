---
title: "DescribeDomainShared"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeDomainShared_zh-tw"
---

指定一個全域設定，獲取該全域設定所關聯的網域名稱。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeDomainShared&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeDomainShared`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|ConfigName |String |否 |表示一個全域設定的名稱，查詢與該全域設定關聯的網域名稱。 |`my_list` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|ConfigName |String |表示該全域設定的名稱。 |`my_list` |
|Domain |String[] |表示一個與該全域設定關聯的網域名稱列表。如果該全域設定還未與任何網域名稱關聯，該參數值為一個空陣列。<br><br>&nbsp;<br><br>當調用該 API 時，如果子帳戶沒有權限訪問某個與該全域設定關聯的網域名稱，該網域名稱不會出現在 `Domain` 列表中。 |`["example.com","www.example.com"]` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeDomainShared&Version=2021-03-01
{
    "ConfigName": "test11"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20241209063311CB50419F0326B7CA55A4",
        "Action": "DescribeDomainShared",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ConfigName": "test11",
        "Domain": [
            "www.example.com"
        ]
    }
}
```


&nbsp;
