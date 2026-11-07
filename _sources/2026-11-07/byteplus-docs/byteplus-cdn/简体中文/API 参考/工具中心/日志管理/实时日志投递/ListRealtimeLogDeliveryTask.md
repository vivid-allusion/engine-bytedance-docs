---
title: "ListRealtimeLogDeliveryTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListRealtimeLogDeliveryTask_zh-cn"
---

获取实时日志投递任务的列表。您可以指定一系列过滤条件对任务列表进行过滤。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=ListRealtimeLogDeliveryTask&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `ListRealtimeLogDeliveryTask`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Desc |String |否 |指定 `Desc` 作为过滤条件，支持模糊匹配。 |`my` |
|Domain |String |否 |指定一个 Domain 作为过滤条件，获取投递该域名日志的任务。 |`www.example.com` |
|Status |String |否 |指定一个任务的状态作为过滤条件。该参数有以下取值：<br><br><br>* `enable`: 表示已启用。<br><br>* `disable`: 表示已停用。 |`enable` |
|TaskID |String |否 |指定一个任务 ID 作为过滤条件。 |`33a1f4df-f384-453e-9d59-3e9ff4b04b4e` |
|TaskType |String |否 |指定一个投递目标作为过滤条件。该参数有以下取值：<br><br><br>* `tls`：表示 BytePlus 日志服务（TLS）。<br><br>* `sls`：表示阿里云日志服务（SLS）。<br><br>* `http_server`：表示 HTTP 服务器。<br><br>* `splunk`：表示 Splunk 日志服务。<br><br>* `bigquery`：表示 BigQuery。 |`tls` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|TaskInfo |Object[] |表示符合过滤条件的任务列表。 | |
|Area |String |该参数值始终是 `outside_chinese_mainland`。 |`outside_chinese_mainland` |
|CreateTime |Long |表示任务的创建时间，格式是 Unix 时间戳。 |`1761816153` |
|Desc |String |表示任务的描述。 |`myDesc` |
|Domain |String |表示任务所关联的域名列表，也就是该任务投递的是哪些域名的日志。 |`www.example.com` |
|HttpServer |Object |当 `TaskType` 为 `http_server` 时，该结构体表示 HTTP 服务器侧的相应配置。 | |
|AuthMechanism |Boolean |表示 HTTP 服务器是否启用了鉴权。该参数有以下取值：<br><br><br>* `true`<br><br>* `false` |`true` |
|CompressType |String |表示在 CDN 投递日志时所使用的压缩算法。该参数有以下取值：<br><br><br>* `gzip`：表示 Gzip 压缩算法。<br><br><br>如果该参数值为空（""），表示不使用压缩。 |`gzip` |
|RequestHeader |Object[] |表示 CDN 在向 HTTP 服务器投递日志时，请求中包含的额外头部列表。 | |
|Key |String |表示列表中一个头部的 Key。 |`key1` |
|Value |String |表示 `Key` 的值。 |`value1` |
|SecretKey |String |表示鉴权 Key，用于计算令牌。该参数仅当 `AuthMechanism` 为 `true` 时才有效。<br><br>关于更多关于鉴权流程与令牌算法的信息，参见 [创建日志投递任务](https://docs.byteplus.com/en/docs/byteplus-cdn/log-streaming-task-config_zh-cn)。 |`xxxxxxxxxxx` |
|Url |String |表示 HTTP 服务器的访问点、端口以及日志存放的路径。 |`http://www.example.com:8080/mylog` |
|SampleRate |Double |表示日志采样率。 |`50` |
|Sls |Object |当 `TaskType` 为 `sls` 时，该结构体表示 SLS 侧的相应配置。 | |
|AccessKeyId |String |表示您阿里云账号的 AccessKey ID。 |`xxxxxxxxxxxxxxxx` |
|AccessKeySecret |String |表示您阿里云账号的 AccessKey Secret。 |`xxxxxxxxxxxxx` |
|Endpoint |String |表示 `Project` 的公网域名。 |`ap-southeast-1.log.aliyuncs.com` |
|LogStore |String |表示存储日志的 LogStore。 |`my_store` |
|Project |String |表示 `LogStore` 所属的日志项目。 |`my_project` |
|Status |String |表示该任务的状态，该参数有以下取值：<br><br><br>* `enable`：表示任务已启用。<br><br>* `disable`：表示任务已停用。 |`enable` |
|StatusDetail |Object[] |表示任务最近发生的异常列表。列表中最多记录 10 个异常。 | |
|Detail |String |表示异常的详情。 |`exception details` |
|Time |Long |表示异常发生的时间，格式为 Unix 时间戳。 |`1761815000` |
|TaskID |String |表示任务的 ID。 |`42de0332-b6e0-4fe1-9a5a-847bb7471def` |
|TaskType |String |表示投递目标，有以下取值：<br><br><br>* `tls`：表示 BytePlus 日志服务（TLS）。<br><br>* `sls`：表示阿里云日志服务（SLS）。<br><br>* `http_server`：表示 HTTP 服务器。<br><br>* `splunk`：表示 Splunk 日志服务。<br><br>* `bigquery`：表示 BigQuery。 |`tls` |
|Tls |Object |当 `TaskType` 为 `tls` 时，该结构体表示 TLS 侧的相应配置。 | |
|Endpoint |String |表示 `Project` 的公网域名。 |`tls-ap-southeast-1.volces.com` |
|ProjectID |String |表示日志主题所属的日志项目 ID。该项目在 `Endpoint` 所对应的投递地域下。 |`a9db2fef-d7f8-47a3-aa0a-c52ef7ef4747` |
|ProjectName |String |表示日志主题所属的日志项目名称。 |`test` |
|Region |String |表示日志项目所在的地域。 |`ap-southeast-1` |
|TopicID |String |表示存储日志的日志主题 ID。 |`b23298e8-c262-4cb6-8138-2c311230b972` |
|TopicName |String |表示存储日志的日志主题的名称。 |`test4` |
|Ttl |Long |表示日志的存储时长，单位是天。<br><br>如果该参数值是 `3650`，表示日志为永久保存。 |`3` |
|UpdateTime |Long |表示该任务最近的更新时间，格式是 Unix 时间戳。 |`1761816153` |
|Splunk |Object |当 `TaskType` 为 `splunk` 时，该结构体表示 Splunk 侧的相应配置。 | |
|CompressType |String |表示在 CDN 投递日志时，是否启用 Gzip 压缩。该参数有以下取值：<br><br><br>* `true`：表示启用 Gzip 压缩。<br><br>* `false`：表示不启用 Gzip 压缩。 |`true` |
|Token |String |表示 HEC 鉴权 Token。 |`B5A79AAD-D822-46CC-80D1-819F80D7BFB0` |
|Url |String |表示 HEC 接口地址。 |`https://192.168.1.100:8088/services/collector` |
|BigQuery |Object |当 `TaskType` 为 `bigquery` 时，该结构体表示 BigQuery 侧的相应配置。 | |
|Authentication |String |Google Cloud 服务账号（Service Account）的 JSON 格式密钥。该密钥包含身份认证信息，用于授权 BytePlus CDN 访问您的 BigQuery 资源并流式写入日志。 | |
|DatasetID |String |您在 BigQuery 中创建的数据集（Dataset）ID。 |`cdn_logs_dataset` |
|ProjectID |String |BigQuery 所在的 GCP 项目（Project）ID。 |`my-project` |
|TableID |String |您在 BigQuery 中创建的表（Table）ID。 |`access_logs` |
|Total |Long |表示列表中的任务数量。 |`3` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=ListRealtimeLogDeliveryTask&Version=2021-03-01
{
    "Desc": "my",
    "Domain": "www.example.com",
    "TaskType": "tls",
    "Status": "enable",
    "TaskID": "b23298e8-c262-4cb6-8138-2c311230b972"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20251030175056FC7B92C49D1494225A51",
        "Action": "ListRealtimeLogDeliveryTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskInfo": [
            {
                "Area": "outside_chinese_mainland",
                "CreateTime": 1761816153,
                "Desc": "myDesc",
                "Domain": "www.example.com",
                "HttpServer": null,
                "SampleRate": 100,
                "Sls": null,
                "Status": "enable",
                "StatusDetail": [],
                "TaskID": "b23298e8-c262-4cb6-8138-2c311230b972",
                "TaskType": "tls",
                "Tls": {
                    "Endpoint": "tls-ap-southeast-1.volces.com",
                    "ProjectID": "a9db2fef-d7f8-47a3-aa0a-c52ef7ef4747",
                    "ProjectName": "test",
                    "Region": "ap-southeast-1",
                    "TopicID": "b23298e8-c262-4cb6-8138-2c311230b972",
                    "TopicName": "test4",
                    "Ttl": 7
                },
                "UpdateTime": 1761816153
            }
        ],
        "Total": 1
    }
}
```


&nbsp;
