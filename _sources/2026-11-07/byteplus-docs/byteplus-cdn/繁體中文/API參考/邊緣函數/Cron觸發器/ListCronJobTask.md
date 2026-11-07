---
title: "ListCronJobTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCronJobTask-zh-tw"
---

獲取指定 Cron 觸發器的任務執行列表。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多發送20個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListCronJobTask&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `ListCronJobTask`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |
|FunctionId |String |是 |函數 ID。您可以呼叫[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-zh-tw)獲取函數 ID。 |
|JobName |String |是 |觸發器名稱。 |
|Page |Integer |否 |頁碼。 |
|Limit |Integer |否 |每頁記錄數。預設為 50 條。最多為 50 條。 |
|OrderBy |Integer |否 |該參數指定查詢數據的順序，接受以下值：<br><br><br>* 1：降序排列數據。<br><br>* 2（預設）：升序排列數據。 |


<span id="返回參數"></span>
## 返回參數


|參數 |類型 |描述 |範例值 |
|---|---|---|---|
|Tasks |Object[] |Cron 觸發器的任務執行列表。 | |
|JobName |String |Cron 觸發器的名稱。 |`cron1` |
|CronExpression |String |Cron 表示式。 |`*/1 * * **` |
|Parameter |String |自訂參數。 |`cron` |
|CronTaskStatus |Long |任務狀態。 |`1` |
|Description |String |任務描述。 |`test` |
|Uuid |String |任務的 UUID。 |`2xju****` |
|CreateTime |Long |建立時間。 |`1638326159` |
|UpdateTime |Long |更新時間。 |`1638326159` |
|TotalCount |Long |任務執行記錄的總數。 |`1` |


<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListCronJobTask&Version=2021-03-01&FunctionId=3gyz993****&JobName=cron1&Page=1&Limit=10&OrderBy=2
```


<span id="返回範例"></span>
### 返回範例

```json

{
    "ResponseMetadata": {
        "RequestId": "20211207213413010225146063****",
        "Action": "ListCronJobTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Tasks": [
            {
                "JobName": "cron1",
                "CronExpression": "*/30 * * * *",
                "Parameter": "cron_all",
                "JobState": 1,
                "CronTaskStatus": 6,
                "Description": "",
                "Uuid": "2xl2****",
                "CreateTime": 1639625400,
                "UpdateTime": 1639625401
            }
        ],
        "TotalCount": 1
    }
}
```


&nbsp;
