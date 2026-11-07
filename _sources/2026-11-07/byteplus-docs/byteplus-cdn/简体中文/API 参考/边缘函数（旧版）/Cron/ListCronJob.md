---
title: "ListCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListCronJob"
---

该接口用于根据函数域名获取触发规则列表。

<span id="使用说明"></span>
## 使用说明

请求限制：每秒最多发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListCronJob&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `ListCronJob`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |
|FunctionId |String |是 |您希望查看调度日志列表的函数ID。您可以通过调用接口[ListSparrow](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSparrow)<br><br>&nbsp;<br><br>&nbsp;<br><br>来获取FunctionId。 |
|Page |Integer |否 |页码 |
|Limit |Integer |否 |每页记录数。<br><br>&nbsp;<br><br>&nbsp;<br><br>目前，一次最多可获取50条记录。 |
|OrderBy |Integer |否 |该参数指定数据查询的顺序。它接受以下值：<br><br><br>* 1：降序排列数据。<br><br>* 2（默认）：升序排列数据。 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Jobs |Object[] |作业列表 |`See description below` |
|JobName |String |任务名称。名称必须满足以下要求：<br><br><br>* 每个函数的任务名称必须是唯一的。<br><br>* 长度不能超过128个字符 |`cron1` |
|CronExpression |String |执行表达式。表达式必须满足以下要求：<br><br>&nbsp;<br><br>支持cron表达式（不支持秒级触发） |`*/1 * * **` |
|Parameter |String |执行参数 |`cron` |
|Description |String |任务描述 |`test` |
|JobState |Long |任务状态。<br><br><br>* 1：计划中<br><br>* 3：已禁用<br><br>* 4：未计划 |`1` |
|CronType |Integer |计划类型。<br><br><br>* 1：全局计划。<br><br>* 2：单点计划。 |`1` |
|CreateTime |Long |创建时间 |`1638326159` |
|UpdateTime |Long |更新时间 |`1638326159` |
|TotalCount |Long |作业总数 |`1` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
GET  https://cdn.byteplusapi.com?Action=ListCronJob&Version=2021-03-01&FunctionId=3gyz993****&Page=1&Limit=10&OrderBy=2
```


<span id="返回示例"></span>
### 返回示例

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
