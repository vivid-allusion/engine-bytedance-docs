---
title: "UpdateCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateCronJob"
---

该接口用于更新触发规则。

<span id="使用说明"></span>
## 使用说明

请求限制：每秒最多发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=UpdateCronJob&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `UpdateCronJob`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|FunctionId |String |是 |您希望停止cron的函数的ID。您可以通过调用接口[ListSparrow](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSparrow)获得FunctionId。 |`3gyz993****` |
|JobName |String |是 |任务名称。名称必须满足以下要求：<br><br><br>* 每个函数的任务名称必须是唯一的<br><br>* 长度不得超过128个字符。 |`cron1` |
|CronExpression |String |是 |执行表达式。表达式必须满足以下要求：<br><br>&nbsp;<br><br>支持cron表达式（不支持秒级触发） |`*/1 * * **` |
|Parameter |String |否 |执行参数 |`cron` |
|Description |String |否 |任务描述 |`test` |
|CronType |Integer |是 |计划类型。可能的值：<br><br>&nbsp;<br><br>1：全局计划。<br><br>&nbsp;<br><br>2：单点计划。 |`1` |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

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
