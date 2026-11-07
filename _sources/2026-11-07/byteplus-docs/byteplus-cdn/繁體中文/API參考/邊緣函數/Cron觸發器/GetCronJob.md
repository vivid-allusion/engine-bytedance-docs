---
title: "GetCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetCronJob-zh-tw"
---

獲取 Cron 觸發器的詳細資訊。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多可傳送20個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetCronJob&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `GetCronJob`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |
|FunctionId |String |是 |函數 ID。您可以呼叫[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-zh-tw)取得函數 ID。 |
|JobName |String |是 |觸發器名稱。 |


<span id="返回參數"></span>
## 返回參數


|參數 |類型 |描述 |範例值 |
|---|---|---|---|
|Job |Object[] |Cron 觸發器列表。 |`Task details` |
|JobName |String |觸發器名稱。 |`cron2` |
|CronExpression |String |Cron 表示式。 |`*/1 * * **` |
|Parameter |String |自訂參數。 |`cron` |
|Description |String |Cron 觸發器的描述。 |`test` |
|JobState |Long |Cron 觸發器的狀態。<br><br><br>* 1：待排程<br><br>* 3：已停用<br><br>* 4：取消排程 |`1` |
|CronType |Integer |Cron 觸發器的排程類型。<br><br><br>* 1：全球。<br><br>* 2：單點排程。 |`1` |
|CreateTime |Long |建立時間。 |`1638326159` |
|UpdateTime |Long |更新時間。 |`1638326159` |


<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```HTTP
GET https://cdn.byteplusapi.com?Action=GetCronJob&Version=2021-03-01&FunctionId=3gyz993****&JobName=cron2
```


<span id="返回範例"></span>
### 返回範例

```json
{
  "ResponseMetadata": {
    "RequestId": "20211207213413010225146063****",
    "Action": "GetCronJob",
    "Version": "2021-03-01",
    "Service": "CDN",
    "Region": "ap-singapore-1"
  },
  "Result": {
    "Job": {
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
  }
}
```
