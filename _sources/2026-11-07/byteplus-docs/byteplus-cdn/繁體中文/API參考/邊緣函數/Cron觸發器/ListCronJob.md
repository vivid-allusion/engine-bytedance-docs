---
title: "ListCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCronJob-zh-tw"
---

獲取 Cron 觸發器列表。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多可傳送20個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListCronJob&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `ListCronJob`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |
|FunctionId |String |是 |函數 ID。您可以呼叫[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-zh-tw)取得函數 ID。 |
|Page |Integer |否 |頁碼 |
|Limit |Integer |否 |每頁記錄數。預設為 50 條。最多為 50 條。 |
|OrderBy |Integer |否 |該參數指定資料查詢的順序。它接受以下值：<br><br><br>* 1：降序排列資料。<br><br>* 2（預設）：升序排列資料。 |


<span id="返回參數"></span>
## 返回參數


|參數 |類型 |描述 |範例值 |
|---|---|---|---|
|Jobs |Object[] |觸發器列表。 | |
|JobName |String |Cron 觸發器名稱。 |`cron1` |
|CronExpression |String |Cron 表示式。 |`*/1 * * **` |
|Parameter |String |自訂參數。 |`cron` |
|Description |String |觸發器描述。 |`test` |
|JobState |Long |觸發器狀態。<br><br><br>* 1：待排程<br><br>* 3：已停用<br><br>* 4：取消排程 |`1` |
|CronType |Integer |Cron 觸發器排程類型。可能的值有：<br><br>&nbsp;<br><br>1：全球：在全部邊緣伺服器執行。<br><br>&nbsp;<br><br>2：單點排程：隨機在任意一個邊緣伺服器執行。 |`1` |
|CreateTime |Long |建立時間 |`1638326159` |
|UpdateTime |Long |更新時間 |`1638326159` |
|TotalCount |Long |觸發器總數。 |`1` |


<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListCronJob&Version=2021-03-01&FunctionId=3gyz993****&Page=1&Limit=10&OrderBy=2
```


<span id="返回範例"></span>
### 返回範例

```json

{
    "ResponseMetadata": {
        "RequestId": "20211207213413010225146063****",
        "Action": "ListCronJob",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Jobs": [
            {
                "JobName": "cron2",
                "CronExpression": "*/59 * * * *",
                "Parameter": "cron_all",
                "Description": "",
                "JobState": 1,
                "CronType": 2,
                "Operator": "****",
                "CreateTime": 1638871686,
                "UpdateTime": 1638871686
            }
        ],
        "TotalCount": 1
    }
}
```


&nbsp;
