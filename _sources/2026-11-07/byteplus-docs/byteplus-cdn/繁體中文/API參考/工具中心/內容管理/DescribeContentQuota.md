---
title: "DescribeContentQuota"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeContentQuota_zh-tw"
---

獲取您 BytePlus 帳號下每日的清除快取和預取任務的配額及配額餘量。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeContentQuota&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeContentQuota`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|PreloadLimit |Long |表示每次可預取的最大 URL 數量。 |`100` |
|PreloadQuota |Long |表示每日可預取的 URL 數量。 |`1000` |
|PreloadRemain |Long |表示今天可預取的 URL 剩餘數量。 |`10` |
|RefreshDirLimit |Long |表示每次可清除快取的最大目錄數量。 |`100` |
|RefreshDirQuota |Long |表示每日可清除快取的目錄數量。 |`50` |
|RefreshDirRemain |Long |表示今天可清除快取的目錄剩餘數量。 |`15` |
|RefreshQuota |Long |表示每日可清除快取的 URL 數量。 |`10000` |
|RefreshQuotaLimit |Long |表示每次可清除快取的最大 URL 數量。 |`100` |
|RefreshRemain |Long |表示今天可清除快取的 URL 剩餘數量。 |`200` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeContentQuota&Version=2021-03-01
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202310271225559FCEDC662FFE48246DCB",
        "Action": "DescribeContentQuota",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "PreloadLimit": 100,
        "PreloadQuota": 1000,
        "PreloadRemain": 1000,
        "RefreshDirLimit": 100,
        "RefreshDirQuota": 50,
        "RefreshDirRemain": 50,
        "RefreshQuota": 10000,
        "RefreshQuotaLimit": 100,
        "RefreshRemain": 1000
    }
}
```


&nbsp;
