---
title: "UpdateCountryCluster"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateCountryCluster-zh-tw"
---

更新金絲雀環境或全量環境所包含的邊緣伺服器。

<span id="使用說明"></span>
## 使用說明

請求限流：每秒最多可發送20個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=UpdateCountryCluster&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |接口名稱。當前 API 的名稱為 `UpdateCountryCluster`。 |
|Version |String |是 |接口版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |是否必選 |描述 |示例值 |
|---|---|---|---|---|
|FunctionId |String |是 |函數 ID。您可以調用[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-zh-tw)獲取函數 ID。 |`3gyz993****` |
|ClusterType |Integer |是 |類型。<br><br><br>* 100：灰度環境<br><br>* 200：正式環境 |`100` |
|Countries |String[] |是 |邊緣伺服器所在的國家或地區。 |`["Singapore"]` |


<span id="返回參數"></span>
## 返回參數

無

<span id="示例"></span>
## 示例

<span id="請求示例"></span>
### 請求示例

```json
POST  https://cdn.byteplusapi.com?Action=UpdateCountryCluster&Version=2021-03-01
{
    "ClusterType": 200,
    "Countries": [
        "Singapore"
    ],
    "FunctionId": "3gyz993****"
}
```
