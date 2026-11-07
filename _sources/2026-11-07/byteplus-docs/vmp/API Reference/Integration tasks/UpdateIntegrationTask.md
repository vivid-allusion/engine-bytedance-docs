---
title: "UpdateIntegrationTask"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/UpdateIntegrationTask"
---

Update an integration task.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VMP has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an access point that is optimal for the region of your services according to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) document.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=UpdateIntegrationTask&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required or not** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdateIntegrationTask |The name of the API. The name of the current API is `UpdateIntegrationTask`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Id |String |Yes |fcbc7eef\-2f6c\-4247\-bce1\*\*\* |The ID of the integration task. |
|Name |String |No |integration\-demo |The name of the integration task.<br><br><br>* The name is a string of 1 to 40 characters.<br><br>* The name can contain Chinese characters, letters, digits, and underscores (_).`_` |
|WorkspaceId |String |No |e28ae750\-bbb8\-4ff4\-abf4\*\*\* |Workspace ID. |
|Params |String |No |{\"JobName\":\"test\",\"ScrapeInterval\":\"1m\",\"Regions\":{\"cn\-beijing\":{\"VCM_ALB\":{},\"VCM_ECS\":{}}},\"MetaLabelWithNewMetric\":false,\"RelabelConfigs\":\"\- action: drop\\n  source_labels:\\n  \- __name__\\n  regex: metricA\|metricB\"} |Settings related to the integration task. The value of this parameter must be a string converted from a JSON object. For details, see [Params](https://docs.byteplus.com/en/docs/88/69224#gDeReb6r). |


<span id="gDeReb6r"></span>
### Params

If the type of the integration is `CloudMonitor`, the Params parameter contains fields shown in the table below.


|**Parameter** |**Type** |**Required or not** |**Sample value** |**Description** |
|---|---|---|---|---|
|JobName |String |No |test |The name of the integration task. |
|ScrapeInterval |String |No |1m |Time interval of collecting metrics.<br><br><br>* It is a numeric value followed by an abbreviated unit (s for seconds and m for minutes). For example, to collect metrics at intervals of 1 minute, set the value to 1m.<br><br>* The valid range is 30s to 5m. |
|Regions |Object |No |{"cn\-beijing": {"VCM_ALB": {}}} |The mapping between cloud services and regions, with the regions as the keys (for example, `cn-beijing`). |
|MetaLabelWithNewMetric |Boolean |No |false |Specifies whether to export metadata labels by using the new metric volc_resource_info.<br><br><br>* **true**: uses the new metric `volc_resource_info` to export metadata labels.<br><br>* **false**: adds metadata labels to cloud service metrics.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For details, see <a href="https://docs.byteplus.com/en/docs/vmp/Monitoring-cloud-services#.5p-l6K-i5LqR5Lqn5ZOB5oyH5qCH">Query metadata of cloud service instances</a>.</div><br> |
|ExportedTags |Array of String |No |demo |Label keys to be added to cloud service metrics. |
|RelabelConfigs |String |No |\- action: drop\n  source_labels:\n  \- __name__\n  regex: metricA\|metricB |Metric relabeling settings. For details, see [Metric relabeling](https://docs.byteplus.com/en/docs/vmp/Metric_relabel). |


To construct a Params parameter, use the following steps:


1. Construct a JSON structure that contains fields allowed in the Params parameter. The following code is an example of a JSON structure.


```JSON
{
    "JobName": "test",
    "ScrapeInterval": "1m",
    "Regions": {
        "cn-beijing": {
            "VCM_ALB": {},
            "VCM_ECS": {}
        }
    },
    "MetaLabelWithNewMetric": false,
    "RelabelConfigs": "- action: drop\n  source_labels:\n  - __name__\n  regex: metricA|metricB"
}
```



2. Escape the JSON structure into a string by using an escaping tool.


```JSON
{\"JobName\":\"test\",\"ScrapeInterval\":\"1m\",\"Regions\":{\"cn-beijing\":{\"VCM_ALB\":{},\"VCM_ECS\":{}}},\"MetaLabelWithNewMetric\":false,\"RelabelConfigs\":\"- action: drop\\n  source_labels:\\n  - __name__\\n  regex: metricA|metricB\"}
```



3. Set the string as the value of `Params` .


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=UpdateIntegrationTask&Version=2021-03-03
Content-Type: application/json
{
    "Id": "fcbc7eef-2f6c-4247-bce1***",
    "Name": "integration-demo",
    "WorkspaceId": "e28ae750-bbb8-4ff4-abf4***",
    "Params": "{\"JobName\":\"test\",\"ScrapeInterval\":\"1m\",\"Regions\":{\"cn-beijing\":{\"VCM_ALB\":{},\"VCM_ECS\":{}}},\"MetaLabelWithNewMetric\":false,\"RelabelConfigs\":\"- action: drop\\n  source_labels:\\n  - __name__\\n  regex: metricA|metricB\"}"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |fcbc7eef\-2f6c\-4247\-bce1\*\*\* |The ID of the integration task. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateIntegrationTask",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "fcbc7eef-2f6c-4247-bce1***"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The error codes for this API are listed in the table below. For a list of error codes for other APIs, see [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).


|**HTTP status code** |**Error code** |**Error message** |**Description** |
|---|---|---|---|
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP service. |
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |An invalid parameter was found. For example, an invalid workspace name was included in requests. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |A required parameter is missing. |
