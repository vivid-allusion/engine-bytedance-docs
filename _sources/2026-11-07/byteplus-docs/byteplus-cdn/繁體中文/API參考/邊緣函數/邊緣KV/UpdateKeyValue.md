---
title: "UpdateKeyValue"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateKeyValue-zh-tw"
---

修改鍵值對的值和有效時長。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多發送20個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=UpdateKeyValue&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `UpdateKeyValue`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |是否必選 |描述 |範例值 |
|---|---|---|---|---|
|Namespace |String |是 |儲存空間的名稱。您可以透過呼叫介面[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-zh-tw)取得。 |`test-kv1` |
|NamespaceId |String |是 |儲存空間的 ID。您可以透過呼叫介面[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-zh-tw)取得。 |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|Key |String |是 |您要修改值或儲存時間的鍵。您可以透過呼叫介面[ListKvKey](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvKey-zh-tw)取得。 |`testkey` |
|Value |String |是 |輸入新的值。如果不指定此參數，則保留原始值。輸入要求如下：<br><br><br>* 只能輸入Base64編碼格式。<br><br>* 不超過128KB。 |`dGVzdDEyMw==` |
|TTL |Long |是 |輸入新的有效時長。單位：秒。鍵值對過期後無法被存取。如果不指定此參數，則保留原始值。<br><br><br>* 0：永不過期。<br><br>* 有效時長不能少於60秒。 |`0` |


<span id="返回參數"></span>
## 返回參數

無

<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```json
POST  https://cdn.byteplusapi.com?Action=UpdateKeyValue&Version=2021-03-01
{
    "Namespace": "test-kv1",
    "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
    "Key": "testkey",
    "Value": "dGVzdDEyMw==",
    "TTL": 0
}
```


&nbsp;
