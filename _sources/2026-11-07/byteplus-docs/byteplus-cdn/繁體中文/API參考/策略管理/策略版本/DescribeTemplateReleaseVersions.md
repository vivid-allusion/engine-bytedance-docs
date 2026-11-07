---
title: "DescribeTemplateReleaseVersions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_zh-tw"
---

取得指定策略的版本清單。您可以額外指定欄位對版本清單進行篩選和排序。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">每個策略最多記錄 50 個已發佈的版本。</div>


<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeTemplateReleaseVersions&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeTemplateReleaseVersions`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|TemplateId |String |是 |表示要取得版本清單的策略 ID。 |`tpl-s18ynd9` |
|Filters |Object[] |否 |表示一個篩選條件清單，最多包含 10 個條件。 | |
|Name |String |否 |表示篩選物件。該參數有以下取值：<br><br><br>* `Status`：表示指定策略狀態對版本清單進行篩選。<br><br>* `Version`：表示指定版本號對版本清單進行篩選。 |`Status` |
|Value |String[] |否 |表示篩選值清單。<br><br><br>* 當 `Name` 是 `Status` 時，您可以指定以下篩選值中一個或者多個：<br><br>   * `stop`：表示狀態是「暫停」。<br><br>   * `running`：表示狀態是「執行中」。<br><br>   * `draft`：表示狀態是「草稿」。<br><br>* 當 `Name` 是 `Version` 時，您可以指定一個或者多個版本號，最多 10 個。 |`["stop","running"]` |
|Fuzzy |Boolean |否 |表示匹配方式。該參數值只能是 `false`，表示精確匹配。<br><br>該參數的預設值是 `false`。 |`false` |
|SortRule |Object |否 |表示排序規則。 | |
|OrderBy |String |否 |表示排序物件。該參數有以下取值：<br><br><br>* `CreateTime`：表示版本的建立時間。<br><br>* `ReleaseTime`：表示版本最近發布的時間。<br><br>* `Version`：表示版本號。 |`CreateTime` |
|Asc |Boolean |否 |表示排序順序，該參數有以下取值：<br><br><br>* `false`：表示按降序排序。<br><br>* `true`：表示按升序排序。<br><br><br>該參數的預設值是 `false`。 |`false` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|Total |Long |表示符合篩選條件的版本數量。 |`10` |
|Versions |Object[] |表示符合條件的版本清單。 | |
|Version |String |表示清單中一個版本的版本號。<br><br><br>* 如果 `Status` 為 `draft`，版本號為 `draft`。<br><br>* 如果 `Status` 不是 `draft`，版本號是一個字串，命名規範是 `P-<first_publish_date>-<random_5_digits>`。 |`P-250414.89520` |
|CreateTime |Long |表示該版本的建立時間，格式為 Unix 時間戳記。 |`1744610623` |
|Env |String |表示該版本的發布環境。<br><br><br>* 如果 `Status` 不是 `draft`，該參數值始終是 `prod`，表示線上環境。<br><br>* 如果 `Status` 是 `draft`，該參數值是空（""）。 |`prod` |
|Message |String |表示該版本的描述。 |`my desc` |
|ReleaseTime |Long |表示該版本最近一次的發布時間，格式為 Unix 時間戳記。 |`1744610623` |
|Status |String |表示該版本的狀態。<br><br><br>* `stop`：表示狀態是「暫停」。<br><br>* `running`：表示狀態是「執行中」。<br><br>* `draft`：表示狀態是「草稿」。 |`stop` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplateReleaseVersions&Version=2021-03-01
{
    "TemplateId": "tpl-s18ynd9",
    "Filters": [
        {
            "Name": "Status",
            "Value": [
                "stop",
                "running",
                "draft"
            ]
        }
    ],
    "SortRule": {
        "OrderBy": "CreateTime",
        "Asc": true
    }
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202504140728216B5EA730EF294C000118",
        "Action": "DescribeTemplateReleaseVersions",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Total": 3,
        "Versions": [
            {
                "CreateTime": 1744361302,
                "Env": "prod",
                "Message": "aaa",
                "ReleaseTime": 1744613891,
                "Status": "running",
                "Version": "P-250411.16282"
            },
            {
                "CreateTime": 1744364788,
                "Env": "prod",
                "Message": "sdfgh",
                "ReleaseTime": 1744599039,
                "Status": "stop",
                "Version": "P-250414.89520"
            },
            {
                "CreateTime": 1744610623,
                "Env": "",
                "Message": "",
                "ReleaseTime": 1744610623,
                "Status": "draft",
                "Version": "draft"
            }
        ]
    }
}
```


&nbsp;
