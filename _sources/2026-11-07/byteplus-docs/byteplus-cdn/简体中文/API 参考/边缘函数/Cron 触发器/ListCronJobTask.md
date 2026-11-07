---
title: "ListCronJobTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCronJobTask-cn"
---

获取指定 Cron 触发器的任务执行列表。

<span id="使用说明"></span>
## 使用说明

请求限制：每秒最多发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListCronJobTask&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `ListCronJobTask`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |
|FunctionId |String |是 |函数 ID。您可以调用[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-cn)获取函数 ID。 |
|JobName |String |是 |触发器名称。 |
|Page |Integer |否 |页码。 |
|Limit |Integer |否 |每页记录数。默认为 50 条。最多为 50 条。 |
|OrderBy |Integer |否 |该参数指定查询数据的顺序，接受以下值：<br><br><br>* 1：降序排列数据。<br><br>* 2（默认）：升序排列数据。 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Tasks |Object[] |Cron 触发器的任务执行列表。 | |
|JobName |String |Cron 触发器的名称。 |`cron1` |
|CronExpression |String |Cron 表达式。 |`*/1 * * **` |
|Parameter |String |自定义参数。 |`cron` |
|CronTaskStatus |Long |任务状态。 |`1` |
|Description |String |任务描述。 |`test` |
|Uuid |String |任务的 UUID。 |`2xju****` |
|CreateTime |Long |创建时间。 |`1638326159` |
|UpdateTime |Long |更新时间。 |`1638326159` |
|TotalCount |Long |任务执行记录的总数。 |`1` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListCronJobTask&Version=2021-03-01&FunctionId=3gyz993****&JobName=cron1&Page=1&Limit=10&OrderBy=2
```


<span id="返回示例"></span>
### 返回示例

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
