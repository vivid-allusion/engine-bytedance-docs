---
title: "ListOfflineLogStoreTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListOfflineLogStoreTask_en-us"
---

Gets a list of log batch delivery tasks. You can specify a series of filter conditions to filter the task list.

<span id="usage-limits"></span>
## Usage Limits

Throttling Limit: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=ListOfflineLogStoreTask&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `ListOfflineLogStoreTask`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Bucket |String |No |Specify the path where log files are stored in the bucket as a filter condition. The format is `<Bucket Name>/<Log File Path>`. |`mybucket/storage/logs` |
|Desc |String |No |Specify `Desc` as a filter condition, which supports fuzzy matching. |`myDesc` |
|Domain |String |No |Specify a Domain as a filter condition to get the task of batch delivering the logs of that domain, that is, the domain associated with the task. |`www.example.com` |
|Region |String |No |Specify the region code of the bucket as a filter condition. The length of the region code cannot exceed 64 characters.<br><br><br>* If `TaskType` is `s3`, please consult the object storage service provider of the bucket to obtain the region code you can specify.<br><br>* If `TaskType` is `tos`, you can specify the following region codes:<br><br>   * `cn-hongkong`: Indicates Hong Kong, China.<br><br>   * `ap-southeast-1`: Indicates Asia Pacific Southeast (Johor).<br><br>   * `ap-southeast-3`: Indicates Asia Pacific Southeast (Jakarta). |`cn-beijing` |
|Status |String |No |Specify the status of a task as a filter condition. This parameter has the following values:<br><br><br>* `enable`: Indicates enabled.<br><br>* `disable`: Indicates disabled. |`enable` |
|TaskID |String |No |Specify a task ID as a filter condition. |`nj2S29or5KaAeEiwcGWA5S` |
|TaskType |String |No |Specify a batch delivery target as a filter condition. This parameter has the following values:<br><br><br>* `tos`: Represents BytePlus Object Storage (TOS).<br><br>* `s3`: Represents AWS S3 or an object storage service that uses S3\-compatible authentication. |`s3` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|TaskInfo |Object[] |Represents the list of tasks that meet the filter conditions. | |
|AuthInformation |Object |Represents the access credential of the batch delivery target. | |
|AccessKeyID |String |Represents the AccessKey ID in the credential. |`xxxxxxxxxxxxxxxxx` |
|AccessKeySecret |String |Represents the AccessKey Secret in the credential. |`xxxxxxxxx` |
|Bucket |String |Represents the path where log files are stored in the bucket. |`mybucket/log` |
|CreateTime |Long |Represents the creation time of the task, in Unix timestamp format. |`1761908274` |
|Desc |String |Represents the description of the task. |`myDesc` |
|Domain |String |Represents the domain associated with the task. |`www.example.net` |
|Endpoint |String |Represents the public access point of the object storage service. |`tos-cn-shanghai.volces.com` |
|PrivateBucketAccess |Boolean |Indicates whether the bucket is private. |`true` |
|Region |String |Represents the region code of the bucket. |`us-east-1` |
|Status |String |Represents the status of the task. This parameter has the following values:<br><br><br>* `enable`: Indicates that the task is enabled.<br><br>* `disable`: Indicates that the task is disabled. |`enable` |
|StatusDetail |Object[] |Represents the list of recent exceptions for the task. The list records up to 10 exceptions. | |
|Detail |String |Represents the details of the exception. |`exception details` |
|Time |Long |Represents the time when the exception occurred, in Unix timestamp format. |`1761815000` |
|TaskID |String |Represents the ID of the task. |`dPFEQ8vwbRShTdW5kNbZe3` |
|TaskType |String |Represents the log batch delivery target, with the following values:<br><br><br>* `tos`: Represents BytePlus Object Storage (TOS).<br><br>* `s3`: Represents AWS S3 or an object storage service that uses S3\-compatible authentication. |`s3` |
|UpdateTime |Long |Represents the last update time of the task, in Unix timestamp format. |`1761908274` |
|Total |Long |Represents the number of tasks in the list. |`1` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

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


<span id="sample-response"></span>
### Sample response

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
