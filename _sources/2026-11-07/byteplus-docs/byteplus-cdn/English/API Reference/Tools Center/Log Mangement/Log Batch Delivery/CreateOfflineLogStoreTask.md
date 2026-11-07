---
title: "CreateOfflineLogStoreTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CreateOfflineLogStoreTask_en-us"
---

Creates a log batch delivery task in CDN.

<span id="usage-limits"></span>
## Usage Limits

Throttling Limit: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=CreateOfflineLogStoreTask&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `CreateOfflineLogStoreTask`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Bucket |String |Yes |Indicates the directory path where log files are stored in the bucket. It cannot end with `/`. The format is `<Bucket Name>/<Directory Path>`.<br><br>If the directory in the path does not exist, CDN will create the corresponding directory in the bucket. |`mybucket/storage/logs` |
|Domain |String |Yes |Indicates which domain's real\-time logs are to be delivered, that is, the domains to be associated with the task.<br><br><br>* If you want to associate all domains under your account, pass in `*`. Here, all domains cover the domains you subsequently add in CDN.<br><br>* If you want to associate specified domains, pass in the list of domains to be associated. The list can contain up to 200 domains, separated by commas (,).<br><br><br>warning<br><br>If you have created a task that is associated with all domains under your account, you cannot create a task that is associated with specified domains. The reverse is also true.<br><br>You can call [ListOfflineLogStoreTask](https://docs.byteplus.com/en/docs/byteplus-cdn/ListOfflineLogStoreTask_en-us) and specify this domain as a filter condition to see if the domain is already associated with a task. |`www.example.com,img.example.com` |
|Endpoint |String |Yes |Represents the public access point of the object storage service, excluding the bucket name.<br><br><br>* If `TaskType` is `s3`, the access point must start with `https://`, not include the bucket name, and the length cannot exceed 1,024 characters.<br><br>* If `TaskType` is `tos`, this parameter has the following values, corresponding to the values of `Region`.<br><br>   * `tos-cn-hongkong.volces.com`<br><br>   * `tos-ap-southeast-1.volces.com`<br><br>   * `tos-ap-southeast-3.volces.com` |`https://oss-ap-southeast-1.aliyuncs.com` |
|Region |String |Yes |Indicates the region code of the bucket. The length cannot exceed 64 characters.<br><br><br>* If `TaskType` is `s3`, please consult the object storage service provider of the bucket to obtain the region code of the bucket.<br><br>* If `TaskType` is `tos`, the region code has the following values:<br><br>   * `cn-hongkong`: Indicates Hong Kong, China.<br><br>   * `ap-southeast-1`: Indicates Asia Pacific (Johor).<br><br>   * `ap-southeast-3`: Indicates Asia Pacific (Jakarta). |`ap-southeast-1` |
|TaskType |String |Yes |Represents the log batch delivery target, with the following values:<br><br><br>* `tos`: Represents BytePlus Object Storage (TOS).<br><br>* `s3`: Represents AWS S3 or an object storage service that uses S3\-compatible authentication. |`s3` |
|AuthInformation |Object |No |Represents the access credential of the batch delivery target. You only need to specify this structure when `PrivateBucketAccess` is `true` and `TaskType` is `s3`. | |
|AccessKeyID |String |No |Represents the AccessKey ID in the credential. |`xxxxxxxxxxxxx` |
|AccessKeySecret |String |No |Represents the AccessKey Secret in the credential. |`xxxxx` |
|Desc |String |No |Represents the description of the task. The length is 3\-45 characters and can contain Chinese characters, letters, and numbers, but cannot start or end with an underscore (_). |`myDesc` |
|PrivateBucketAccess |Boolean |No |Indicates whether the bucket is private. This parameter has the following values:<br><br><br>* `true`<br><br>* `false`<br><br><br>The default value of this parameter is `false`. |`true` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|TaskID |String |Represents the ID of the task. |`nj2S29or5KaAeEiwcGWA5S` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

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


<span id="sample-response"></span>
### Sample response

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
