---
title: "CreateCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateCronJob-zh-tw"
---

建立 Cron 觸發器。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多可傳送 20 個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=CreateCronJob&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `CreateCronJob`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |是否必選 |描述 |範例值 |
|---|---|---|---|---|
|FunctionId |String |是 |函數 ID。您可以呼叫[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-zh-tw)取得函數 ID。 |`3gyz993****` |
|JobName |String |是 |Cron 觸發器名稱。名稱必須符合以下要求：<br><br><br>* 每個函數中的 Cron 觸發器名稱必須唯一。<br><br>* 名稱長度不能超過128個字元。 |`cron1` |
|CronExpression |String |是 |Cron 表示式。參見 [支援的 Cron 表示式](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-cron-triggers-cn-zh-tw#%E6%94%AF%E6%8F%B4%E7%9A%84-cron-%E8%A1%A8%E9%81%94%E5%BC%8F)。 |`*/1 * * **` |
|Parameter |String |否 |自訂參數。在函數執行時，邊緣函數把該參數傳遞給函數程式碼中的 CronEvent 物件。 |`cron` |
|Description |String |否 |Cron 觸發器描述。 |`test` |
|CronType |Integer |是 |Cron 觸發器排程類型：<br><br>&nbsp;<br><br>1：全球：在全部邊緣伺服器執行。<br><br>&nbsp;<br><br>2：單點排程：隨機在任意一個邊緣伺服器執行。 |`1` |


<span id="返回參數"></span>
## 返回參數

無

<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```json
POST  https://cdn.byteplusapi.com?Action=CreateCronJob&Version=2021-03-01
{
    "FunctionId":"3gyz993****",
    "JobName":"test1111",
    "CronExpression":"5 4 * * *",
    "Parameter":"fetch_1",
    "Description":"",
    "CronType":2
}
```
