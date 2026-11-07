---
title: "GetKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetKvNamespace-zh-tw"
---

取得儲存空間的詳細資訊。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多發送 20 個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetKvNamespace&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `GetKvNamespace`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |
|Namespace |String |是 |儲存空間的名稱。您可以透過呼叫介面[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-zh-tw)取得。 |
|NamespaceId |String |是 |儲存空間的 ID。您可以透過呼叫介面[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-zh-tw)取得。 |


<span id="返回參數"></span>
## 返回參數


|參數 |類型 |描述 |範例值 |
|---|---|---|---|
|Namespace |Object |儲存空間詳情。 | |
|Namespace |String |儲存空間的名稱。您可以透過呼叫介面[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-zh-tw)取得。 |`test-kv1` |
|NamespaceId |String |儲存空間的 ID。您可以透過呼叫介面[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-zh-tw)取得。 |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|Description |String |儲存空間的描述。 |`test` |
|Creator |String |儲存空間的建立者。 |`testuser` |
|CreateTime |Long |建立時間。格式為 Unix 時間標記（秒）。 |`1661864175` |
|UpdateTime |Long |更新時間。格式為 Unix 時間標記（秒）。 |`1678288603` |
|ProjectName |String |儲存空間所屬的專案的名稱。 |`default` |


<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```HTTP
GET  https://cdn.byteplusapi.com?Action=GetKvNamespace&Version=2021-03-01&Namespace=test-kv1&NamespaceId=46d79a9944ae2fd81f2643e2fe5ef42d****
```


<span id="返回範例"></span>
### 返回範例

```json

{
    "ResponseMetadata": {
        "RequestId": "202308080952004CD21902****",
        "Action": "GetKvNamespace",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Namespace": {
            "Namespace": "test-kv1",
            "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
            "Description": "test",
            "Creator": "testuser",
            "ProjectName": "default",
            "CreateTime": 1661864175,
            "UpdateTime": 1678288603
        }
    }
}
```


&nbsp;
