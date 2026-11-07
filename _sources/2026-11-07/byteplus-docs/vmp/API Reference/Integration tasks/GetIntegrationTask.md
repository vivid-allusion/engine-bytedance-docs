---
title: "GetIntegrationTask"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/GetIntegrationTask"
---

Get an integration task.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VMP has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an access point that is optimal for the region of your services according to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) document.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=GetIntegrationTask&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameters** |**Type** |**Required or not** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetIntegrationTask |The API name. The name of the current API operation is `GetIntegrationTask`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Id |String |Yes |fcbc7eef\-2f6c\-4247\-bce1\*\*\* |The ID of the integration task. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=GetIntegrationTask&Version=2021-03-03
Content-Type: application/json
{
    "Id": "fcbc7eef-2f6c-4247-bce1***"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Descriptions** |
|---|---|---|---|
|Id |String |fcbc7eef\-2f6c\-4247\-bce1\*\*\* |The ID of the integration task. |
|Name |String |test |The name of the integration task. |
|WorkspaceId |String |fcbc7eef\-2f6c\-4247\-bce1\*\*\* |Workspace ID. |
|Type |String |CloudMonitor |Integration task type. The value `CloudMonitor` indicates a Cloud Monitor integration task. |
|Status |String |Creating |The status of the integration task. Valid values:<br><br><br>* **Creating**: creating<br><br>* **Updating**: updating<br><br>* **Active**: working properly<br><br>* **Error**: errors occurred<br><br>* **Deleting**: deleting |
|Params |String |{\"JobName\":\"test\",\"ScrapeInterval\":\"1m\",\"Regions\":{\"cn\-beijing\":{\"VCM_ALB\":{},\"VCM_ECS\":{}}},\"MetaLabelWithNewMetric\":false,\"RelabelConfigs\":\"\- action: drop\\n  source_labels:\\n  \- __name__\\n  regex: metricA\|metricB\"} |Integration task settings. |
|Environment |String |Vke |The environment to which the integration task is deployed. Valid values:<br><br><br>* **Vke**: the integration task is deployed in a VKE cluster.<br><br>* **Managed**: the integration task is deployed in a managed environment.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When you create a Cloud Monitor integration task, you can select only a managed environment.</div><br> |
|VkeClusterId |String |cd2i3c1beif8n1\*\*\* |The ID of the VKE cluster where the integration task is deployed. |
|VkeClusterInfo |Object of [VkeClusterInfo](https://docs.byteplus.com/en/docs/88/69221#vkeclusterinfo) |\- |Information about the VKE cluster to which the integration task is deployed. |


<span id="vkeclusterinfo"></span>
### VkeClusterInfo


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Name |String |cluster\-demo |The name of the VKE cluster. |
|Status |String |Running |The VKE cluster status. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetIntegrationTask",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "fcbc7eef-2f6c-4247-bce1***",
        "Name": "test",
        "WorkspaceId": "fcbc7eef-2f6c-4247-bce1***",
        "Type": "CloudMonitor",
        "Status": "Creating",
        "Params": "{\"JobName\":\"test\",\"ScrapeInterval\":\"1m\",\"Regions\":{\"cn-beijing\":{\"VCM_ALB\":{},\"VCM_ECS\":{}}},\"MetaLabelWithNewMetric\":false,\"RelabelConfigs\":\"- action: drop\\n  source_labels:\\n  - __name__\\n  regex: metricA|metricB\"}",
        "Environment": "Vke",
        "VkeClusterId": "cd2i3c1beif8n1***",
        "VkeClusterInfo": {
            "Name": "cluster-demo",
            "Status": "Running"
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for current API only are listed in the table below. See [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes) to view error codes for any APIs.


|**HTTP status code** |**Error code** |**Error message** |**Description** |
|---|---|---|---|
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP service. |
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |Invalid parameters are found. For example, an invalid workspace name is included in requests. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing required parameters. |
