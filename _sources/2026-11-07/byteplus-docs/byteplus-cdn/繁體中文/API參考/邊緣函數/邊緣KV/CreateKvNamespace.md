---
title: "CreateKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateKvNamespace-zh-tw"
---

建立儲存空間。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多傳送 20 個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=CreateKvNamespace&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `CreateKvNamespace`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |是否必選 |描述 |範例值 |
|---|---|---|---|---|
|Namespace |String |是 |為儲存空間設定一個可識別的名稱。輸入要求如下：<br><br><br>* 長度應在 2 到 64 個字元之間。<br><br>* 只能包含英文字母、數字、連字號(\-)和底線(_)。<br><br>* 不區分大小寫，這意味著「Namespace」和「NAMESPACE」被認為是相同的。另外，邊緣函數不會對大小寫進行轉換。 |`test-kv1` |
|Description |String |否 |為儲存空間設定描述。長度不得超過 80 個字元。 |`test` |
|ProjectName |String |否 |儲存空間所屬的專案名稱，預設為`default`。 |`default` |


<span id="返回參數"></span>
## 返回參數

無

<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```json
POST   https://cdn.byteplusapi.com?Action=CreateKvNamespace&Version=2021-03-01
{
    "Namespace": "test-kv1",
    "Description": "test",
    "ProjectName": "default"
}
```


&nbsp;
