---
title: "ListFunctionDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCDNDomain-zh-tw"
---

為指定函數獲取可以關聯的網域名稱的列表。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多可傳送 20 個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListFunctionDomains&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `ListFunctionDomains`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |
|FunctionId |String |是 |需要關聯網域名稱的函數的ID。 |
|Page |Integer |是 |頁碼 |
|Limit |Integer |是 |每頁記錄數。<br><br>&nbsp;<br><br>&nbsp;<br><br>目前，一次最多可取得50條記錄。 |
|OrderBy |Integer |否 |該參數指定資料查詢的順序。它接受以下值：<br><br><br>* 1：降序排列資料。<br><br>* 2（預設）：升序排列資料。 |


<span id="返回參數"></span>
## 返回參數


|參數 |類型 |描述 |範例值 |
|---|---|---|---|
|Domains |Object[] |網域名稱列表。 |`["test.example.com"]` |
|Domain |String |網域名稱。 |`test.example.com` |
|BindStatus |Integer |網域名稱與指定函數之間的關聯狀態：<br><br><br>* 1：已關聯<br><br>* 2：可關聯<br><br>* 3：無法關聯 |`2` |
|TotalCount |Long |函數總數。 |`1` |


<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListFunctionDomains&Version=2021-03-01&FunctionId=b21f19d28c7f4fbbb8b8bc799f28****&Page=1&Limit=10
```


<span id="返回範例"></span>
### 返回範例

```json
{
    "ResponseMetadata": {
        "RequestId": "2023050920020063355B94DB6C32617243",
        "Action": "ListFunctionDomains",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domains": [
            {
                "Domain": "123.example.com",
                "BindStatus": 2
            },
            {
                "Domain": "test.example.com",
                "BindStatus": 2
            }
        ],
        "TotalCount": 3
    }
}
```


&nbsp;
