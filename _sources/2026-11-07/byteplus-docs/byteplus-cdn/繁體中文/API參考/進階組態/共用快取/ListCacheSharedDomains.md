---
title: "ListCacheSharedDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListCacheSharedDomains_zh-tw"
---

獲取已建立的共用快取設定。您可以指定過濾條件對 API 返回的設定進行過濾。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=ListCacheSharedDomains&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `ListCacheSharedDomains`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|PrimaryDomain |String |否 |表示一個網域名稱，獲取以該網域名稱作為目標網域名稱的共用快取設定。<br><br>如果不指定該參數，表示不指定該過濾條件。<br><br>`PrimaryDomain` 和 `SecondaryDomain` 只能指定其中一個。 |`example` |
|SecondaryDomain |String |否 |表示一個網域名稱，獲取共用快取網域名稱清單中包含該網域名稱的共用快取設定。<br><br>如果不指定該參數，表示不指定該過濾條件。 |`example.net` |
|ExactMatch |Boolean |否 |表示在將 `PrimaryDomain` 或 `SecondaryDomain` 與設定中的網域名稱匹配時，CDN 是否使用精確匹配。該參數有以下取值：<br><br><br>* `true`：表示使用精確匹配。<br><br>* `false`：表示使用模糊匹配。<br><br><br>該參數的預設值是 `false`。 |`false` |
|PageSize |Long |否 |該 API 對獲取的設定進行分頁。該參數表示每頁包含的設定數量。該參數的取值範圍是 1\-100，預設值是 `10`。 |`10` |
|PageNum |Long |否 |表示展示哪個分頁上的設定。該參數的預設值是 `1`。 |`1` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|Data |Object[] |表示該 API 返回的共用快取設定清單。 | |
|CacheSharedOn |String |表示一個設定網域名稱清單。多個網域名稱之間使用逗號（,）分隔。 |`www.example.com,abc.example.com` |
|TargetHost |String |表示目標網域名稱。 |`www.example.com` |
|UpdateTime |Long |表示該設定的最近更新時間，格式是 Unix 時間標記，單位是秒。 |`1755831922` |
|PageNumber |Long |表示您指定的 `PageNumber`。 |`1` |
|PageSize |Long |表示您指定的 `PageSize`。 |`10` |
|Total |Long |表示符合過濾條件的設定數量。 |`3` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=ListCacheSharedDomains&Version=2021-03-01
{
    "ExactMatch": false,
    "PrimaryDomain": "example"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20250910102143FC1FDB61C3CFED0130C4",
        "Action": "ListCacheSharedDomains",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": [
            {
                "CacheSharedOn": "www.example.com,abc.example.com",
                "TargetHost": "www.example.net",
                "UpdateTime": 1755831922
            },
            {
                "CacheSharedOn": "docs.example.com",
                "TargetHost": "docs.example.net",
                "UpdateTime": 1749631703
            }
        ],
        "PageNumber": 1,
        "PageSize": 50,
        "Total": 2
    }
}
```


&nbsp;
