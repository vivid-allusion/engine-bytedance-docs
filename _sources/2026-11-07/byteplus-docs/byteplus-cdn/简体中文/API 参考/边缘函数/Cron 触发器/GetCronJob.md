---
title: "GetCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetCronJob-cn"
---

获取 Cron 触发器的详细信息。

<span id="使用说明"></span>
## 使用说明

请求限制：每秒最多发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetCronJob&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `GetCronJob`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |
|FunctionId |String |是 |函数 ID。您可以调用[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-cn)获取函数 ID。 |
|JobName |String |是 |触发器名称。 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Job |Object[] |Cron 触发器列表。 |`Task details` |
|JobName |String |触发器名称。 |`cron2` |
|CronExpression |String |Cron 表达式。 |`*/1 * * **` |
|Parameter |String |自定义参数。 |`cron` |
|Description |String |Cron 触发器的描述。 |`test` |
|JobState |Long |Cron 触发器的状态。<br><br><br>* 1：待调度<br><br>* 3：已停用<br><br>* 4：取消调度 |`1` |
|CronType |Integer |Cron 触发器的调度类型。<br><br><br>* 1：全球。<br><br>* 2：单点调度。 |`1` |
|CreateTime |Long |创建时间。 |`1638326159` |
|UpdateTime |Long |更新时间。 |`1638326159` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```HTTP
GET https://cdn.byteplusapi.com?Action=GetCronJob&Version=2021-03-01&FunctionId=3gyz993****&JobName=cron2
```


<span id="返回示例"></span>
### 返回示例

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
