---
title: "ListWorkspaces"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/ListWorkspaces"
---

Obtain a list of workspaces.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide to provide you with a more stable, lower\-latency experience. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=ListWorkspaces&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListWorkspaces |API name. The API name is `ListWorkspaces`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|PageNumber |Long |No |1 |Current page number. The minimum and default values are both 1. |
|PageSize |Long |No |10 |Results per page:<br><br><br>* A number from 0 to 100.<br><br>* The default number is 10. |
|Filters |Object of [WorkspaceFilter](https://docs.byteplus.com/en/docs/vmp/ListWorkspaces#workspacefilter) |No |\- |Filter conditions for workspaces. |
|TagFilters |Array of [TagFilter](https://docs.byteplus.com/en/docs/vmp/ListWorkspaces#tagfilter) |No |\- |Use labels to filter workspaces. |
|ProjectName |String |No |default |Project name. |


<span id="WorkspaceFilter"></span>
### WorkspaceFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Ids |Array of String |No |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |Exact query by workspace IDs. |
|Name |String |No |workspace\-demo |Fuzzy query by a workspace name. |
|Statuses |Array of String |No |["Active"] |Exact query by workspace statuses. Available statuses:<br><br><br>* **Creating**: in the process of creating<br><br>* **Active**: working properly<br><br>* **Updating**: in the process of updating<br><br>* **Deleting**: in the process of deleting<br><br>* **OverdueShutted**: shutdown due to overdue payment<br><br>* **Resuming**: in the process of reactivating<br><br>* **Error**: errors occurred |
|InstanceTypeIds |Array of String |No |["vmp.standard.15d"] |Exact query by workspace types. Available types:<br><br><br>* **vmp.standard.15d**: 15\-day storage workspace.<br><br>* **vmp.standard.30d**: 30\-day storage workspace.<br><br>* **vmp.standard.90d**: 90\-day storage workspace.<br><br>* **vmp.standard.180d**: 180\-day storage workspace.<br><br>* **vmp.standard.1y**: 1\-year storage workspace. |


<span id="TagFilter"></span>
### TagFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |Yes |doc |Key of the label. |
|Values |Array of String |No |demo |Value of the label. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=ListWorkspaces&Version=2021-03-03
Content-Type: application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filters": {
        "Ids": [
            "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
        ],
        "Name": "workspace-demo",
        "InstanceTypeIds": [
            "vmp.standard.15d"
        ]
    },
    "ProjectName": "default"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Total |Long |100 |Total number of workspaces. |
|Items |Array of [Workspace](https://docs.byteplus.com/en/docs/vmp/ListWorkspaces#workspace) |\- |Total number of workspaces. |


<span id="Workspace"></span>
### Workspace


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Workspace ID. |
|CreateTime |String |2022\-01\-01T00:00:00Z |The creation date of a workspace. It is presented in RFC3339 format. |
|Name |String |workspace\-demo |Workspace name. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/vmp/ListWorkspaces#tag) |\- |Workspace tags. |
|Description |String |This is a workspace description |Workspace description. |
|Status |String |Active |Workspace statuses:<br><br><br>* **Creating**: in the process of creating<br><br>* **Active**: working properly<br><br>* **Updating**: in the process of updating<br><br>* **Deleting**: in the process of deleting<br><br>* **OverdueShutted**: shutdown due to overdue payment<br><br>* **Resuming**: in the process of reactivating<br><br>* **Error**: errors occurred |
|InstanceTypeId |String |vmp.standard.15d |Workspace specifications. |
|OverdueReclaimTime |String |2022\-01\-01T00:00:00Z |Estimated reclaim time of workspace for overdue payments. It is presented in RFC3339 format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field remains empty until overdue payments happen.</div><br> |
|Username |String |admin |BasicAuth username of the workspace. |
|PrometheusQueryIntranetEndpoint |String |http://query.prometheus\-cn\-beijing.ivolces.com/workspaces/1d0\*\*\* |Query URL of the workspace. |
|PrometheusWriteIntranetEndpoint |String |http://write.prometheus\-cn\-beijing.ivolces.com/workspaces/1d0\*\*\* |RemoteWrite URL of the workspace. |
|PrometheusPushIntranetEndpoint |String |http://push.prometheus\-cn\-beijing.ivolces.com/workspaces/\*\*\*/api/v1/push |Push Gateway URL of the workspace. |
|DeleteProtectionEnabled |Boolean |true |Whether the deletion protection for a workspace is enabled:<br><br><br>* **true**: enabled.<br><br>* **false**: disabled. |
|ProjectName |String |default |Project name. |


<span id="Tag"></span>
### Tag


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Key |String |doc |Key of the label. |
|Value |String |demo |Value of the label. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListWorkspaces",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 100,
        "Items": [
            {
                "Id": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
                "Name": "workspace-demo",
                "Tags": [
                    {
                        "Key": "key1",
                        "Value": "value1"
                    }
                ],
                "Status": "Active",
                "Username": "admin",
                "Description": "This is a workspace discription",
                "ProjectName": "default",
                "InstanceTypeId": "vmp.standard.15d",
                "CreateTime": "2022-01-01T00:00:00Z",
                "OverdueReclaimTime": "2022-01-01T00:00:00Z",
                "DeleteProtectionEnabled": true,
                "PrometheusPushIntranetEndpoint": "http://push.prometheus-cn-beijing.ivolces.com/workspaces/{{workspace id}}/api/v1/push",
                "PrometheusQueryIntranetEndpoint": "http://query.prometheus-cn-beijing.ivolces.com/workspaces/{{workspace id}}",
                "PrometheusWriteIntranetEndpoint": "http://write.prometheus-cn-beijing.ivolces.com/workspaces/{{workspace id}}/api/v1/write"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes for this API. For common error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).


|HTTP status codes |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |An invalid parameter was found. For example, an invalid workspace name was included in requests. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |
