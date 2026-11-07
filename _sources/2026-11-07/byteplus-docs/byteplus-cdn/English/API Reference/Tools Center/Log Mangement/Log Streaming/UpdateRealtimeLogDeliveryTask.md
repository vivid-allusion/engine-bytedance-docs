---
title: "UpdateRealtimeLogDeliveryTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateRealtimeLogDeliveryTask_en-us"
---

Modifies the configuration of a real\-time log delivery task.

When calling this API,


* You must specify one of the following structures: `HttpServer`, `Sls`, `Tls`, `Splunk`, `BigQuery`.

* If a parameter is not specified, it is set to its default value.


<span id="usage-limits"></span>
## Usage Limits

Throttling: You can submit a maximum of 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=UpdateRealtimeLogDeliveryTask&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `UpdateRealtimeLogDeliveryTask`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Area |String |Yes |The value of this parameter can only be `chinese_mainland`, indicating the Chinese mainland. |`outside_chinese_mainland` |
|Domain |String |Yes |Specifies the list of domains associated with the task.<br><br><br>* To associate all domains under the account, pass `*`. Here, all domains include those you subsequently add in CDN.<br><br>* To associate specific domains, pass the list of domains to be associated. The list can contain up to 200 domains, separated by commas (,).<br><br><br>warning<br><br>If there is already another task associated with specific domains, you cannot specify `Domain` as `*`.<br><br>You can call ListRealtimeLogDeliveryTask and specify this domain as a filter to check whether the domain is already associated with a task. |`www.example.com,img.example.com` |
|TaskID |String |Yes |Specifies the ID of a task to be modified. |`b23298e8-c262-4cb6-8138-2c311230b972` |
|Desc |String |No |Specifies the description of the task. The input requirements for this parameter are as follows:<br><br><br>* The length is 3 to 64 characters. It can contain Chinese characters, letters, digits, underscores (_), and hyphens (\-). A Chinese character occupies 3 characters.<br><br>* It cannot start or end with a hyphen (\-) or underscore (_). |`newDesc` |
|HttpServer |Object |No |Represents the corresponding configuration on the HTTP server side. | |
|AuthMechanism |Boolean |No |Specifies whether authentication is enabled for the HTTP server. This parameter supports the following values:<br><br><br>* `true`<br><br>* `false` |`true` |
|CompressType |String |No |Specifies the compression type enabled during CDN log delivery. This parameter supports the following values:<br><br><br>* `gzip`: Indicates Gzip compression.<br><br><br>If this parameter is not specified, compression is not enabled. |`gzip` |
|RequestHeader |Object[] |No |Specifies the list of additional headers to be included in the request when CDN delivers logs to the HTTP server. The list can contain up to 10 headers.<br><br>If this parameter is not specified, no additional headers are added to the request. | |
|Key |String |No |Specifies the Key of a header in the list. The length cannot exceed 1,024 characters. `Key` cannot be `User-Agent` or start with `x-bdcdn-`. |`mykey` |
|Value |String |No |Specifies the value of `Key`. The length cannot exceed 1,024 characters. |`myvalue` |
|SecretKey |String |No |Specifies the authentication Key used to calculate the token. The length of this parameter is 6 to 40 characters.<br><br>If `AuthMechanism` is `true`, `SecretKey` must be specified.<br><br>For more information about the authentication process and token algorithm, see [Create a log delivery task](https://www.volcengine.com/docs/6454/1536426#http-%E6%9C%8D%E5%8A%A1%E5%99%A8). |`xxxxxxxxx` |
|Url |String |No |Specifies the endpoint, port, and log storage path of the HTTP server. The port is optional. The endpoint must start with `http://` or `https://` and cannot exceed 1,024 characters in length. |`https://img.example.com:8090/cdn-logs` |
|SampleRate |Double |No |Specifies the log sampling rate. The value range is 0.00 to 100.00, accurate to two decimal places.<br><br>The sampling rate refers to the proportion of delivered logs. For example, if you set the sampling rate to 10, it means that for every 100 logs collected on the CDN node, CDN randomly selects 10 logs to deliver to your specified location. |`70` |
|Sls |Object |No |Represents the corresponding configuration on the SLS side. | |
|AccessKeyId |String |No |Specifies the AccessKey ID of your Alibaba Cloud account. The length cannot exceed 128 characters. |`xxxxxxxxxxxx` |
|AccessKeySecret |String |No |Specifies the AccessKey Secret of your Alibaba Cloud account. The length cannot exceed 128 characters. |`xxxxxxxxx` |
|Endpoint |String |No |Specifies the public domain name of the `Project`. |`ap-southeast-1.log.aliyuncs.com` |
|LogStore |String |No |Specifies the LogStore where logs are stored. |`myStore` |
|Project |String |No |Specifies the log project to which the `LogStore` belongs. This project is in the delivery region corresponding to the `Endpoint`. |`myProject` |
|Tls |Object |No |Represents the corresponding configuration on the TLS side. | |
|Ttl |Long |No |Specifies the storage duration of the logs. The value range is 1 to 3649, in days.<br><br>If you enter `3650`, the logs will be stored permanently. |`3` |
|Splunk |Object |No |Represents the corresponding configuration on the Splunk side. | |
|CompressType |String |No |Indicates whether to enable Gzip compression during CDN log delivery. This parameter supports the following values:<br><br><br>* `true`: Enables Gzip compression.<br><br>* `false`: Disables Gzip compression.<br><br><br>The default value is `false`. |`true` |
|Token |String |Yes |Indicates the HEC authentication token. |`B5A79AAD-D822-46CC-80D1-819F80D7BFB0` |
|Url |String |Yes |Indicates the HEC endpoint. |`https://192.168.1.100:8088/services/collector` |
|BigQuery |Object |No |Represents the corresponding configuration on the BigQuery side. | |
|Authentication |String |No |The JSON\-formatted key of your Google Cloud Service Account. It contains authentication credentials that authorize BytePlus CDN to access your BigQuery resources and stream logs.<br><br>tip<br><br>You need to serialize the content of the GCP JSON key file into a complete single\-line string as the value of the `Authentication` parameter. The processing rules are as follows:<br><br><br>* Escape all double quotes `"` in the JSON file to `\"`.<br><br>* Convert newline characters to `\n`. | |
|DatasetID |String |No |The ID of the dataset you created in BigQuery. |`my_dataset` |
|ProjectID |String |No |The ID of the GCP project where BigQuery resides. |`my-project` |
|TableID |String |No |The ID of the table you created in BigQuery. |`my_table` |


<span id="response-parameters"></span>
## Response Parameters

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

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
