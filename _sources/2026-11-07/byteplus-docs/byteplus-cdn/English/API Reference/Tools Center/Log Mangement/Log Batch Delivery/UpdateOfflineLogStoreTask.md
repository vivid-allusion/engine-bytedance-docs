---
title: "UpdateOfflineLogStoreTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateOfflineLogStoreTask_en-us"
---

Modifies the configuration of a log batch delivery task. When calling this API, if a parameter is not specified, it will be set to its default value.

<span id="usage-limits"></span>
## Usage Limits

Throttling Limit: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=UpdateOfflineLogStoreTask&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `UpdateOfflineLogStoreTask`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Bucket |String |Yes |Indicates the directory path where log files are stored in the bucket. It cannot end with `/`. The format is `<Bucket Name>/<Directory Path>`.<br><br>If the directory in the path does not exist, CDN will create the corresponding directory in the bucket. |`mybucket/new/logs` |
|Domain |String |Yes |Represents the list of domains to be associated with the task.<br><br><br>* If you want to associate all domains under your account, pass in `*`. Here, all domains cover the domains you subsequently add in CDN.<br><br>* If you want to associate specified domains, pass in the list of domains to be associated. The list can contain up to 200 domains, separated by commas (,).<br><br><br>warning<br><br>If other tasks that are associated with specified domains already exist, you cannot specify `Domain` as `*`.<br><br>You can call [ListOfflineLogStoreTask](https://docs.byteplus.com/en/docs/byteplus-cdn/log-streaming-task-config_en-us) and specify this domain as a filter condition to see if the domain is already associated with a task. |`www.example.com` |
|Endpoint |String |Yes |Represents the public access point of the object storage service, excluding the bucket name.<br><br><br>* If the batch delivery target of the task represented by `TaskId` is `s3`, the access point must start with `https://`, not include the bucket name, and the length cannot exceed 1,024 characters.<br><br>* If the batch delivery target is `tos`, this parameter has the following values, corresponding to the values of `Region`.<br><br>   * `tos-cn-hongkong.volces.com`<br><br>   * `tos-ap-southeast-1.volces.com`<br><br>   * `tos-ap-southeast-3.volces.com` |`tos-ap-southeast-1.volces.com` |
|Region |String |Yes |Indicates the region code of the bucket. The length cannot exceed 64 characters.<br><br><br>* If the batch delivery target of the task represented by `TaskId` is `s3`, please consult the object storage service provider of the bucket to obtain the region code of the bucket.<br><br>* If the batch delivery target is `tos`, the region code has the following values:<br><br>   * `cn-hongkong`: Indicates Hong Kong, China.<br><br>   * `ap-southeast-1`: Indicates Asia Pacific Southeast (Johor).<br><br>   * `ap-southeast-3`: Indicates Asia Pacific Southeast (Jakarta). |`ap-southeast-1` |
|TaskID |String |Yes |Represents the ID of a task to be modified. |`dPFEQ8vwbRShTdW5kNbZe3` |
|AuthInformation |Object |No |Represents the access credential of the batch delivery target. You only need to specify this structure when `PrivateBucketAccess` is `true` and `TaskType` is `s3`. | |
|AccessKeyID |String |No |Represents the AccessKey ID in the credential. |`xxxxxxxxxx` |
|AccessKeySecret |String |No |Represents the AccessKey Secret in the credential. |`xxxxxx` |
|Desc |String |No |Represents the description of the task. The length is 3\-45 characters and can contain Chinese characters, letters, and numbers, but cannot start or end with an underscore (_). |`newDesc` |
|PrivateBucketAccess |Boolean |No |Indicates whether the bucket is private. This parameter has the following values:<br><br><br>* `true`<br><br>* `false`<br><br><br>The default value of this parameter is `false`. |`true` |


<span id="response-parameters"></span>
## Response Parameters

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=UpdateOfflineLogStoreTask&Version=2021-03-01
{
    "Bucket": "mybucket/new/log",
    "Desc": "myDesc_new",
    "Domain": "www.example.com",
    "Endpoint": "https://mybucket.s3-website-us-east-1.amazonaws.com",
    "PrivateBucketAccess": true,
    "Region": "us-east-1",
    "TaskID": "dPFEQ8vwbRShTdW5kNbZe3",
    "AuthInformation": {
        "AccessKeyID": "xxxxxxxxxxxxxxxxxxx",
        "AccessKeySecret": "xxxxxxxxxx"
    }
}
```


&nbsp;
