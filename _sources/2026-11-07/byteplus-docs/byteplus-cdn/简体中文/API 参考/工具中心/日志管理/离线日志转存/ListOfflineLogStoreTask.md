---
title: "ListOfflineLogStoreTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListOfflineLogStoreTask_zh-cn"
---

获取离线日志转存任务的列表。您可以指定一系列过滤条件对任务列表进行过滤。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=ListOfflineLogStoreTask&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `ListOfflineLogStoreTask`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Bucket |String |否 |指定存储桶下存放日志文件的路径作为过滤条件，格式为 `<存储桶名称>/<日志文件路径>`。 |`mybucket/storage/logs` |
|Desc |String |否 |指定 `Desc` 作为过滤条件，支持模糊匹配。 |`myDesc` |
|Domain |String |否 |指定一个 Domain 作为过滤条件，获取转存该域名日志的任务，也就是关联了该任务的域名。 |`www.example.com` |
|Region |String |否 |指定存储桶所在的地域代码（region code）作为过滤条件。地域代码的长度不能超过 64 个字符。<br><br><br>* 如果 `TaskType` 为 `s3`，请咨询该存储桶的对象存储服务提供商以获取您可以指定的地域代码。<br><br>* 如果 `TaskType` 为 `tos`，您可以指定以下地域代码：<br><br>   * `cn-hongkong`：表示中国香港。<br><br>   * `ap-southeast-1`：表示亚太东南（柔佛）。<br><br>   * `ap-southeast-3`：表示亚太东南（雅加达）。 |`ap-southeast-1` |
|Status |String |否 |指定一个任务的状态作为过滤条件。该参数有以下取值：<br><br><br>* `enable`: 表示已启用。<br><br>* `disable`: 表示已停用。 |`enable` |
|TaskID |String |否 |指定一个任务 ID 作为过滤条件。 |`nj2S29or5KaAeEiwcGWA5S` |
|TaskType |String |否 |指定一个转存目标作为过滤条件。该参数有以下取值：<br><br><br>* `tos`：表示 BytePlus 对象存储（TOS）。<br><br>* `s3`：表示 AWS S3 或者使用兼容 S3 鉴权方式的对象存储服务。 |`s3` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|TaskInfo |Object[] |表示符合过滤条件的任务列表。 | |
|AuthInformation |Object |表示转存目标的访问凭证。 | |
|AccessKeyID |String |表示凭证中的 AccessKey ID。 |`xxxxxxxxxxxxxxxxx` |
|AccessKeySecret |String |表示凭证中的 AccessKey Secret。 |`xxxxxxxxx` |
|Bucket |String |表示存储桶下存放日志文件的路径。 |`mybucket/log` |
|CreateTime |Long |表示任务的创建时间，格式是 Unix 时间戳。 |`1761908274` |
|Desc |String |表示任务的描述。 |`myDesc` |
|Domain |String |表示关联了该任务的域名。 |`www.example.net` |
|Endpoint |String |表示对象存储服务的公网访问点。 |`tos-ap-southeast-1.volces.com` |
|PrivateBucketAccess |Boolean |表示该存储桶是否是私有的。 |`true` |
|Region |String |表示存储桶所在的地域代码（region code）。 |`us-east-1` |
|Status |String |表示该任务的状态，该参数有以下取值：<br><br><br>* `enable`：表示任务已启用。<br><br>* `disable`：表示任务已停用。 |`enable` |
|StatusDetail |Object[] |表示任务最近发生的异常列表。列表中最多记录 10 个异常。 | |
|Detail |String |表示异常的详情。 |`exception details` |
|Time |Long |表示异常发生的时间，格式为 Unix 时间戳。 |`1761815000` |
|TaskID |String |表示任务的 ID。 |`dPFEQ8vwbRShTdW5kNbZe3` |
|TaskType |String |表示日志转存目标，有以下取值：<br><br><br>* `tos`：表示 BytePlus 对象存储（TOS）。<br><br>* `s3`：表示 AWS S3 或者使用兼容 S3 鉴权方式的对象存储服务。 |`s3` |
|UpdateTime |Long |表示该任务最近的更新时间，格式是 Unix 时间戳。 |`1761908274` |
|Total |Long |表示列表中的任务数量。 |`1` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=ListOfflineLogStoreTask&Version=2021-03-01
{
    "Bucket": "mybucket/log",
    "Desc": "myDesc",
    "Domain": "www.example.net",
    "Region": "us-east-1",
    "Status": "enable",
    "TaskID": "dPFEQ8vwbRShTdW5kNbZe3",
    "TaskType": "s3"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20251103163008001C7913418610FF31AA",
        "Action": "ListOfflineLogStoreTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskInfo": [
            {
                "AuthInformation": {
                    "AccessKeyID": "xxxxxxxxxxxxxxx",
                    "AccessKeySecret": "xxxxxxxx"
                },
                "Bucket": "mybucket/log",
                "CreateTime": 1761908274,
                "Desc": "myDesc",
                "Domain": "www.example.net",
                "Endpoint": "https://mybucket.s3-website-us-east-1.amazonaws.com",
                "PrivateBucketAccess": true,
                "Region": "us-east-1",
                "Status": "enable",
                "StatusDetail": [],
                "TaskID": "dPFEQ8vwbRShTdW5kNbZe3",
                "TaskType": "s3",
                "UpdateTime": 1761908274
            }
        ],
        "Total": 1
    }
}
```


&nbsp;
