---
title: "UpdateRealtimeLogDeliveryTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateRealtimeLogDeliveryTask_zh-cn"
---

修改一个实时日志投递任务的配置。

在调用该 API 时，


* 您需要指定 `HttpServer`、`Sls`、`Tls`、`Splunk`、`BigQuery` 这五个结构体中的一个。

* 如果某个参数未指定，该参数将被设置为默认值。


<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=UpdateRealtimeLogDeliveryTask&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `UpdateRealtimeLogDeliveryTask`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Area |String |是 |该参数值只能是 `outside_chinese_mainland`，表示中国内地。 |`outside_chinese_mainland` |
|Domain |String |是 |表示该任务所关联的域名列表。<br><br><br>* 如果您要关联账号下的所有域名，请传入`*`。这里，所有域名涵盖您后续在 CDN 中添加的域名。<br><br>* 如果您要关联指定的域名，请传入待关联的域名列表，列表中最多可以包含 200 个域名，多个域名之间以逗号（,）分隔。<br><br><br>注意<br><br>如果已存在关联指定域名的其他任务，您无法指定 `Domain` 为 `*`。<br><br>您可以调用 ListRealtimeLogDeliveryTask 并指定指定该域名作为过滤条件，以查看该域名是否已与某个任务关联。 |`www.example.com,img.example.com` |
|TaskID |String |是 |表示一个待修改任务的 ID。 |`b23298e8-c262-4cb6-8138-2c311230b972` |
|Desc |String |否 |表示任务的描述。该参数的输入要求如下：<br><br><br>* 长度为 3 \- 64 个字符，可以包含中文、字母、数字、下划线（_）和连字符（\-）。中文占 3 个字符。<br><br>* 不能以连字符（\-）或下划线（_）开头或结尾。 |`newDesc` |
|HttpServer |Object |否 |表示 HTTP 服务器侧的相应配置。 | |
|AuthMechanism |Boolean |否 |表示 HTTP 服务器是否启用了鉴权。该参数有以下取值：<br><br><br>* `true`<br><br>* `false` |`true` |
|CompressType |String |否 |表示在 CDN 投递日志时所启用压缩类型。该参数有以下取值：<br><br><br>* `gzip`：表示 Gzip 压缩。<br><br><br>如果该参数不指定，表示不启用压缩。 |`gzip` |
|RequestHeader |Object[] |否 |表示 CDN 在向 HTTP 服务器投递日志时，请求中需要额外包含的头部列表。列表中最多可以包含 10 个头部。<br><br>如果该参数不指定，表示请求中不添加额外的头部。 | |
|Key |String |否 |表示列表中一个头部的 Key，长度不能超过 1,024 个字符。`Key` 不能是 `User-Agent`，也不能以 `x-bdcdn-` 开头 |`mykey` |
|Value |String |否 |表示 `Key` 的值，长度不能超过 1,024 个字符。 |`myvalue` |
|SecretKey |String |否 |表示鉴权 Key，用于计算令牌。该参数的长度为 6\-40 个字符。<br><br>如果 `AuthMechanism` 为 `true`，`SecretKey` 必须指定。<br><br>关于更多关于鉴权流程与令牌算法的信息，参见 [创建日志投递任务](https://www.volcengine.com/docs/6454/1536426#http-%E6%9C%8D%E5%8A%A1%E5%99%A8)。 |`xxxxxxxxx` |
|Url |String |否 |表示 HTTP 服务器的访问点、端口以及日志存放的路径。端口是可选的。访问点必须以 `http://` 或者 `https://` 开头，长度不能超过 1,024 个字符。 |`https://img.example.com:8090/cdn-logs` |
|SampleRate |Double |否 |表示日志采样率，范围为 0.00 \- 100.00，精确到 2 位小数。<br><br>采样率指的是投递的日志比例。例如，您设置采样率为 10，则意味着在 CDN 节点上每采集 100 条日志，CDN 会随机选择 10 条日志投递到您指定的位置。 |`70` |
|Sls |Object |否 |表示 SLS 侧的相应配置。 | |
|AccessKeyId |String |否 |表示您阿里云账号的 AccessKey ID，长度不能超过 128 个字符。 |`xxxxxxxxxxxx` |
|AccessKeySecret |String |否 |表示您阿里云账号的 AccessKey Secret，长度不能超过 128 个字符。 |`xxxxxxxxx` |
|Endpoint |String |否 |表示 `Project` 的公网域名。 |`ap-southeast-1.log.aliyuncs.com` |
|LogStore |String |否 |表示存储日志的 LogStore。 |`myStore` |
|Project |String |否 |表示 `LogStore` 所属的日志项目。该项目在 `Endpoint` 所对应的投递地域下。 |`myProject` |
|Tls |Object |否 |表示 TLS 侧的相应配置。 | |
|Ttl |Long |否 |表示日志的存储时长，范围为 1 \- 3649，单位是天。<br><br>如果您输入 `3650`，表示日志将永久保存。 |`3` |
|Splunk |Object |否 |表示 Splunk 侧的相应配置。 | |
|CompressType |String |否 |表示在 CDN 投递日志时，是否启用 Gzip 压缩。该参数有以下取值：<br><br><br>* `true`：表示启用 Gzip 压缩。<br><br>* `false`：表示不启用 Gzip 压缩。<br><br><br>该参数的默认值是 `false`。 |`true` |
|Token |String |是 |表示 HEC 鉴权 Token。 |`B5A79AAD-D822-46CC-80D1-819F80D7BFB0` |
|Url |String |是 |表示 HEC 接口地址。 |`https://192.168.1.100:8088/services/collector` |
|BigQuery |Object |否 |表示 BigQuery 侧的相应配置。 | |
|Authentication |String |否 |Google Cloud 服务账号（Service Account）的 JSON 格式密钥。该密钥包含身份认证信息，用于授权 BytePlus CDN 访问您的 BigQuery 资源并流式写入日志。<br><br>说明<br><br>您需要将 GCP JSON 密钥文件中的内容序列化为一个完整的单行字符串作为 `Authentication` 参数的值，处理规则如下：<br><br><br>* 将 JSON 文件中的所有双引号 `"` 转换为 `\"`。<br><br>* 将换行符转换为 `\n`。 | |
|DatasetID |String |否 |您在 BigQuery 中创建的数据集（Dataset）ID。 |`cdn_logs_dataset` |
|ProjectID |String |否 |BigQuery 所在的 GCP 项目（Project）ID。 |`my-project` |
|TableID |String |否 |您在 BigQuery 中创建的表（Table）ID。 |`access_logs` |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=UpdateRealtimeLogDeliveryTask&Version=2021-03-01
{
    "Area": "outside_chinese_mainland",
    "TaskID": "6af98494-c4fd-4c1b-bc36-88c4de0b5b9e",
    "Domain": "www.example.com",
    "Sls": {
        "AccessKeyId": "yyyyyyyyyyyyyyyyyy",
        "AccessKeySecret": "yyyyyyyyyy",
        "Endpoint": "ap-southeast-1.log.aliyuncs.com",
        "LogStore": "my_store",
        "Project": "my_project"
    }
}
```


&nbsp;
