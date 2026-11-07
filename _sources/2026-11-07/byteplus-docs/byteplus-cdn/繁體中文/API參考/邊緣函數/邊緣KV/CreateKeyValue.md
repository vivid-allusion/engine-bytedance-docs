---
title: "CreateKeyValue"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateKeyValue-zh-tw"
---

在儲存空間中新增鍵值對。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多傳送 20 個請求。


* 新增鍵值對成功後，Key 不可修改。

* 同一儲存空間中的 Key 不能相同。Key 不區分大小寫，即 `Key` 和 `KEY` 被視為相同。


<span id="請求說明"></span>
## 請求說明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=CreateKeyValue&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `CreateKeyValue`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |是否必選 |描述 |範例值 |
|---|---|---|---|---|
|Namespace |String |是 |儲存空間的名稱。您可以透過呼叫介面[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-cn)取得。 |`test-kv1` |
|NamespaceId |String |是 |儲存空間的 ID。您可以透過呼叫介面[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-cn)取得。 |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|Key |String |是 |鍵。輸入要求如下：<br><br><br>* 只能包含英文字母、數字、短橫線（\-）和底線（_）。<br><br>* 不超過 512 位元組。 |`testkey` |
|Value |String |是 |值。輸入要求如下：<br><br><br>* 只能輸入 Base64 編碼格式。<br><br>* 不超過 128KB。 |`dGVzdHZhbHVlMTIz` |
|TTL |Long |否 |設定鍵值對的有效時長。單位：秒。鍵值對過期後，邊緣函數將無法讀取 Key 的 Value。<br><br><br>* 如果未指定此參數或參數值為 0，則永不過期。<br><br>* 有效時長不得少於 60s。 |`0` |


<span id="返回參數"></span>
## 返回參數

無

<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```json
POST   https://cdn.byteplusapi.com?Action=CreateKeyValue&Version=2021-03-01
{
    "Namespace": "test-kv1",
    "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
    "Key": "testkey",
    "Value": "dGVzdHZhbHVlMTIz",
    "TTL": 0
}
```


&nbsp;
