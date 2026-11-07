---
title: "CreateRealtimeLogDeliveryTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CreateRealtimeLogDeliveryTask_en-us"
---

Creates a log streaming task in CDN. A maximum of 20 tasks can exist under the primary account.

<span id="usage-limits"></span>
## Usage Limits

Throttling Limit: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=CreateRealtimeLogDeliveryTask&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `CreateRealtimeLogDeliveryTask`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Area |String |Yes |Indicates from which service area's CDN nodes to collect logs. Currently, the value of this parameter can only be `outside_chinese_mainland`, which means global (excluding the Chinese Mainland). |`outside_chinese_mainland` |
|Domain |String |Yes |Indicates which domain's real\-time logs are to be delivered, that is, the domains to be associated with the task.<br><br><br>* If you want to associate all domains under your account, pass in `*`. Here, all domains cover the domains you subsequently add in CDN.<br><br>* If you want to associate specified domains, pass in the list of domains to be associated. The list can contain up to 200 domains, separated by commas (,).<br><br><br>warning<br><br>If you have created a task that is associated with all domains under your account, you cannot create a task that is associated with specified domains. The reverse is also true.<br><br>You can call [ListRealtimeLogDeliveryTask](https://docs.byteplus.com/en/docs/byteplus-cdn/ListRealtimeLogDeliveryTask_en-us) and specify this domain as a filter condition to see if the domain is already associated with a task. |`www.example.com,img.example.com` |
|TaskType |String |Yes |Represents the delivery target, with the following values:<br><br><br>* `tls`: Represents BytePlus Log Service (TLS).<br><br>* `sls`: Represents Alibaba Cloud Log Service (SLS).<br><br>* `http_server`: Represents an HTTP server.<br><br>* `splunk`: Indicates Splunk.<br><br>* `bigquery`: Indicates GCP BigQuery。 |`sls` |
|Desc |String |No |Represents the description of the task. The input requirements for this parameter are as follows:<br><br><br>* The length is 3 \- 64 characters and can contain Chinese, letters, numbers, underscores (_), and hyphens (\-). Chinese characters occupy 3 characters.<br><br>* Cannot start or end with a hyphen (\-) or underscore (_). |`my desc` |
|HttpServer |Object |No |When `TaskType` is `http_server`, this structure represents the corresponding configuration on the HTTP server side. | |
|AuthMechanism |Boolean |No |Indicates whether authentication is enabled on the HTTP server. This parameter has the following values:<br><br><br>* `true`<br><br>* `false` |`true` |
|CompressType |String |No |Specifies the compression algorithm used for delivering logs in CDN. This parameter has the following values:<br><br><br>* `gzip`: Specifies the Gzip compression algorithm.<br><br><br>If this parameter is not specified, logs are not compressed. |`gzip` |
|RequestHeader |Object[] |No |Indicates the list of additional headers that need to be included in the request when CDN delivers logs to the HTTP server. The list can contain up to 10 headers.<br><br>If this parameter is not specified, it means that no additional headers are added to the request. | |
|Key |String |No |Represents the Key of a header in the list. The length cannot exceed 1,024 characters. `Key` cannot be `User-Agent`, nor can it start with `x-bdcdn-`. |`mykey` |
|Value |String |No |Represents the value of `Key`. The length cannot exceed 1,024 characters. |`myvalue` |
|SecretKey |String |No |Represents the authentication Key, which is used to calculate the token. The length of this parameter is 6\-40 characters.<br><br>If `AuthMechanism` is `true`, `SecretKey` must be specified.<br><br>For more information about the authentication process and token algorithm, see [Create a log delivery task](https://docs.byteplus.com/en/docs/byteplus-cdn/log-streaming-task-config_en-us). |`xxxxxxxxxx` |
|Url |String |No |Represents the access point, port, and log storage path of the HTTP server. The port is optional. The access point must start with `http://` or `https://`, and the length cannot exceed 1,024 characters. |`https://www.example.com:8080/cdn-logs` |
|SampleRate |Double |No |Represents the log sampling rate, ranging from 0.00 to 100.00, accurate to 2 decimal places.<br><br>The sampling rate refers to the proportion of delivered logs. For example, if you set the sampling rate to 10, it means that for every 100 logs collected on the CDN node, CDN will randomly select 10 logs to deliver to the location you specify. |`50.55` |
|Sls |Object |No |When `TaskType` is `sls`, this structure represents the corresponding configuration on the SLS side. | |
|AccessKeyId |String |No |Represents the AccessKey ID of your Alibaba Cloud account. The length cannot exceed 128 characters. |`xxxxxxxxxxxx` |
|AccessKeySecret |String |No |Represents the AccessKey Secret of your Alibaba Cloud account. The length cannot exceed 128 characters. |`xxxxxxxxx` |
|Endpoint |String |No |Represents the public domain name of the `Project`. |`ap-southeast-1.log.aliyuncs.com` |
|LogStore |String |No |Represents the LogStore where logs are stored. |`myStore` |
|Project |String |No |Represents the log project to which the `LogStore` belongs. |`myProject` |
|Tls |Object |No |When `TaskType` is `tls`, this structure represents the corresponding configuration on the TLS side. | |
|Endpoint |String |No |Represents the public domain name of the `Project`. This parameter has the following values, corresponding to the values of `Region`.<br><br><br>* `tls-cn-hongkong.volces.com`<br><br>* `tls-ap-southeast-1.volces.com`<br><br>* `tls-ap-southeast-3.volces.com` |`tls-ap-southeast-1.volces.com` |
|ProjectID |String |No |Represents the log project ID to which the log topic belongs. |`a9db2fef-d7f8-47a3-aa0a-c52ef7ef4747` |
|TopicName |String |No |Represents the name of the log topic where logs are stored. If the log topic does not exist, CDN will create it. The input requirements for this parameter are as follows:<br><br><br>* The length is 3 to 64 characters.<br><br>* Can only contain Chinese, lowercase letters, numbers, underscores (_), and hyphens (\-).<br><br>* Cannot start or end with an underscore (_) or hyphen (\-).<br><br>* Cannot start with `tls_`, `tos_`, or `tls-`.<br><br><br>tip<br><br>If the log topic has been specified in other delivery tasks, you cannot specify this log topic.<br><br>You can call [ListRealtimeLogDeliveryTask](https://docs.byteplus.com/en/docs/byteplus-cdn/ListRealtimeLogDeliveryTask_en-us) to determine whether a log topic has been specified by other tasks. |`test_topic` |
|Ttl |Long |No |Represents the storage duration of logs, ranging from 1 to 3649, in days.<br><br>If you enter `3650`, it means that the logs will be stored permanently. |`3` |
|Splunk |Object |No |When `TaskType` is `splunk`, this structure indicates the corresponding configuration on the Splunk side. | |
|CompressType |String |No |Indicates whether to enable Gzip compression during CDN log delivery. This parameter supports the following values:<br><br><br>* `true`: Enables Gzip compression.<br><br>* `false`: Disables Gzip compression.<br><br><br>The default value is `false`. |`true` |
|Token |String |Yes |Indicates the HEC authentication token. |`B5A79AAD-D822-46CC-80D1-819F80D7BFB0` |
|Url |String |Yes |Indicates the HEC endpoint. |`https://192.168.1.100:8088/services/collector` |
|BigQuery |Object |No |When `TaskType` is `bigquery`, this structure indicates the corresponding configuration on the BigQuery side.<br><br>Prerequisites<br><br>Before calling this API to create a log delivery task, you must first create a target table in Google BigQuery and configure a schema for it that can receive the standard fields of CDN real\-time logs.<br><br>**Configuration method**: When creating a table in the BigQuery console, navigate to the **Schema** configuration section, enable the **Edit as text** mode, and then paste the JSON code from the attachment into the text box to generate the correct table schema.<br><br>&nbsp;<br><br> | |
|Authentication |String |No |The JSON\-formatted key of your Google Cloud Service Account. It contains authentication credentials that authorize BytePlus CDN to access your BigQuery resources and stream logs.<br><br>tip<br><br>You need to serialize the content of the GCP JSON key file into a complete single\-line string as the value of the `Authentication` parameter. The processing rules are as follows:<br><br><br>* Escape all double quotes `"` in the JSON file to `\"`.<br><br>* Convert newline characters to `\n`. |`See the example below` |
|DatasetID |String |No |The ID of the dataset you created in BigQuery. |`my_dataset` |
|ProjectID |String |No |The ID of the GCP project where BigQuery resides. |`my-project` |
|TableID |String |No |The ID of the table you created in BigQuery. |`my_table` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|TaskID |String |Represents the ID of the task. |`b23298e8-c262-4cb6-8138-2c311230b972` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

**Delivery target is an HTTP server**

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


**Delivery target is TLS**

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


**Delivery target is SLS**

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


**Delivery target is Splunk**

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


**Delivery target is BigQuery**

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


<span id="sample-response"></span>
### Sample response

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
