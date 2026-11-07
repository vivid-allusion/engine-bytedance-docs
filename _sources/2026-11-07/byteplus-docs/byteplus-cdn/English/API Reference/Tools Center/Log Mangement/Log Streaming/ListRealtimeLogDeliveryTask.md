---
title: "ListRealtimeLogDeliveryTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListRealtimeLogDeliveryTask_en-us"
---

Gets a list of log streaming tasks. You can specify a series of filter conditions to filter the task list.

<span id="usage-limits"></span>
## Usage Limits

Throttling Limit: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=ListRealtimeLogDeliveryTask&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `ListRealtimeLogDeliveryTask`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Desc |String |No |Specify `Desc` as a filter condition, which supports fuzzy matching. |`my` |
|Domain |String |No |Specify a Domain as a filter condition to get the task of delivering the logs of that domain. |`www.example.com` |
|Status |String |No |Specify the status of a task as a filter condition. This parameter has the following values:<br><br><br>* `enable`: Indicates enabled.<br><br>* `disable`: Indicates disabled. |`enable` |
|TaskID |String |No |Specify a task ID as a filter condition. |`33a1f4df-f384-453e-9d59-3e9ff4b04b4e` |
|TaskType |String |No |Specify a delivery target as a filter condition. This parameter has the following values:<br><br><br>* `tls`: Represents BytePlus Log Service (TLS).<br><br>* `sls`: Represents Alibaba Cloud Log Service (SLS).<br><br>* `http_server`: Represents an HTTP server.<br><br>* `splunk`: Indicates Splunk.<br><br>* `bigquery`: Indicates BigQuery. |`tls` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|TaskInfo |Object[] |Represents the list of tasks that meet the filter conditions. | |
|Area |String |The value of this parameter is always `outside_chinese_mainland`. |`outside_chinese_mainland` |
|CreateTime |Long |Represents the creation time of the task, in Unix timestamp format. |`1761816153` |
|Desc |String |Represents the description of the task. |`myDesc` |
|Domain |String |Represents the list of domains associated with the task, that is, which domains' logs are delivered by the task. |`www.example.com` |
|HttpServer |Object |When `TaskType` is `http_server`, this structure represents the corresponding configuration on the HTTP server side. | |
|AuthMechanism |Boolean |Indicates whether authentication is enabled on the HTTP server. This parameter has the following values:<br><br><br>* `true`<br><br>* `false` |`true` |
|CompressType |String |Specifies the compression algorithm used for delivering logs in CDN. This parameter has the following values:<br><br><br>* `gzip`: Specifies the Gzip compression algorithm.<br><br><br>If the value for this parameter is an empty string (""), compression is not used. |`gzip` |
|RequestHeader |Object[] |Indicates the list of additional headers included in the request when CDN delivers logs to the HTTP server. | |
|Key |String |Represents the Key of a header in the list. |`key1` |
|Value |String |Represents the value of `Key`. |`value1` |
|SecretKey |String |Represents the authentication Key, which is used to calculate the token. This parameter is only valid when `AuthMechanism` is `true`.<br><br>For more information about the authentication process and token algorithm, see [Create a log delivery task](https://docs.byteplus.com/en/docs/byteplus-cdn/log-streaming-task-config_en-us). |`xxxxxxxxxxx` |
|Url |String |Represents the access point, port, and log storage path of the HTTP server. |`http://www.example.com:8080/mylog` |
|SampleRate |Double |Represents the log sampling rate. |`50` |
|Sls |Object |When `TaskType` is `sls`, this structure represents the corresponding configuration on the SLS side. | |
|AccessKeyId |String |Represents the AccessKey ID of your Alibaba Cloud account. |`xxxxxxxxxxxxxxxx` |
|AccessKeySecret |String |Represents the AccessKey Secret of your Alibaba Cloud account. |`xxxxxxxxxxxxx` |
|Endpoint |String |Represents the public domain name of the `Project`. |`ap-southeast-1.log.aliyuncs.com` |
|LogStore |String |Represents the LogStore where logs are stored. |`my_store` |
|Project |String |Represents the log project to which the `LogStore` belongs. |`my_project` |
|Status |String |Represents the status of the task. This parameter has the following values:<br><br><br>* `enable`: Indicates that the task is enabled.<br><br>* `disable`: Indicates that the task is disabled. |`enable` |
|StatusDetail |Object[] |Represents the list of recent exceptions for the task. The list records up to 10 exceptions. | |
|Detail |String |Represents the details of the exception. |`exception details` |
|Time |Long |Represents the time when the exception occurred, in Unix timestamp format. |`1761815000` |
|TaskID |String |Represents the ID of the task. |`42de0332-b6e0-4fe1-9a5a-847bb7471def` |
|TaskType |String |Represents the delivery target, with the following values:<br><br><br>* `tls`: Represents BytePlus Log Service (TLS).<br><br>* `sls`: Represents Alibaba Cloud Log Service (SLS).<br><br>* `http_server`: Represents an HTTP server.<br><br>* `splunk`: Indicates Splunk.<br><br>* `bigquery`: Indicates BigQuery. |`tls` |
|Tls |Object |When `TaskType` is `tls`, this structure represents the corresponding configuration on the TLS side. | |
|Endpoint |String |Represents the public domain name of the `Project`. |`tls-ap-southeast-1.volces.com` |
|ProjectID |String |Represents the log project ID to which the log topic belongs. |`a9db2fef-d7f8-47a3-aa0a-c52ef7ef4747` |
|ProjectName |String |Represents the name of the log project to which the log topic belongs. |`test` |
|Region |String |Represents the region where the log project is located. |`ap-southeast-1` |
|TopicID |String |Represents the ID of the log topic where logs are stored. |`b23298e8-c262-4cb6-8138-2c311230b972` |
|TopicName |String |Represents the name of the log topic where logs are stored. |`test4` |
|Ttl |Long |Represents the storage duration of logs, in days.<br><br>If the value of this parameter is `3650`, it means that the logs are stored permanently. |`3` |
|UpdateTime |Long |Represents the last update time of the task, in Unix timestamp format. |`1761816153` |
|Splunk |Object |When `TaskType` is `splunk`, this structure indicates the corresponding configuration on the Splunk side. | |
|CompressType |String |Indicates whether to enable Gzip compression during CDN log delivery. This parameter supports the following values:<br><br><br>* `true`: Enables Gzip compression.<br><br>* `false`: Disables Gzip compression.<br><br><br>The default value is `false`. |`true` |
|Token |String |Indicates the HEC authentication token. |`B5A79AAD-D822-46CC-80D1-819F80D7BFB0` |
|Url |String |Indicates the HEC endpoint. |`https://192.168.1.100:8088/services/collector` |
|BigQuery |Object |When `TaskType` is `bigquery`, this structure indicates the corresponding configuration on the BigQuery side. | |
|Authentication |String |The JSON\-formatted key of your Google Cloud Service Account. It contains authentication credentials that authorize BytePlus CDN to access your BigQuery resources and stream logs.无 | |
|DatasetID |String |The ID of the dataset you created in BigQuery. |`my_dataset` |
|ProjectID |String |The ID of the GCP project where BigQuery resides. |`my-project` |
|TableID |String |The ID of the table you created in BigQuery. |`my_table` |
|Total |Long |Represents the number of tasks in the list. |`3` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

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


<span id="sample-response"></span>
### Sample response

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
