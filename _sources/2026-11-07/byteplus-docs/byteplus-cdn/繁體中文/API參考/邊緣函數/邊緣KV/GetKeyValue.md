---
title: "GetKeyValue"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetKeyValue-zh-tw"
---

查看索引鍵值對的值和過期時間。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多發送 20 個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetKeyValue&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `GetKeyValue`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |
|Namespace |String |是 |儲存空間的名稱。您可以透過呼叫介面[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-zh-tw)取得。 |
|NamespaceId |String |是 |儲存空間的 ID。您可以透過呼叫介面[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-zh-tw)取得。 |
|Key |String |是 |您要查詢值或過期時間的索引鍵。 |


<span id="返回參數"></span>
## 返回參數


|參數 |類型 |描述 |範例值 |
|---|---|---|---|
|DDL |Long |索引鍵值對的過期時間。索引鍵值對過期後，函數將無法存取 Key 的 Value。<br><br><br>* 以秒級 Unix 時間標記格式顯示。<br><br>* 0：永不過期。 |`0` |
|Key |String |查詢的索引鍵。 |`testkey` |
|Value |String |查詢的索引鍵的值。值為 Base64 編碼格式。 |`dGVzdHZhbHVlMTIz` |


<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```HTTP
GET   https://cdn.byteplusapi.com?Action=GetKeyValue&Version=2021-03-01&Namespace=test-kv1&NamespaceId=46d79a9944ae2fd81f2643e2fe5ef42d****&Key=testkey
```


<span id="返回範例"></span>
### 返回範例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetKeyValue",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DDL": 0,
        "Key": "testkey",
        "Value": "dGVzdHZhbHVlMTIz"
    }
}
```


&nbsp;
