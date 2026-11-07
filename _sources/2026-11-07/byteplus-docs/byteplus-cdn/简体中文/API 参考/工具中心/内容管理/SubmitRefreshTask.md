---
title: "SubmitRefreshTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/submitrefreshtask"
---

在 BytePlus CDN 中提交一个刷新任务。如果在任务中指定文件 URL，CDN 会执行任务时会删除这些文件。如果在任务中指定目录，CDN 默认会标记这些目录中的文件为过期。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以发送 20 个请求。

默认情况下，每个 BytePlus 主账号的刷新额度如下：


* 每天最多刷新 10,000 个 URL。

* 每天最多刷新 50 个目录。

* 每个任务可以包含最多 100 个 URL 或 50 个目录。


<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=SubmitRefreshTask&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `SubmitRefreshTask`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Type |String |否 |表示一个刷新类型。该参数有以下取值：<br><br><br>* `file`：表示 URL 刷新，对一个或者多个文件执行刷新操作。<br><br>* `dir`：表示目录刷新，对一个或者多个目录下的所有文件，包括子目录下的文件执行刷新操作。<br><br>* `regex`：表示正则刷新。指定一个或多个正则表达式，对与正则表达式匹配的文件 URL 执行刷新操作。要使用正则刷新，请 [提交工单](https://console.byteplus.com/workorder/create)。关于正则刷新的介绍和 URL 规范，参见 [正则刷新](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-purge-cn#%E6%AD%A3%E5%88%99%E5%88%B7%E6%96%B0)。<br><br><br>该参数的默认值为 `file`。 |`file` |
|Prefix |Boolean |否 |表示是否使用前缀刷新。该参数仅当 `Type` 是 `dir` 时有效，有以下取值：<br><br><br>* `true`：表示使用前缀刷新，对以指定前缀开头的目录下的所有文件执行刷新操作。<br><br>* `false`：表示不使用前缀刷新。<br><br><br>该参数的默认值是 `false`。 |`true` |
|UrlList |String[] |否 |表示一个待刷新的 URL 列表。每个 URL 必须以 `http://` 或 `https://` 开头。<br><br><br>* 当 `Type` 是 `file` 时，您指定的是文件 URL。<br><br>* 当 `Type` 是 `dir` 时，<br><br>   * 如果 `Prefix` 是 `false`，您指定的是以 `/` 结尾的目录，例如 `http://www.example.com/image/`。<br><br>   * 如果 `Prefix` 是 `true`，您指定的是目录前缀。例如 `http://www.example.com/im` 可以匹配 `http://www.example.com/image/` 与 `http://www.example.com/ime/` 这两个目录。<br><br>* 当 `Type` 是 `regex` 时，您指定的是用来匹配文件 URL 的正则表达式。参见 [正则刷新](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-purge-cn#%E6%AD%A3%E5%88%99%E5%88%B7%E6%96%B0)。要使用该参数值，请 [提交工单](https://console.byteplus.com/workorder/create)。<br><br><br>说明<br><br>您不能直接对泛域名下的文件和目录执行刷新操作，而是要对每个子域名进行这些操作。 |`["https://www.example.com/1.jpg","https://www.example.com/2.jpg"]` |
|Delete |Boolean |否 |对于目录刷新，该参数表示是否从缓存中删除 `Urls`或 `UrlList` 指定的文件。该参数仅当 `Type` 是 `dir` 时有效。要使用该参数，请 [提交工单](https://console.byteplus.com/workorder/create)。<br><br>该参数有以下取值：<br><br><br>* `true`：表示删除这些文件。之后，如果收到了这些文件的请求，CDN 会向源站请求这些文件。<br><br>* `false`：表示不删除这些文件，仅标记这些文件为已过期。之后，如果收到了这些文件的请求，CDN 会执行 [回源校验](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-caching-rules-cn#%E5%9B%9E%E6%BA%90%E6%A0%A1%E9%AA%8C)。<br><br><br>该参数的默认值是 `false`。 |`false` |
|Urls |String |否 |**不建议**使用该参数，请使用 `UrlList` 代替。<br><br>该参数的作用与 `UrlList` 相同。在 `Urls` 中指定多个 URL 时，URL 之间必须以 `\n` 分隔。<br><br>如果您同时指定了 `UrlList` 和 `Urls`，仅 `UrlList` 生效。 |`https://www.example.com/1.jpg\nhttps://www.example.com/2.jpg` |
|RequestHeaderInstances |Object[] |否 |指定待刷新文件在缓存键中必须包含的请求头。只有当缓存文件的缓存键中完全包含了此处指定的请求头时，该文件才会被匹配并刷新。<br><br>列表中最多包含 10 个请求头。 | |
|Key |String |否 |表示列表中一个请求头的名称。名称有以下要求：<br><br><br>* 名称不能是 `User-Agent`。<br><br>* 名称不能以 `x-bdcdn-` 或者 `Volc-Cdn` 开头。<br><br>* 名称不能超过 1,024 个字符。 |`header1` |
|Value |String |否 |表示该请求头的值，长度不能超过 1,024 个字符。 |`value1` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|TaskID |String |表示该任务的 ID。您可以调用 [DescribeContentTasks](https://docs.byteplus.com/en/docs/byteplus-cdn/describecontenttasks) 查看 `Urls` 列表中每个对象的刷新结果。 |`refresh_url_bbd36e1cb5154f52b648b07ee119223e2971399f5a1075c0` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=SubmitRefreshTask&Version=2021-03-01
{
    "Type": "file",
    "UrlList": [
        "https://www.example.com/1.txt",
        "https://www.example.com/2.txt"
    ],
    "RequestHeaderInstances": [
        {
            "Key": "header1",
            "Value": "value1"
        },
        {
            "Key": "header2",
            "Value": "value2"
        }
    ]
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202201141648440102100180260E003ABA",
        "Action": "SubmitRefreshTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskID": "refresh_url_bbd36e1cb5154f52b648b07ee119223e2971399f5a1075c0"
    }
}
```
