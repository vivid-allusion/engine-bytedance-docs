---
title: "CreateCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateCronJob-cn"
---

创建 Cron 触发器。

<span id="使用限制"></span>
## 使用限制

请求限流：每秒最多可发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=CreateCronJob&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |API 名称。当前 API 的名称为 `CreateCronJob`。 |
|Version |String |是 |API 版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|FunctionId |String |是 |函数 ID。您可以调用[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-cn)获取函数 ID。 |`3gyz993****` |
|JobName |String |是 |Cron 触发器名称。名称必须符合以下要求：<br><br><br>* 每个函数中的 Cron 触发器名称必须唯一。<br><br>* 名称长度不能超过128个字符。 |`cron1` |
|CronExpression |String |是 |Cron 表达式。参见 [支持的 Cron 表达式](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-cron-triggers-cn#%E6%94%AF%E6%8C%81%E7%9A%84-cron-%E8%A1%A8%E8%BE%BE%E5%BC%8)。 |`*/1 * * **` |
|Parameter |String |否 |自定义参数。在函数执行时，边缘函数把该参数传递给函数代码中的 CronEvent 对象。 |`cron` |
|Description |String |否 |Cron 触发器描述。 |`test` |
|CronType |Integer |是 |Cron 触发器调度类型：<br><br>&nbsp;<br><br>1：全球：在全部边缘节点执行。<br><br>&nbsp;<br><br>2：单点调度：随机在任意一个边缘节点执行。 |`1` |


<span id="返回参数"></span>
## 返回参数

无

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

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
