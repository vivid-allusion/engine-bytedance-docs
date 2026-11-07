---
title: "ListFunction"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-zh-tw"
---

取得函數清單。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多可傳送 20 個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListFunction&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `ListFunction`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |
|Page |Integer |否 |頁碼。 |
|Limit |Integer |否 |每頁記錄數。預設為 100。每次最多可取得 100 條記錄。 |
|OrderBy |Integer |否 |該參數指定資料查詢的順序。它接受以下值：<br><br><br>* 1：降序排列資料。<br><br>* 2（預設）：升序排列資料。 |
|OrderType |String |否 |可用的排序類型有：<br><br><br>* create_time（預設）：根據建立時間對資料進行排序。<br><br>* update_time：根據最後更新時間對資料进行排序。 |
|Status |String |否 |函數的狀態。<br><br><br>* 100：執行中<br><br>* 400：未關聯<br><br>* 500：設定中 |


<span id="返回參數"></span>
## 返回參數


|參數 |類型 |描述 |範例值 |
|---|---|---|---|
|Functions |Object[] |函數清單。 | |
|AccountIdentity |Long |BytePlus 帳戶 ID。 |`20****` |
|UserIdentity |Long |該參數無實際意義。請忽略該參數。 | |
|Domain |String[] |綁定到函數的網域名稱。 |`["example.com"]` |
|Name |String |函數的名稱。 |`hello-ve` |
|FunctionId |String |函數的 ID。 |`3gyz993****` |
|Status |Integer |函數狀態。<br><br><br>* 100：執行中<br><br>* 400：未關聯<br><br>* 500：設定中 |`100` |
|Creator |String |建立函數的使用者名稱。 |`example` |
|CreateTime |Long |建立時間。格式為 Unix 時間戳（秒）。 |`1638326159` |
|UpdateTime |Long |更新時間。格式為 Unix 時間戳（秒）。 |`1638326159` |
|Remark |String |函數的備註。 |`this is a test` |
|ProjectName |String |函數所屬專案的名稱。 |`default` |
|TotalCount |Long |函數總數。 |`1` |


<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListFunction&Version=2021-03-01
```


<span id="返回範例"></span>
### 返回範例

```json

{
  "ResponseMetadata": {
    "RequestId": "202404220913221B87E7D87928AD8F42F8",
    "Action": "ListFunction",
    "Version": "2021-03-01",
    "Service": "CDN",
    "Region": "ap-singapore-1"
  },
  "Result": {
        "Functions": [
            {
                "AccountIdentity": 300000****,
                "UserIdentity": 0,
                "Domain": [
                    "test1.example.com"
                ],
                "Name": "test1",
                "ClazzName": "Free",
                "BindingType": 200,
                "FunctionId": "54ac587666c148a6b9ffacbb0cb1****",
                "Status": 100,
                "IsPublish": true,
                "IsFullPublish": true,
                "CodeType": "",
                "Creator": "example_user",
                "CreateTime": 1711004239,
                "UpdateTime": 1713270175,
                "Remark": "",
                "ProjectName": "default"
            },
            {
                "AccountIdentity": 300000****,
                "UserIdentity": 0,
                "Domain": [
                    "test2.example.com"
                ],
                "Name": "test",
                "ClazzName": "Free",
                "BindingType": 0,
                "FunctionId": "bc36dc7c58e942f0b9f125d186df****",
                "Status": 400,
                "IsPublish": false,
                "IsFullPublish": false,
                "CodeType": "",
                "Creator": "example_user",
                "CreateTime": 1713776330,
                "UpdateTime": 1713776330,
                "Remark": "",
                "ProjectName": "default"
            }
        ],
        "TotalCount": 2
    }
}
```


&nbsp;
