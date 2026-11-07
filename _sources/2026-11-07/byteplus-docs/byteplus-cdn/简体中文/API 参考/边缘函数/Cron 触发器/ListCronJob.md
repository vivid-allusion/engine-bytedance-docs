---
title: "ListCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCronJob-cn"
---

获取 Cron 触发器列表。

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
|FunctionId |String |是 |函数 ID。您可以调用[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-cn)获取函数 ID。 |
|Page |Integer |否 |页码 |
|Limit |Integer |否 |每页记录数。默认为 50 条。最多为 50 条。 |
|OrderBy |Integer |否 |该参数指定数据查询的顺序。它接受以下值：<br><br><br>* 1：降序排列数据。<br><br>* 2（默认）：升序排列数据。 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Jobs |Object[] |触发器列表。 | |
|JobName |String |Cron 触发器名称。 |`cron1` |
|CronExpression |String |Cron 表达式。 |`*/1 * * **` |
|Parameter |String |自定义参数。 |`cron` |
|Description |String |触发器描述。 |`test` |
|JobState |Long |触发器状态。<br><br><br>* 1：待调度<br><br>* 3：已停用<br><br>* 4：取消调度 |`1` |
|CronType |Integer |Cron 触发器调度类型。可能的值有：<br><br>&nbsp;<br><br>1：全球：在全部边缘节点执行。<br><br>&nbsp;<br><br>2：单点调度：随机在任意一个边缘节点执行。 |`1` |
|CreateTime |Long |创建时间 |`1638326159` |
|UpdateTime |Long |更新时间 |`1638326159` |
|TotalCount |Long |触发器总数。 |`1` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```HTTP
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
