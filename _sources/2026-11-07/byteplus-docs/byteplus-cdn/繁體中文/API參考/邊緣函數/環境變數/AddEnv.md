---
title: "AddEnv"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-AddEnv-zh-tw"
---

為指定的函數新增環境變數。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您對環境變數的新增刪除修改操作在函數被再次發佈後才會生效。</div>


<span id="使用說明"></span>
## 使用說明

請求限流：每秒最多可發送20個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=AddEnv&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `AddEnv`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |是否必選 |描述 |範例值 |
|---|---|---|---|---|
|FunctionId |String |是 |函數 ID。您可以呼叫[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-zh-tw)取得函數 ID。 |`23455331245` |
|Envs |Object[] |是 |環境變數。 |`[{"Key": "abc","Value": "123"}]` |
|Key |String |是 |環境變數的鍵。 |`abc` |
|Value |String |是 |環境變數的值。 |`123` |


<span id="返回參數"></span>
## 返回參數

無

<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```json
POST  https://cdn.byteplusapi.com?Action=AddEnv&Version=2021-03-01
{
    "FunctionId": "23455331245",
    "Envs": [
        {
            "Key": "abc",
            "Value": "123"
        }
    ]
}
```
