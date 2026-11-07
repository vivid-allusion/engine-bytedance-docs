---
title: "UpdateCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateCronJob-zh-tw"
---

更新 Cron 觸發器。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多發送20個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=UpdateCronJob&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `UpdateCronJob`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |是否必選 |描述 |範例值 |
|---|---|---|---|---|
|FunctionId |String |是 |函數 ID。您可以呼叫[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-zh-tw)獲取函數 ID。 |`3gyz993****` |
|JobName |String |是 |Cron 觸發器名稱。 |`cron1` |
|CronExpression |String |是 |Cron 表示式。 |`*/1 * * **` |
|Parameter |String |否 |自訂參數。 |`cron` |
|Description |String |否 |觸發器描述。 |`test` |
|CronType |Integer |是 |Cron 觸發器的排程類型。<br><br><br>* 1：全球。<br><br>* 2：單點排程。 |`1` |


<span id="返回參數"></span>
## 返回參數

無

<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```json
POST  https://cdn.byteplusapi.com?Action=UpdateCronJob&Version=2021-03-01
{
    "FunctionId":"3gyz993****",
    "JobName":"test1",
    "CronExpression":"*/1 * * * *",
    "Parameter":"cron_al",
    "Description":"",
    "CronType":1
}
```
