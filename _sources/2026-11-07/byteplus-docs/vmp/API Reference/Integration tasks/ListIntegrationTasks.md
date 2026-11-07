---
title: "ListIntegrationTasks"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/ListIntegrationTasks"
---

Get a list of integration tasks.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VMP has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an access point that is optimal for the region of your services according to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) document.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=ListIntegrationTasks&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required or not** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListIntegrationTasks |The API name. The name of the current API is `ListIntegrationTasks`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|PageNumber |Long |No |1 |Current page number. The minimum and default values are both 1. |
|PageSize |Long |No |10 |Number per page:<br><br><br>* The value can range from 0 to 100.<br><br>* Default value is 10. |
|Filters |Object of [IntegrationFilter](https://docs.byteplus.com/en/docs/88/69225#integrationfilter) |No |\- |Filter conditions for integration tasks. |


<span id="integrationfilter"></span>
### IntegrationFilter


|**Parameter** |**Type** |**Required or not** |**Sample value** |**Description** |
|---|---|---|---|---|
|Ids |Array of String |No |fcbc7eef\-2f6c\-4247\-bce1\*\*\* |The IDs of the integration tasks. |
|Name |String |No |integration\-demo |Task name. Fuzzy search is supported. |
|Statuses |Array of String |No |Creating |The status of the integration task. Valid values:<br><br><br>* **Creating**: creating<br><br>* **Updating**: updating<br><br>* **Active**: working properly<br><br>* **Error**: errors occurred<br><br>* **Deleting**: deleting |
|Environment |String |No |Managed |The environment to which the integration task is deployed. Valid values:<br><br><br>* **Vke**: the integration task is deployed in a VKE cluster.<br><br>* **Managed**: the integration task is deployed in a managed environment.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When you create a Cloud Monitor integration task, you can select only a managed environment.</div><br> |
|WorkspaceId |String |No |e28ae750\-bbb8\-4ff4\-abf4\*\*\* |Workspace ID. |
|VkeClusterIds |Array of String |No |cd2i3c1beif8n1\*\*\* |The ID of the VKE cluster where the integration task is deployed. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=ListIntegrationTasks&Version=2021-03-03
Content-Type: application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filters": {
        "Ids": [
            "fcbc7eef-2f6c-4247-bce1***"
        ],
        "Name": "integration-demo",
        "Statuses": [
            "Creating"
        ],
        "Environment": "Managed",
        "WorkspaceId": "e28ae750-bbb8-4ff4-abf4***",
        "VkeClusterIds": [
            "cd2i3c1beif8n1***"
        ]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |D**Description**escription |
|---|---|---|---|
|Total |Long |100 |Total number of integration tasks. |
|Items |Array of [IntegrationTask](https://docs.byteplus.com/en/docs/88/69225#integrationtask) |\- |A list of integration tasks. |


<span id="integrationtask"></span>
### IntegrationTask


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |fcbc7eef\-2f6c\-4247\-bce1\*\*\* |The ID of the integration task. |
|Name |String |integration\-demo |The name of the integration task. |
|Type |String |CloudMonitor |Integration task type. |
|Status |String |Active |The status of the integration task. Valid values:<br><br><br>* **Creating**: creating<br><br>* **Updating**: updating<br><br>* **Active**: working properly<br><br>* **Error**: errors occurred<br><br>* **Deleting**: deleting |
|Environment |String |Vke |The environment to which the integration task is deployed. Valid values:<br><br><br>* **Vke**: the integration task is deployed in a VKE cluster.<br><br>* **Managed**: the integration task is deployed in a managed environment.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When you create a Cloud Monitor integration task, you can select only a managed environment.</div><br> |
|WorkspaceId |String |e28ae750\-bbb8\-4ff4\-abf4\*\*\* |Workspace ID. |
|VkeClusterId |String |cd2i3c1beif8n1\*\*\* |The ID of the VKE cluster that runs the integration task. |
|VkeClusterInfo |Object of [VkeClusterInfo](https://docs.byteplus.com/en/docs/88/69225#vkeclusterinfo) |\- |Information about the VKE cluster to which the integration task is deployed. |


<span id="vkeclusterinfo"></span>
### VkeClusterInfo


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Name |String |cluster\-demo |The VKE cluster name. |
|Status |String |Running |VKE cluster status. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListIntegrationTasks",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 100,
        "Items": [
            {
                "Id": "fcbc7eef-2f6c-4247-bce1***",
                "Name": "integration-demo",
                "Type": "CloudMonitor",
                "Status": "Active",
                "Environment": "Vke",
                "WorkspaceId": "e28ae750-bbb8-4ff4-abf4***",
                "VkeClusterId": "cd2i3c1beif8n1***",
                "VkeClusterInfo": {
                    "Name": "cluster-demo",
                    "Status": "Running"
                }
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for current API only are listed in the table below. See [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes) to view error codes for any APIs.


|**HTTP status codes** |**Error code** |**Error message** |**Description** |
|---|---|---|---|
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP service. |
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |An invalid parameter was found. For example, an invalid workspace name was included in requests. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing necessary parameters. |
