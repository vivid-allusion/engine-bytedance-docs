---
title: "DeleteMultiKeys"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/api-ref-delete-multikeys-zh-tw"
---

批次刪除索引鍵值對。

<span id="使用說明"></span>
## 使用說明

請求限制：每分鐘最多發送 6 個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=DeleteMultiKeys&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `DeleteMultiKeys`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |是否必選 |描述 |範例值 |
|---|---|---|---|---|
|Namespace |String |是 |儲存空間的名稱。您可以透過呼叫介面[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-zh-tw)取得。 |`test-kv1` |
|NamespaceId |String |是 |儲存空間的 ID。您可以透過呼叫介面[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-zh-tw)取得。 |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|KeyList |Array of strings |是 |要刪除的索引鍵值對的索引鍵。 |`["key1","key2"]` |


<span id="返回參數"></span>
## 返回參數


|參數 |類型 |描述 |範例值 |
|---|---|---|---|
|DeleteResult |Object |刪除結果。 | |
|FailedKeys |Array of strings |刪除失敗的索引鍵。 |`["key1","key2"]` |
|SuccessfulCount |String |成功被刪除的索引鍵的數量。 |`1` |


<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```json
POST  https://cdn.byteplusapi.com?Action=DeleteMultiKeys&Version=2021-03-01
{
  "Namespace": "test-kv1",
  "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
  "KeyList": [
    "key1",
    "key2"
  ]
}
```


<span id="返回範例"></span>
### 返回範例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230808095102CFDFA3280****",
        "Action": "DeleteMultiKeys",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
        "Result": {
            "DeleteResult": {
                "FailedKeys": [
                    "key2"
                ],
                "SuccessfulCount": 1
            }
        }
}        
```
