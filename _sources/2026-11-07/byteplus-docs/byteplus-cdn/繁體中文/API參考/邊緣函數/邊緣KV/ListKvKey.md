---
title: "ListKvKey"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvKey-zh-tw"
---

取得儲存空間中的索引鍵值對列表。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多發送 20 個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListKvKey&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `ListKvKey`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |
|Namespace |String |是 |儲存空間的名稱。您可以透過呼叫介面[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-zh-tw)取得。 |
|NamespaceId |String |是 |儲存空間的 ID。您可以透過呼叫介面[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-zh-tw)取得。 |
|Page |Integer |否 |頁碼。 |
|Limit |Integer |否 |每頁記錄數。預設為 50 條。<br><br>最多為 50 條。 |
|OrderBy |Integer |否 |該參數指定查詢索引鍵值對的順序，接受以下值：<br><br><br>* 1：降序排列索引鍵值對。<br><br>* 2（預設）：升序排列索引鍵值對。 |
|OrderType |String |否 |可用的排序類型有：<br><br><br>* create_time（預設）：根據建立時間排序索引鍵值對。<br><br>* update_time：根據最後更新時間排序索引鍵值對。 |


<span id="返回參數"></span>
## 返回參數


|參數 |類型 |描述 |範例值 |
|---|---|---|---|
|NamespaceKeys |Object |儲存空間中的索引鍵值對詳情。 | |
|Namespace |String |索引鍵值對所屬的儲存空間的名稱。 |`test-kv1` |
|NamespaceId |String |索引鍵值對所屬的儲存空間的 ID。 |`14776510402228****` |
|Key |String |索引鍵。 |`testkey` |
|KeyStatus |Integer |索引鍵值對狀態。<br><br><br>* 100：已過期<br><br>* 200：正常 |`200` |
|DDL |Long |索引鍵值對的過期時間。索引鍵值對過期後，Key 中的 Value 將無法存取。<br><br><br>* 以 UNIX 時間標記格式顯示。<br><br>* 0：永久儲存。 |`0` |
|CreateTime |Long |索引鍵值對的建立時間。以 UNIX 時間標記格式顯示。 |`1662005890` |
|UpdateTime |Long |索引鍵值對的更新時間。以 UNIX 時間標記格式顯示。 |`1664337001` |
|TotalCount |Long |儲存空間中的索引鍵值對總數。 |`2` |


<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListKvKey&Version=2021-03-01&Namespace=test-kv1&NamespaceId=46d79a9944ae2fd81f2643e2fe5ef42d****&Page=1&Limit=10&OrderBy=2&OrderType=create_time
```


<span id="返回範例"></span>
### 返回範例

```json

{
    "ResponseMetadata": {
        "RequestId": "20230810210051741B321D8****",
        "Action": "ListKvKey",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "NamespaceKeys": [
            {
                "Namespace": "test-kv1",
                "NamespaceId": "14776510402****",
                "Key": "testkey",
                "KeyStatus": 200, 
                "DDL": 0,
                "CreateTime": 1678085786,
                "UpdateTime": 1678085786
            },
            {
                "Namespace": "test-kv1",
                "NamespaceId": "14776510402****",
                "Key": "key",
                "KeyStatus": 100,
                "DDL": 1678259532,
                "CreateTime": 1678092385,
                "UpdateTime": 1682327035
            },
        ],
        "TotalCount": 2
    }
}
```


&nbsp;
