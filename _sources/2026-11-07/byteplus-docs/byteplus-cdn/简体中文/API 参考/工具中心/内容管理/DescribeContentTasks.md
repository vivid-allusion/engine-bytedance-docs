---
title: "DescribeContentTasks"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/describecontenttasks"
---

获取过去 7 天内提交的刷新或预热任务，细分到这些任务中的每个 URL。返回结果展示了每个任务的详情，包括任务的执行结果。您可以使用多个过滤选项对任务列表进行过滤。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeContentTasks&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeContentTasks`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|UrlList |String[] |否 |表示一个 URL 列表，用于对查询结果进行过滤，以获取列表中每个任务详情。每个 URL 都必须以 `http://` 或 `https://` 开头。<br><br>该参数是一个字符串数组。<br><br>如果您同时指定了 `Url`，则 `Url` 不生效。 |`["https://www.example.com/1.jpg","https://www.example.com/2.jpg"]` |
|DomainName |String |否 |表示一个域名，用于对查询结果进行过滤，以获取 URL 中包含该域名的任务。 |`www.example.com` |
|TaskID |String |否 |表示一个任务 ID，用以获取该 ID 的所有任务。 |`prefetch_url_89c25a1aa3044b39921387190fc9b0e438f3d071f278f031` |
|TaskType |String |是 |表示一个任务类型，用于对查询结果进行过滤，以获取该类型任务。该参数的可用值如下：<br><br><br>* `refresh_file`：表示 URL 刷新任务。<br><br>* `refresh_dir`：表示目录刷新任务。<br><br>* `preload`：表示 URL 预热任务。<br><br>* `refresh_regex`：表示正则刷新任务。 |`preload` |
|Status |String |否 |表示一个任务状态，用于对查询结果进行过滤，以获取该状态下任务。该参数的可用值如下：<br><br><br>* `complete`：表示已完成的任务。<br><br>* `running`：表示执行中的任务。<br><br>* `failed`：表示执行失败的任务。<br><br><br>如果不指定该参数，则表示不使用该参数对任务列表进行过滤。 |`complete` |
|StartTime |Long |否 |表示一个开始时间，格式是 Unix 时间戳，以获取提交时间晚于或等于该时间的任务。需要留意的是，您无法查询 7 天前提交的任务。<br><br>您必须同时指定 `StartTime` 和 `EndTime`，或者两个参数都不指定。如果两个参数都不指定，则获取过去 7 天内提交的任务。 |`1641844915` |
|EndTime |Long |否 |表示一个结束时间，格式是 Unix 时间戳，以获取提交时间早于或等于该时间的任务。 |`1641845373` |
|PageNum |Long |否 |表示一个页码，用以获取该页面上的任务。该参数的默认值为 `1`。<br><br>CDN 对符合过滤条件的任务进行分页。您可以根据响应正文中的 `Total` 和 `PageSize` 参数的值计算页数。 |`1` |
|PageSize |Long |否 |表示每页包含的任务数量。该参数的取值范围是 1\-1000，默认值是 `50`。 |`10` |
|Url |String |否 |**不建议**使用该参数，请使用 `UrlList` 代替。<br><br>该参数的作用与 `UrlList` 相同。在 `Urls` 中指定多个 URL 时，URL 之间必须以 `\n` 分隔。<br><br>如果您同时指定了 `UrlList` 和 `Urls`，仅 `UrlList` 生效。 |`https://www.example.com/1.jpg\nhttps://www.example.com/2.jpg` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Total |Long |表示符合过滤条件的任务总数。 |`2` |
|PageNum |Long |表示请求正文中的 `PageNum`。 |`1` |
|PageSize |Long |表示请求正文中的 `PageSize`。 |`100` |
|Data |Object[] |表示 `PageNum` 上的任务列表。如果 `PageNum` 所表示页码不存在或者该页上没有任务，该参数值为 `null`。 | |
|Url |String |表示列表中一个任务所操作的 URL。 |`https://www.example.com/1.jpg` |
|Status |String |表示该任务的状态。该参数有以下取值：<br><br><br>* `complete`：表示任务已完成。<br><br>* `running`：表示任务正在执行中。<br><br>* `failed`：表示任务执行失败。 |`complete` |
|TaskType |String |表示该任务的类型。该参数有以下取值：<br><br><br>* `refresh_file`：表示 URL 刷新任务。<br><br>* `refresh_dir`：表示目录刷新任务。<br><br>* `preload`：表示 URL 预热任务。<br><br>* `refresh_regex`：表示正则刷新任务。 |`preload` |
|RefreshPrefix |Boolean |表示该任务中是否有 "前缀刷新" 这个配置。仅当 `TaskType` 是 `refresh_dir` 时，该参数有效。该参数有以下取值：<br><br><br>* `true`：表示该任务中有这个配置。<br><br>* `false`：表示该任务中没有这个配置。<br><br><br>如果 `TaskType` 不是 `refresh_dir`，该参数值始终是 `false`。 |`true` |
|CreateTime |Long |表示该任务的提交时间，格式是 Unix 时间戳。 |`1601371409` |
|TaskID |String |表示该任务的 ID。 |`prefetch_url_89c25a1aa3044b39921387190fc9b0e438f3d071f278f031` |
|Process |String |表示该任务的进度，以百分比表示。 |`70%` |
|Delete |Boolean |表示该任务是否指定了删除缓存中的文件。该参数仅当 `TaskType` 是 `refresh_dir` 时有效。该参数有以下取值：<br><br><br>* `true`：表示删除缓存中的文件。<br><br>* `false`：表示不删除缓存中的文件，仅标记这些文件为过期。<br><br><br>当 `TaskType` 不是 `refresh_dir` 时，`Delete` 的值始终是 `false`。 |`false` |
|Remark |String |* 如果 `Status` 是 `failed` 并且 CDN 可以定位到问题，该参数记录了任务失败的原因。<br><br>* 在其他情况下，该参数值为空（""）。 |`origin_error` |
|StatusCode |Long |* 如果 `Remark` 不是空（"")，该参数值表示源站的响应状态码。状态码为 4xx 或者 5xx。<br><br>* 如果 `Remark` 是空（"")，该参数不会出现。 | |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeContentTasks&Version=2021-03-01
{
    "StartTime": 1625587200,
    "EndTime": 1625673600,
    "TaskType": "preload",
    "PageSize": 10,
    "PageNum": 1
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202406301133492C6A5B1ABB315058A120",
        "Action": "DescribeContentTasks",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": [
            {
                "CreateTime": 1719738505,
                "Process": "100%",
                "Remark": "origin_error",
                "Status": "failed",
                "TaskID": "prefetch_url_3ed013a15c0f47258ed8feff3700f7396222fb893dade871",
                "TaskType": "preload",
                "Url": "https://www.example.com/2.txt"
            },
            {
                "CreateTime": 1719738505,
                "Process": "100%",
                "Remark": "",
                "Status": "complete",
                "TaskID": "prefetch_url_3ed013a15c0f47258ed8feff3700f7396222fb893dade871",
                "TaskType": "preload",
                "Url": "https://www.example.com/1.txt"
            }
        ],
        "PageNum": 1,
        "PageSize": 50,
        "Total": 2
    }
}
```


&nbsp;
