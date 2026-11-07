---
title: "UpdateKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateKvNamespace-zh-tw"
---

修改儲存空間的描述。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多發送20個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=UpdateKvNamespace&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `UpdateKvNamespace`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |是否必選 |描述 |範例值 |
|---|---|---|---|---|
|Namespace |String |是 |儲存空間的名稱。您可以透過呼叫介面[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-zh-tw)取得。 |`test-kv1` |
|NamespaceId |String |是 |儲存空間的 ID。您可以透過呼叫介面[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-zh-tw)取得。 |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|Description |String |否 |儲存空間的新描述資訊，長度不得超過80個字元。如果未指定此參數，則保留原始描述。 |`test` |


<span id="返回參數"></span>
## 返回參數

無

<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```json
POST   https://cdn.byteplusapi.com?Action=UpdateKvNamespace&Version=2021-03-01
{
    "Namespace": "test-kv1",
    "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
    "Description": "test"
}
```
