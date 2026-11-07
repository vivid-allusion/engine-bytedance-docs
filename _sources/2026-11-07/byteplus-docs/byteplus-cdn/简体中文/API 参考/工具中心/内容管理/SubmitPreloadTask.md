---
title: "SubmitPreloadTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/submitpreloadtask"
---

在 BytePlus CDN 中提交一个预热任务，将一个或者多个文件提前缓存到 CDN 的缓存节点。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

默认情况下，每个 BytePlus 主账号的任务额度如下：


* 每天最多预热 1,000 个 URL。

* 每个任务最多预热 100 个 URL。


<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=SubmitPreloadTask&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `SubmitPreloadTask`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|UrlList |String[] |否 |表示一个或多个文件 URL。CDN 将这些文件提前缓存到缓存节点。<br><br>说明<br><br>URL 中不能包含泛域名。如果您需要为一个泛域名下的多个子域名提交一个预热任务，您必须对每个子域名指定需要预热的那些 URL。 |`["https://www.example.com/1.jpg","https://www.example.com/2.jpg"]` |
|Area |String |否 |表示一个加速区域。CDN 将 `Urls` 中的每个文件提前缓存到该区域下的那些缓存节点。该参数有以下取值：<br><br><br>* `chinese_mainland`：表示中国内地。<br><br>* `outside_chinese_mainland`：表示全球，但不包含中国内地。<br><br>* `global`：表示全球。<br><br><br>如果不指定该参数，对于 `Urls` 中一个 URL，这个加速区域就是该 URL 所含域名的加速区域。 |`outside_chinese_mainland` |
|ConcurrentLimit |Long |否 |表示 CDN 在执行预热任务时，每次向源站请求的最大文件数量。默认值是 `10`，该参数的取值范围是 1\-1000。 |`20` |
|Urls |String |否 |**不建议**使用该参数，请使用 `UrlList` 代替。<br><br>该参数的作用与 `UrlList` 相同。在 `Urls` 中指定多个 URL 时，URL 之间必须以 `\n` 分隔。<br><br>如果您同时指定了 `UrlList` 和 `Urls`，仅 `UrlList` 生效。 |`https://www.example.com/1.jpg\nhttps://www.example.com/2.jpg` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|TaskID |String |表示该任务的 ID。您可以调用 [DescribeContentTasks](https://docs.byteplus.com/en/docs/byteplus-cdn/describecontenttasks) 查看 `Urls` 中每个 URL 的预热结果。 |`prefetch_url_89c25a1aa3044b39921387190fc9b0e438f3d071f278f031` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=SubmitPreloadTask&Version=2021-03-01
{
    "UrlList": [
        "https://www.example.com/1.jpg",
        "https://www.example.com/2.jpg"
    ]
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202406300908245F2C63BC765D774F1CB0",
        "Action": "SubmitPreloadTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskID": "prefetch_url_3ed013a15c0f47258ed8feff3700f7396222fb893dade871"
    }
}
```


&nbsp;
