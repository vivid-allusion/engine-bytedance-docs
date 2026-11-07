---
title: "ListKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-zh-tw"
---

取得儲存空間列表。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多發送 20 個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListKvNamespace&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `ListKvNamespace`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |
|Page |Integer |否 |頁碼。預設為 1。 |
|Limit |Integer |否 |每頁記錄數。預設為 50 條記錄。<br><br>最多為 50 條記錄。 |
|OrderBy |Integer |否 |該參數指定查詢資料的順序，接受以下值：<br><br><br>* 1：降序排列儲存空間。<br><br>* 2（預設）：升序排列儲存空間。 |
|OrderType |String |否 |可用的排序類型有：<br><br><br>* create_time（預設）：根據建立時間排序儲存空間。<br><br>* update_time：根據最後更新時間排序儲存空間。 |


<span id="返回參數"></span>
## 返回參數


|參數 |類型 |描述 |範例值 |
|---|---|---|---|
|Namespaces |Object |儲存空間列表。 | |
|Namespace |String |儲存空間的名稱。 |`test-kv1` |
|NamespaceId |String |儲存空間的 ID。 |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|Description |String |儲存空間的描述。 |`test` |
|Creator |String |儲存空間的建立者。 |`testuser` |
|CreateTime |Long |建立時間。格式為 Unix 時間標記（秒）。 |`1661864175` |
|UpdateTime |Long |更新時間。格式為 Unix 時間標記（秒）。 |`1678288603` |
|TotalCount |Long |儲存空間的總數量。 |`2` |


<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListKvNamespace&Version=2021-03-01&Page=1&Limit=10&OrderBy=2&OrderType=create_time
```


<span id="返回範例"></span>
### 返回範例

```json

{
    "ResponseMetadata": {
        "RequestId": "20230808095102CFDFA3280****",
        "Action": "ListKvNamespace",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Namespaces": [
            {
                "Namespace": "test-kv1",
                "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
                "Description": "test",
                "Creator": "testuser",
                "CreateTime": 1661864175,
                "UpdateTime": 1678288603
            },
            {
                "Namespace": "asdJSJasdad",
                "NamespaceId": "510257916f6b5503b288d064b7154****",
                "Description": "",
                "Creator": "testuser",
                "CreateTime": 1662005890,
                "UpdateTime": 1664337001
            }
        ],
        "TotalCount": 2
    }
}
```


&nbsp;
