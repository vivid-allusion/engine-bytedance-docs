---
title: "GetFunction"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetFunction-zh-tw"
---

取得指定函數的詳細資訊。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多可傳送 20 個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetFunction&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `GetFunction`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |
|FunctionId |String |是 |函數 ID。您可以呼叫[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-zh-tw)取得函數 ID。 |


<span id="返回參數"></span>
## 返回參數


|參數 |類型 |描述 |範例值 |
|---|---|---|---|
|AccountIdentity |Long |BytePlus 帳戶 ID。 |`20****` |
|UserIdentity |Long |該參數無實際意義。請忽略該參數。 | |
|Domain |String[] |綁定到函數的網域名稱。 |`["example.com"]` |
|Name |String |函數的名稱。 |`hello-ve` |
|ClazzName |String |該參數無實際意義。請忽略該參數。 | |
|BindingType |Integer |該參數無實際意義。請忽略該參數。 | |
|FunctionId |String |函數的 ID。 |`3gyz993****` |
|Status |Integer |函數狀態。<br><br><br>* 100：執行中<br><br>* 400：未關聯<br><br>* 500：設定中 |`100` |
|IsPublish |Boolean |該參數無實際意義。請忽略該參數。 | |
|IsFullPublish |Boolean |該參數無實際意義。請忽略該參數。 | |
|CodeType |String |該參數無實際意義。請忽略該參數。 | |
|Creator |String |建立函數的使用者名稱。 |`example` |
|CreateTime |Long |建立時間。格式為 Unix 時間戳（秒）。 |`1638326159` |
|UpdateTime |Long |更新時間。格式為 Unix 時間戳（秒）。 |`1638326159` |
|Remark |String |函數的備註。 |`this is a test` |
|ProjectName |String |函數所屬專案的名稱。 |`default` |


<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```HTTP
GET  https://cdn.byteplusapi.com?Action=GetFunction&Version=2021-03-01&FunctionId=bc36dc7c58e942f0b9f125d186df****
```


<span id="返回範例"></span>
### 返回範例

```json

{
    "ResponseMetadata": {
        "RequestId": "202404220913431B87E7D87928AD8F48BE",
        "Action": "GetFunction",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Function": {
            "AccountIdentity": 300000****,
            "UserIdentity": 0,
            "Domain": [
                "test.example.com"
            ],
            "Name": "test",
            "ClazzName": "Free",
            "BindingType": 0,
            "FunctionId": "bc36dc7c58e942f0b9f125d186df****",
            "Status": 400,
            "IsPublish": true,
            "IsFullPublish": true,
            "CodeType": "js",
            "Creator": "test_user",
            "CreateTime": 1713776330,
            "UpdateTime": 1713776330,
            "Remark": "",
            "ProjectName": "default"
        }
    }
}
```


&nbsp;
