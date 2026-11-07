---
title: "ListCronJobTaskLog"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCronJobTaskLog-zh-tw"
---

獲取指定 Cron 觸發器的任務執行日誌列表。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多發送20個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListCronJobTaskLog&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `ListCronJobTaskLog`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |
|FunctionId |String |是 |函數 ID。您可以呼叫[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-zh-tw)獲取函數 ID。 |
|JobName |String |是 |Cron 觸發器名稱。 |
|Uuid |String |是 |任務的 UUID。您可以呼叫 [ListCronJobTask](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCronJobTask-zh-tw) 獲取任務的 UUID。 |
|Page |Integer |否 |頁碼。 |
|Limit |Integer |否 |每頁記錄數。預設為 50 條。最大為 50 條。 |
|OrderBy |Integer |否 |該參數指定查詢數據的順序，接受以下值：<br><br><br>* 1：降序排列數據。<br><br>* 2（預設）：升序排列數據。 |


<span id="返回參數"></span>
## 返回參數


|參數 |類型 |描述 |範例值 |
|---|---|---|---|
|Logs |Object[] |日誌列表。 | |
|JobName |String |任務名稱。 |`cron1` |
|CronExpression |String |Cron 表示式。 |`*/1 * * **` |
|Parameter |String |自訂參數。 |`cron` |
|Continent |String |大洲。 |`America` |
|Country |String |國家或地區。 |`America` |
|JobState |Long |任務狀態。<br><br><br>* 1：已執行<br><br>* 3：已禁用<br><br>* 4：未執行 |`1` |
|Description |String |任務描述。 |`test` |
|Uuid |String |任務的 UUID |`2xuls***` |
|SchedulerState |Long |任務狀態。<br><br><br>* 5：執行失敗。<br><br>* 6：執行完成。 |`5` |
|ResponseMsg |String |回應訊息 |`this is a msg` |
|CreateTime |Long |建立時間。 |`1638326159` |
|UpdateTime |Long |更新時間。 |`1638326159` |
|TotalCount |Long |日誌的總數。 |`1` |


<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListCronJobTaskLog&Version=2021-03-01&FunctionId=3gyz993****&JobName=cron1&Uuid=2xl2l4u****&Page=1&Limit=10&OrderBy=2
```


<span id="返回範例"></span>
### 返回範例

```json

{
    "ResponseMetadata": {
        "RequestId": "20211207213413010225146063****",
        "Action": "ListCronJobTaskLog",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Logs": [
            {
                "JobName": "cron1",
                "CronExpression": "*/30 * * * *",
                "Event": "cron",
                "Parameter": "cron_all",
                "ClusterName": "test-local",
                "ClusterAlias": "telecom",
                "JobState": 1,
                "Uuid": "2xl2****",
                "SchedulerState": 6,
                "ResponseMsg": "",
                "CreateTime": 1639625401,
                "UpdateTime": 1639625401
            }
        ],
        "TotalCount": 1
    }
}
```


&nbsp;
