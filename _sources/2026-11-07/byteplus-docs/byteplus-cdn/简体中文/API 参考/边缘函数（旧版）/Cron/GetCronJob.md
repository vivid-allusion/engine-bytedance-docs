---
title: "GetCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/GetCronJob"
---

该接口用于获取触发规则的详细信息。

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
|FunctionId |String |是 |您想查看调度日志列表的功能的ID。您可以通过调用接口[ListSparrow](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSparrow)<br><br>&nbsp;<br><br>获取FunctionId。 |
|JobName |String |是 |任务名称。名称必须满足以下要求：<br><br><br>* 每个函数的任务名称必须唯一。<br><br>* 长度不能超过128个字符。 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Job |Object[] |见下文 |`Task details` |
|JobName |String |任务名称。名称必须满足以下要求：<br><br><br>* 每个函数的任务名称必须唯一。<br><br>* 长度不能超过128个字符 |`cron2` |
|CronExpression |String |执行表达式。表达式必须满足以下要求：<br><br>&nbsp;<br><br>支持cron表达式（不支持秒级触发） |`*/1 * * **` |
|Parameter |String |执行参数 |`cron` |
|Description |String |任务描述 |`test` |
|JobState |Long |任务状态。<br><br><br>* 1：已调度<br><br>* 3：已禁用<br><br>* 4：未调度 |`1` |
|CronType |Integer |调度类型。<br><br><br>* 1：全局调度。<br><br>* 2：单点调度。 |`1` |
|CreateTime |Long |创建时间 |`1638326159` |
|UpdateTime |Long |更新时间 |`1638326159` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
GET  https://cdn.byteplusapi.com?Action=GetCronJob&Version=2021-03-01&FunctionId=3gyz993****&JobName=cron2
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
        "job": {
            "job_name": "cron2",
            "cron_expression": "*/59 * * * *",
            "parameter": "cron_all",
            "description": "",
            "job_state": 0,
            "cron_type": 2,
            "operator": "****",
            "create_time": 1638871686,
            "update_time": 1638871686
        }
    }
}
```


&nbsp;
