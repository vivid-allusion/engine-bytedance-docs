---
title: "ListContinentCluster"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListContinentCluster-zh-tw"
---

獲取金絲雀環境或全量環境的邊緣伺服器列表。

<span id="使用說明"></span>
## 使用說明

請求限流：每秒最多可傳送 20 個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListContinentCluster&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `ListContinentCluster`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |
|FunctionId |String |是 |函數 ID。您可以呼叫[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-zh-tw)獲取函數 ID。 |
|Continents |String |否 |指定大洲。可以指定多個大洲，用逗號分隔。 |
|Countries |String |否 |指定國家。可以指定多個國家，用逗號分隔。 |
|ClusterType |Integer |否 |發佈環境類型。<br><br><br>* 100：金絲雀環境。<br><br>* 200：全量環境。 |
|Page |Integer |否 |邊緣伺服器列表的頁碼。<br><br>如果 Page 和 Limit 參數都不被指定，將返回全量資料；如果僅指定 Limit，不指定 Page ，將返回第 1 頁資料；如果僅指定 Page，不指定 Limit，將返回全量資料；如果 Page 和 Limit 都指定，將返回符合條件的資料。 |
|Limit |Integer |否 |每頁記錄數。目前，每頁最多可獲取 50 條記錄。<br><br>如果 Page 和 Limit 參數都不被指定，將返回全量資料；如果僅指定 Limit，不指定 Page ，將返回第 1 頁資料；如果僅指定 Page，不指定 Limit，將返回全量資料；如果 Page 和 Limit 都指定，將返回符合條件的資料。 |
|OrderBy |Integer |否 |邊緣伺服器的排序方式。<br><br><br>* 1：降序排列資料。<br><br>* 2（預設）：升序排列資料。 |


<span id="返回參數"></span>
## 返回參數


|參數 |類型 |描述 |範例值 |
|---|---|---|---|
|ContinentCluster |Object[] |邊緣伺服器列表。 | |
|Country |String |邊緣伺服器所在的國家或地區。 |`Singapore` |
|Continent |String |邊緣伺服器所在的大洲。 |`Asia` |
|ClusterType |Integer |邊緣伺服器類型。<br><br><br>* 100：金絲雀發佈邊緣伺服器<br><br>* 200：全量發佈邊緣伺服器 |`100` |
|Traffic |String |部署在該邊緣伺服器上函數的版本號。 |`[{"version_tag":"1.0.1"}]` |
|TotalCount |Long |符合查詢條件的邊緣伺服器總數。 |`1` |


<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListContinentCluster&Version=2021-03-01&FunctionId=b21f19d28c7f4fbbb8b8bc799f28****
```


<span id="返回範例"></span>
### 返回範例

```json

{
    "ResponseMetadata": {
        "RequestId": "2022011310531001022511001100*****",
        "Action": "ListContinentCluster",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ContinentCluster": [
            {
                "Continent": "Europe",
                "Country": "France",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Turkey",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Philippines",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Japan",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Malaysia",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Saudi Arabia",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "South America",
                "Country": "Brazil",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "South Korea",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Europe",
                "Country": "Russia",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Thailand",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Indonesia",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "North America",
                "Country": "United States",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Singapore",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Vietnam",
                "ClusterType": 100,
                "Traffics": "[{\\"version_tag\\":\\"1.0.1\\"}]"
            },
            {
                "Continent": "Europe",
                "Country": "Germany",
                "ClusterType": 100,
                "Traffics": ""
            }
        ],
        "TotalCount": 15
    }
}
```


&nbsp;
