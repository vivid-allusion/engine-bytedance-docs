---
title: "CreateOfflineLogStoreTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CreateOfflineLogStoreTask_zh-cn"
---

在 CDN 中创建一个离线日志转存任务。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=CreateOfflineLogStoreTask&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `CreateOfflineLogStoreTask`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Bucket |String |是 |表示存储桶下存放日志文件的目录路径，不能以 `/` 结尾，格式为 `<存储桶名称>/<目录路径>`。<br><br>如果路径中的目录不存在，CDN 会在存储桶下创建相应的目录。 |`mybucket/storage/logs` |
|Domain |String |是 |表示投递哪些域名的实时日志，也就是该任务将关联的域名。<br><br><br>* 如果您要关联账号下的所有域名，请传入`*`。这里，所有域名涵盖您后续在 CDN 中添加的域名。<br><br>* 如果您要关联指定的域名，请传入待关联的域名列表，列表中最多可以包含 200 个域名，多个域名之间以逗号（,）分隔。<br><br><br>注意<br><br>如果您已创建了关联账号下所有域名的任务，则无法再创建关联指定域名的任务。反之亦然。<br><br>您可以调用 [ListOfflineLogStoreTask](https://docs.byteplus.com/en/docs/byteplus-cdn/ListOfflineLogStoreTask_zh-cn) 并指定指定该域名作为过滤条件，以查看该域名是否已与某个任务关联。 |`www.example.com,img.example.com` |
|Endpoint |String |是 |表示对象存储服务的公网访问点，不包含存储桶的名称。<br><br><br>* 如果 `TaskType` 为 `s3`，访问点必须以 `https://`开头，不包含存储桶的名称，长度不能超过 1,024 个字符。<br><br>* 如果 `TaskType` 为 `tos`，该参数有以下取值，与 `Region` 的取值对应。<br><br>   * `tos-cn-hongkong.volces.com`<br><br>   * `tos-ap-southeast-1.volces.com`<br><br>   * `tos-ap-southeast-3.volces.com` |`tos-ap-southeast-1.volces.com` |
|Region |String |是 |表示存储桶所在的地域代码（region code），长度不能超过 64 个字符。<br><br><br>* 如果 `TaskType` 为 `s3`，请咨询该存储桶的对象存储服务提供商以获取该存储桶的地域代码。<br><br>* 如果 `TaskType` 为 `tos`，地域代码有以下取值：<br><br>   * `cn-hongkong`：表示中国香港。<br><br>   * `ap-southeast-1`：表示亚太东南（柔佛）。<br><br>   * `ap-southeast-3`：表示亚太东南（雅加达）。 |`ap-southeast-1` |
|TaskType |String |是 |表示日志转存目标，有以下取值：<br><br><br>* `tos`：表示 BytePlus 对象存储（TOS）。<br><br>* `s3`：表示 AWS S3 或者使用兼容 S3 鉴权方式的对象存储服务。 |`s3` |
|AuthInformation |Object |否 |表示转存目标的访问凭证。仅当 `PrivateBucketAccess` 为 `true` 并且 `TaskType` 为 `s3` 时，您需要指定该结构体。 | |
|AccessKeyID |String |否 |表示凭证中的 AccessKey ID。 |`xxxxxxxxxxxxx` |
|AccessKeySecret |String |否 |表示凭证中的 AccessKey Secret。 |`xxxxx` |
|Desc |String |否 |表示任务的描述，长度为 3\-45 个字符，可以包含汉字，字母，数字，但不能以下划线（_）开头或结尾。 |`myDesc` |
|PrivateBucketAccess |Boolean |否 |表示该存储桶是否是私有的，该参数有以下取值：<br><br><br>* `true`<br><br>* `false`<br><br><br>该参数的默认值是 `false`。 |`true` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|TaskID |String |表示任务的 ID。 |`nj2S29or5KaAeEiwcGWA5S` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

**日志转存目标为 TOS**

```json
POST https://cdn.byteplusapi.com/?Action=CreateOfflineLogStoreTask&Version=2021-03-01
{
    "Bucket": "myBucket/logfile",
    "Desc": "myDesc",
    "Domain": "www.example.com,img.example.com",
    "Endpoint": "tos-ap-southeast-1.volces.com",
    "PrivateBucketAccess": true,
    "Region": "ap-southeast-1",
    "TaskType": "tos"
}
```


**日志转存目标为 AWS S3**

```json
POST https://cdn.byteplusapi.com/?Action=CreateOfflineLogStoreTask&Version=2021-03-01
{
    "AuthInformation": {
        "AccessKeyID": "xxxxxxxxxxxxxxx",
        "AccessKeySecret": "xxxxxxxx"
    },
    "Bucket": "mybucket/log",
    "Desc": "myDesc",
    "Domain": "www.example.com",
    "Endpoint": "https://mybucket.s3-website-us-east-1.amazonaws.com",
    "PrivateBucketAccess": true,
    "Region": "us-east-1",
    "TaskType": "s3"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202510311813528D239468E6A7A99DA92C",
        "Action": "CreateOfflineLogStoreTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskID": "5daCXtLTDpRYDDhFruQ9hP"
    }
}
```


&nbsp;
