---
title: "DescribeCdnRegionAndIsp"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeCdnRegionAndIsp_zh-tw"
---

獲取 BytePlus IP 地址資料庫所涵蓋的中國省級行政區、全球的國家和地區、以及中國大陸網路營運商的名稱和代碼。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeCdnRegionAndIsp&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeCdnRegionAndIsp`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Area |String |否 |表示查詢的範圍。該參數有以下取值：<br><br><br>* `China`：表示中國省級行政區和中國內地網路營運商的代碼和名稱。<br><br>* `Global`：表示全球國家和地區、以及中國內地網路營運商的代碼和名稱。<br><br><br>該參數的預設值是 `China`。 |`Global` |
|Lang |String |否 |表示查詢結果顯示的語言。該參數有以下取值：<br><br><br>* `zh`：表示簡體中文。<br><br>* `en`：表示英文。<br><br><br>該參數的預設值是 `en`。 |`en` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|Isps |Object[] |表示中國內地的網路營運商。 | |
|Code |String |表示一個網路營運商的代碼。 |`CU` |
|Name |String |表示該網路營運商的名稱。 |`China Unicom` |
|Regions |Object[] |表示一個區域列表。<br><br><br>* 如果 `Area` 是 `Global`，該參數表示一個全球各國家和地區的列表。<br><br>* 如果 `Area` 是 `China`，該參數表示一個中國各省級行政區的列表。 | |
|Code |String |表示一個國家、地區、或中國省級行政區的代碼。 |`BJ` |
|Name |String |表示該國家、地區、或中國省級行政區的名稱。 |`Beijing` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCdnRegionAndIsp&Version=2021-03-01
{
    "Area": "Global"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20240423061106DA1BD20A355B07CBEC2D",
        "Action": "DescribeCdnRegionAndIsp",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Isps": [
            {
                "Code": "CT",
                "Name": "China Telecom"
            },
            {
                "Code": "CM",
                "Name": "China Mobile"
            },
            {
                "Code": "CU",
                "Name": "China Unicom"
            },
            {
                "Code": "GWBN",
                "Name": "Great Wall Broadband"
            },
            ...
        ],
        "Regions": [
            {
                "Code": "CHE",
                "Name": "Switzerland"
            },
            {
                "Code": "AZE",
                "Name": "Azerbaijan"
            },
            {
                "Code": "PNG",
                "Name": "Papua New Guinea"
            },
            {
                "Code": "PSE",
                "Name": "Palestine"
            },
            {
                "Code": "FSM",
                "Name": "Micronesia"
            },
            ...
        ]
    }
}
```


&nbsp;
