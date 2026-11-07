---
title: "ListAddons"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ListAddons"
---

Query the details of installed add\-ons that meet the criteria.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListAddons&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListAddons&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table contains the request parameters for the API. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListAddons |The API name. The name of the current API is `ListAddons`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Filter |Object of [ListAddonsFilter](https://docs.byteplus.com/en/docs/vke/ListAddons#listaddonsfilter) |no |\- |Filters for the add\-ons to be queried. |
|PageNumber |Integer |no |1 |The starting page number when querying. The default number is 1. |
|PageSize |Integer |no |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |


<span id="listaddonsfilter"></span>
### ListAddonsFilter


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|ClusterIds |Array of String |no |["cc5silumrsfeq\*\*\*\*"] |A list of cluster IDs.<br><br>Cluster IDs can be fetched by calling [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API. Up to 100 cluster IDs can be included in a single query.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If this parameter is an empty array, filtering is performed based on all clusters in the specified region within the account.</div><br> |
|Names |Array of String |no |["ingress\-nginx"] |A list of add\-on names.<br><br>You can call the [ListSupportedAddons](https://docs.byteplus.com/en/docs/vke/ListSupportedAddons) API to obtain the cluster add\-on names. A maximum of 100 add\-on names can be specified in a single request.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If this parameter is an empty array, filtering will be performed on all add\-ons in the specified cluster.</div><br> |
|DeployModes |Array of String |no |["Unmanaged"] |Supported deployment modes. Values:<br><br><br>* **Unmanaged**: Query add\-ons deployed in unmanaged mode.<br><br>* **Managed**: Query add\-ons deployed in managed mode.<br><br>* An empty value indicates that add\-ons with all supported deployment modes are returned. |
|DeployNodeTypes |Array of String |no |["VirtualNode"] |Deployment node type. This parameter is required only when `DeployMode` is set to Unmanaged. Valid values:<br><br><br>* **Node**: Obtain add\-ons with node (ECS) as their deployment node type.<br><br>* **VirtualNode**: Obtain add\-ons with virtual node (VCI) as their deployment node type.<br><br>* An empty value indicates that add\-ons with all supported deployment node types are returned. |
|Statuses |Array of [AddonStatusFilter](https://docs.byteplus.com/en/docs/vke/ListAddons#addonstatusfilter) |no |[{"Phase":"Running","Conditions.Type":"Ok"}] |Add\-on status.<br><br>Up to 15 array elements can be provided at a time. The logic OR is applied to represent relations among multiple statuses. |
|CreateClientToken |String |no |ed6b1190\-dc17\-11ec\-9519\-eb58a7\*\*\*\*\*\* |The ClientToken generated upon successful creation. The ClientToken is a string that ensures request idempotency. This string is provided by the caller. |
|UpdateClientToken |String |no |BC028527\-33B9\-4990\-A633\-54A859\*\*\*\*\*\* |Filter by update idempotency token for precise querying.<br><br>The ClientToken generated for the last successful update. The ClientToken is a string that ensures request idempotency. This string is provided by the caller. |


<span id="addonstatusfilter"></span>
### AddonStatusFilter


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Phase |String |no |Running |Add\-on status. Values:<br><br><br>* **Running**<br><br>* **Failed**<br><br>* **Creating**<br><br>* **Deleting**<br><br>* **Updating**<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">At least one of <strong>Phase</strong> and <strong>Conditions.Type</strong> must be provided. Otherwise, it is an invalid array element. For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resources status description</a>.</div><br> |
|Conditions.Type |String |no |Ok |The condition under which the add\-on enters the primary status. You can specify multiple conditions. Valid values:<br><br><br>* **Unknown**<br><br>* **ClusterNotRunning**<br><br>* **CrashLoopBackOff**<br><br>* **ImagePullBackOff**<br><br>* **SchedulingFailed**<br><br>* **NameConflict**<br><br>* **ResourceCleanupFailed**<br><br>* **ClusterVersionUpgrading**<br><br>* **Ok**<br><br>* **Degraded**<br><br>* **Progressing**<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">At least one of <strong>Phase</strong> and <strong>Conditions.Type</strong> must be provided. Otherwise, it is an invalid array element. For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resources status description</a>.</div><br> |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST /?Action=ListAddons&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "Filter": {
        "ClusterIds": ["cc5silumrsf******"],
        "Names": ["ingress-nginx"],
        "DeployModes": ["Unmanaged"],
        "DeployNodeTypes": ["VirtualNode"],
        "Statuses": [{
            "Phase": "Running",
            "Conditions.Type": "Ok"
        }],
        "CreateClientToken": "ed6b1190-dc17-11ec-9519-eb58a7******",
        "UpdateClientToken": "BC028527-33B9-4990-A633-54A859******"
    },
    "PageNumber": 1,
    "PageSize": 10
}

```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Items |Array of [Addon](https://docs.byteplus.com/en/docs/vke/ListAddons#addon) |\- |A list of add\-ons. |
|PageNumber |Integer |1 |The current page number. |
|PageSize |Integer |10 |The number of add\-ons displayed per page. |
|TotalCount |Integer |100 |Total number of items in the returned data list. |


<span id="addon"></span>
### Add\-on


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|ClusterId |String |cc5sil\*\*\*\* |The ID of the cluster where the add\-on belongs. |
|Name |String |ingress\-nginx |The name of the add\-on. |
|Version |String |v0.44.0 |The version of the add\-on. |
|DeployMode |String |Unmanaged |The add\-on deployment mode. Values:<br><br><br>* **Unmanaged**: Deployed in unmanaged mode.<br><br>* **Managed**: Deployed in managed mode. |
|DeployNodeType |String |VirtualNode |Deployment node type. Values:<br><br><br>* **Node**: Deployed using the node type.<br><br>* **VirtualNode**: Deployed using the virtual node type.<br><br>   This parameter is returned only when `DeployMode` is set to `Unmanaged`. |
|Config |String | |Add\-on configuration. For parameter details, see [Add-on configuration information](https://docs.byteplus.com/en/docs/vke/CreateAddon#.57uE5Lu26YWN572u5L-h5oGv). |
|CreateTime |String |2021\-10\-27T10:33:30Z |The time when the add\-on was installed.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|UpdateTime |String |2021\-10\-29T10:33:30Z |The time when the add\-on was updated.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|Status |Object of [AddonStatus](https://docs.byteplus.com/en/docs/vke/ListAddons#addonstatus) | |Add\-on status. |
|CreateClientToken |String |ed6b1190\-dc17\-11ec\-9519\-eb58a7\*\*\*\*\*\* |The ClientToken generated upon successful creation. |
|UpdateClientToken |String |BC028527\-33B9\-4990\-A633\-54A859\*\*\*\*\*\* |The ClientToken generated for the last successful update. |


<span id="addonstatus"></span>
### AddonStatus


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Phase |String |Running |Add\-on status. Values:<br><br><br>* **Running**<br><br>* **Failed**<br><br>* **Creating**<br><br>* **Deleting**<br><br>* **Updating**<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resources status description</a>.</div><br> |
|Conditions |Array of [AddonCondition](https://docs.byteplus.com/en/docs/vke/ListAddons#addoncondition) |["Type":"Ok"] |Conditions under which the add\-on enters the primary status.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resources status description</a>.</div><br> |


<span id="addoncondition"></span>
### AddonCondition


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Type |String |Ok |The condition under which the add\-on enters the primary status. You can specify multiple conditions. Valid values:<br><br><br>* **Progressing**<br><br>* **ClusterVersionUpgrading**<br><br>* **Unknown**<br><br>* **Degraded**<br><br>* **NameConflict**<br><br>* **ClusterNotRunning**<br><br>* **CrashLoopBackOff**<br><br>* **SchedulingFailed**<br><br>* **ResourceCleanupFailed** |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type:application/json
{
    "ResponseMetadata": {
        "RequestId": "202***",
        "Action": "ListAddons",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Items": [
            {
                "ClusterId": "cc**",
                "Name": "ingress-nginx",
                "Version": "v1.3.1-vke.5",
                "DeployMode": "Unmanaged",
                "DeployNodeType": "Node",
                "Config": "{\"Replica\":1,\"Resource\":{\"Request\":{\"Cpu\":\"0.25\",\"Memory\":\"512Mi\"},\"Limit\":{\"Cpu\":\"0.5\",\"Memory\":\"1024Mi\"}},\"PrivateNetwork\":{\"SubnetId\":\"subnet-2d61qn69iji****\",\"IpVersion\":\"IPV4\"}}",
                "CreateTime": "2022-10-31 07:45:16.19943 +0000 UTC",
                "UpdateTime": "2023-04-25 01:50:16.68753 +0000 UTC",
                "Status": {
                    "Phase": "Running",
                    "Conditions": [
                        {
                            "Type": "Ok"
                        }
                    ]
                },
                "CreateClientToken": "",
                "UpdateClientToken": "",
                "ClusterType": ""
            }
        ],
        "PageNumber": 1,
        "PageSize": 10,
        "TotalCount": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no proprietary error codes for this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details.

&nbsp;
