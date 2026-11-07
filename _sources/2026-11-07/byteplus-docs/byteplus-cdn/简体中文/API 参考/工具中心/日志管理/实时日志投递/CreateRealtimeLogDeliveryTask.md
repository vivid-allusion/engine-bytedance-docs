---
title: "CreateRealtimeLogDeliveryTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CreateRealtimeLogDeliveryTask_zh-cn"
---

在 CDN 中创建一个实时日志投递任务。主账号下最多可以存在 20 个任务。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=CreateRealtimeLogDeliveryTask&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `CreateRealtimeLogDeliveryTask`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Area |String |是 |表示从哪个服务区域内的 CDN 节点上采集日志。当前，该参数值只能是 `outside_chinese_mainland`，表示全球（不含中国内地）。 |`outside_chinese_mainland` |
|Domain |String |是 |表示投递哪些域名的实时日志，也就是该任务将要关联的域名。<br><br><br>* 如果您要关联账号下的所有域名，请传入`*`。这里，所有域名涵盖您后续在 CDN 中添加的域名。<br><br>* 如果您要关联指定的域名，请传入待关联的域名列表，列表中最多可以包含 200 个域名，多个域名之间以逗号（,）分隔。<br><br><br>注意<br><br>如果您已创建了关联账号下所有域名的任务，则无法再创建关联指定域名的任务。反之亦然。<br><br>您可以调用 [ListRealtimeLogDeliveryTask](https://docs.byteplus.com/en/docs/byteplus-cdn/ListRealtimeLogDeliveryTask_zh-cn) 并指定指定该域名作为过滤条件，以查看该域名是否已与某个任务关联。 |`www.example.com,img.example.com` |
|TaskType |String |是 |表示投递目标，有以下取值：<br><br><br>* `tls`：表示 BytePlus 日志服务（TLS）。<br><br>* `sls`：表示阿里云日志服务（SLS）。<br><br>* `http_server`：表示 HTTP 服务器。<br><br>* `splunk`：表示 Splunk 日志服务。<br><br>* `bigquery`：表示 GCP BigQuery。 |`sls` |
|Desc |String |否 |表示任务的描述。该参数的输入要求如下：<br><br><br>* 长度为 3 \- 64 个字符，可以包含中文、字母、数字、下划线（_）和连字符（\-）。中文占 3 个字符。<br><br>* 不能以连字符（\-）或下划线（_）开头或结尾。 |`my desc` |
|HttpServer |Object |否 |当 `TaskType` 为 `http_server` 时，该结构体表示 HTTP 服务器侧的相应配置。 | |
|AuthMechanism |Boolean |否 |表示 HTTP 服务器是否启用了鉴权。该参数有以下取值：<br><br><br>* `true`<br><br>* `false` |`true` |
|CompressType |String |否 |表示在 CDN 投递日志时所使用的压缩算法。该参数有以下取值：<br><br><br>* `gzip`：表示 Gzip 压缩算法。<br><br><br>如果该参数不指定，表示不使用压缩。 |`gzip` |
|RequestHeader |Object[] |否 |表示 CDN 在向 HTTP 服务器投递日志时，请求中需要额外包含的头部列表。列表中最多可以包含 10 个头部。<br><br>如果该参数不指定，表示请求中不添加额外的头部。 | |
|Key |String |否 |表示列表中一个头部的 Key，长度不能超过 1,024 个字符。`Key` 不能是 `User-Agent`，也不能以 `x-bdcdn-` 开头 |`mykey` |
|Value |String |否 |表示 `Key` 的值，长度不能超过 1,024 个字符。 |`myvalue` |
|SecretKey |String |否 |表示鉴权 Key，用于计算令牌。该参数的长度为 6\-40 个字符。<br><br>如果 `AuthMechanism` 为 `true`，`SecretKey` 必须指定。<br><br>关于更多关于鉴权流程与令牌算法的信息，参见 [创建日志投递任务](https://docs.byteplus.com/en/docs/byteplus-cdn/log-streaming-task-config_zh-cn)。 |`xxxxxxxxxx` |
|Url |String |否 |表示 HTTP 服务器的访问点、端口以及日志存放的路径。端口是可选的。访问点必须以 `http://` 或者 `https://` 开头，长度不能超过 1,024 个字符。 |`https://www.example.com:8080/cdn-logs` |
|SampleRate |Double |否 |表示日志采样率，范围为 0.00 \- 100.00，精确到 2 位小数。<br><br>采样率指的是投递的日志比例。例如，您设置采样率为 10，则意味着在 CDN 节点上每采集 100 条日志，CDN 会随机选择 10 条日志投递到您指定的位置。 |`50.55` |
|Sls |Object |否 |当 `TaskType` 为 `sls` 时，该结构体表示 SLS 侧的相应配置。 | |
|AccessKeyId |String |否 |表示您阿里云账号的 AccessKey ID，长度不能超过 128 个字符。 |`xxxxxxxxxxxx` |
|AccessKeySecret |String |否 |表示您阿里云账号的 AccessKey Secret，长度不能超过 128 个字符。 |`xxxxxxxxx` |
|Endpoint |String |否 |表示 `Project` 的公网域名。 |`ap-southeast-1.log.aliyuncs.com` |
|LogStore |String |否 |表示存储日志的 LogStore。 |`myStore` |
|Project |String |否 |表示 `LogStore` 所属的日志项目。 |`myProject` |
|Tls |Object |否 |当 `TaskType` 为 `tls` 时，该结构体表示 TLS 侧的相应配置。 | |
|Endpoint |String |否 |表示 `Project` 的公网域名。该参数有以下取值，与 `Region` 的取值对应。<br><br><br>* `tls-cn-hongkong.volces.com`<br><br>* `tls-ap-southeast-1.volces.com`<br><br>* `tls-ap-southeast-3.volces.com` |`tls-ap-southeast-1.volces.com` |
|ProjectID |String |否 |表示日志主题所属的日志项目 ID。 |`a9db2fef-d7f8-47a3-aa0a-c52ef7ef4747` |
|TopicName |String |否 |表示存储日志的日志主题的名称。如果该日志主题不存在，CDN 会创建该主题。该参数的输入要求如下：<br><br><br>* 长度为 3～64 个字符。<br><br>* 只能包含中文、小写字母、数字、下划线（_）和连字符（\-）。<br><br>* 不能以下划线（_）或连字符（\-）开头或结尾。<br><br>* 不能以 `tls_`、`tos_`、`tls-` 开头。<br><br><br>说明<br><br>如果该日志主题已在其他投递任务中指定，您无法指定该日志主题。<br><br>您可以调用 [ListRealtimeLogDeliveryTask](https://docs.byteplus.com/en/docs/byteplus-cdn/ListRealtimeLogDeliveryTask_zh-cn) 判断某个日志主题是否已被其他任务指定。 |`test_topic` |
|Ttl |Long |否 |表示日志的存储时长，范围为 1 \- 3649，单位是天。<br><br>如果您输入 `3650`，表示日志将永久保存。 |`3` |
|Splunk |Object |否 |当 `TaskType` 为 `splunk` 时，该结构体表示 Splunk 侧的相应配置。 | |
|CompressType |String |否 |表示在 CDN 投递日志时，是否启用 Gzip 压缩。该参数有以下取值：<br><br><br>* `true`：表示启用 Gzip 压缩。<br><br>* `false`：表示不启用 Gzip 压缩。<br><br><br>该参数的默认值是 `false`。 |`true` |
|Token |String |是 |表示 HEC 鉴权 Token。 |`B5A79AAD-D822-46CC-80D1-819F80D7BFB0` |
|Url |String |是 |表示 HEC 接口地址。 |`https://192.168.1.100:8088/services/collector` |
|BigQuery |Object |否 |当 `TaskType` 为 `bigquery` 时，该结构体表示 BigQuery 侧的相应配置。<br><br>前提条件<br><br>在调用本 API 创建日志投递任务前，您必须先在 Google BigQuery 中创建目标数据表（Table），并为该表配置能够接收 CDN 实时日志标准字段的表 Schema。<br><br>配置方法：在 BigQuery 控制台创建数据表时，请在 **Schema** 配置区域中，开启 **Edit as text** 模式，然后将附件中的 JSON 代码粘贴至文本框中，以生成正确的表 schema。<br><br>&nbsp;<br><br> | |
|Authentication |String |否 |Google Cloud 服务账号（Service Account）的 JSON 格式密钥。该密钥包含身份认证信息，用于授权 BytePlus CDN 访问您的 BigQuery 资源并流式写入日志。<br><br>说明<br><br>您需要将 GCP JSON 密钥文件中的内容序列化为一个完整的单行字符串作为 `Authentication` 参数的值，处理规则如下：<br><br><br>* 将 JSON 文件中的所有双引号 `"` 转换为 `\"`。<br><br>* 将换行符转换为 `\n`。 |`参见下方示例` |
|DatasetID |String |否 |您在 BigQuery 中创建的数据集（Dataset）ID。 |`cdn_logs_dataset` |
|ProjectID |String |否 |BigQuery 所在的 GCP 项目（Project）ID。 |`my-project` |
|TableID |String |否 |您在 BigQuery 中创建的表（Table）ID。 |`access_logs` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|TaskID |String |表示任务的 ID。 |`b23298e8-c262-4cb6-8138-2c311230b972` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

**投递目标为 HTTP 服务器**

```json
POST https://cdn.byteplusapi.com/?Action=CreateRealtimeLogDeliveryTask&Version=2021-03-01
{
    "Area": "outside_chinese_mainland",
    "Domain": "img.example.com",
    "Desc": "mydesc",
    "HttpServer": {
        "Url": "http://www.example.com:8000/mylogs",
        "AuthMechanism": true,
        "SecretKey": "xxxxxxxxxx",
        "CompressType": "gzip",
        "RequestHeader": [
            {
                "key": "header1",
                "value": "value1"
            },
            {
                "key": "header2",
                "value": "value2"
            }
        ]
    },
    "SampleRate": 50.55,
    "TaskType": "http_server"
}
```


**投递目标为 TLS**

```json
POST https://cdn.byteplusapi.com/?Action=CreateRealtimeLogDeliveryTask&Version=2021-03-01
{
    "Area": "outside_chinese_mainland",
    "Desc": "myDesc",
    "Domain": "www.example.com,img.example.com",
    "SampleRate": 100,
    "TaskType": "tls",
    "Tls": {
        "Endpoint": "tls-ap-southeast-1.volces.com`",
        "ProjectID": "a9db2fef-d7f8-47a3-aa0a-c52ef7ef4747",
        "TopicName": "topic2",
        "Ttl": 7
    }
}
```


**投递目标为 SLS**

```json
POST https://cdn.byteplusapi.com/?Action=CreateRealtimeLogDeliveryTask&Version=2021-03-01
{
    "Area": "outside_chinese_mainland",
    "Desc": "myDesc",
    "Domain": "www.example.com",
    "SampleRate": 100,
    "Sls": {
        "AccessKeyId": "xxxxxxxxxxxxxxxxxx",
        "AccessKeySecret": "xxxxxxxxxxxxx",
        "Endpoint": "ap-southeast-1.log.aliyuncs.com",
        "LogStore": "my_store",
        "Project": "my_project"
    },
    "TaskType": "sls"
}
```


**投递目标为 Splunk 日志服务**

```json
POST https://cdn.byteplusapi.com/?Action=CreateRealtimeLogDeliveryTask&Version=2021-03-01
{
    "Area": "outside_chinese_mainland",
    "Desc": "myDesc",
    "Domain": "www.example.com",
    "SampleRate": 100,
    "Splunk": {
        "Url": "https://192.168.1.100:8088/services/collector",
        "Token": "B5A79AAD-D822-46CC-80D1-819F80D7BFB0",
        "CompressType": "true"
    },
    "TaskType": "splunk"
}
```


**投递目标为 GCP BigQuery**

```json
POST https://cdn.byteplusapi.com/?Action=CreateRealtimeLogDeliveryTask&Version=2021-03-01
{
  "Area": "outside_chinese_mainland",
  "Domain": "www.example.com",
  "TaskType": "bigquery",
  "Desc": "Test",
  "SampleRate": 100,
  "BigQuery": {
    "ProjectID": "your-project-id",
    "Authentication": "{\n  \"type\": \"service_account\",\n  \"project_id\": \"your-project-id\",\n  \"private_key_id\": \"your_private_key_id\",\n  \"private_key\": \"-----BEGIN PRIVATE KEY-----\\nYOUR_PRIVATE_KEY_CONTENT_HERE\\n-----END PRIVATE KEY-----\\n\",\n  \"client_email\": \"your-service-account@your-project-id.iam.gserviceaccount.com\",\n  \"client_id\": \"123456789012345678901\",\n  \"auth_uri\": \"https://accounts.google.com/o/oauth2/auth\",\n  \"token_uri\": \"https://oauth2.googleapis.com/token\",\n  \"auth_provider_x509_cert_url\": \"https://www.googleapis.com/oauth2/v1/certs\",\n  \"client_x509_cert_url\": \"https://www.googleapis.com/robot/v1/metadata/x509/your-service-account%40your-project-id.iam.gserviceaccount.com\",\n  \"universe_domain\": \"googleapis.com\"\n}",
    "DatasetID": "cdn_logs_dataset",
    "TableID": "access_logs"
  }
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20251030172232277BC0277930A92087E9",
        "Action": "CreateRealtimeLogDeliveryTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskID": "b23298e8-c262-4cb6-8138-2c311230b972"
    }
}
```


&nbsp;
