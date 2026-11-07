---
title: "ListCountry"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCountry-zh-tw"
---

對於指定的函數，獲取可用的邊緣伺服器所在的國家或地區列表。

<span id="使用說明"></span>
## 使用說明

請求限流：每秒最多可發送20個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListCountry&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |接口名稱。當前 API 的名稱為 `ListCountry`。 |
|Version |String |是 |接口版本。當前 API 的版本為 2021\-03\-01。 |
|FunctionId |String |是 |函數 ID。您可以調用[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-zh-tw)獲取函數 ID。 |
|Continents |String |否 |一個或多個大洲。多個大洲用逗號分隔。 |


<span id="返回參數"></span>
## 返回參數


|參數 |類型 |描述 |示例值 |
|---|---|---|---|
|Countries |String[] |邊緣伺服器所在的國家或地區。 |`["Singapore"]` |


<span id="示例"></span>
## 示例

<span id="請求示例"></span>
### 請求示例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListCountry&Version=2021-03-01&FunctionId=3gyz993****&Continents=\[\"Asia\"]
```


<span id="返回示例"></span>
### 返回示例

```json

{
    "ResponseMetadata": {
        "RequestId": "2022011310531001022511001100*****",
        "Action": "ListCountry",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Countries": [
            "Singapore"
        ]
    }
}
```


&nbsp;
