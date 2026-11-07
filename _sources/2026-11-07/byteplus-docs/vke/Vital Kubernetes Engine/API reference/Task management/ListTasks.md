---
title: "ListTasks"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ListTasks"
---

Get a list of various tasks in the VKE cluster.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point based on the region where your business is located.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListTasks&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListTasks&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameter

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListTasks |The API name. The current API name is `ListTasks`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|AccountId |Long |Yes |210\*\*\*\*\*\* |BytePlus root user ID. Log in to the [BytePlus console](https://console.byteplus.com/home) and obtain the account ID on the homepage. |
|Filter |Object of [ListTasksFilter](https://docs.byteplus.com/en/docs/90/120400#listtasksfilter) |No |\- |Filter criteria for the upgrade task list to be queried. |
|PageNumber |Integer |No |1 |The starting page number of the pagination query, starting from 1. Default value: 1. |
|PageSize |Integer |No |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |


<span id="listtasksfilter"></span>
### ListTasksFilter


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Ids |Array of String |No |["taskxj\*\*\*\*\*\*"] |Task ID.<br><br>When calling [UpgradeNodePools](https://docs.byteplus.com/en/docs/vke/UpgradeNodePools) or [UpdateClusterVersion](https://docs.byteplus.com/en/docs/vke/UpdateClusterVersion), the corresponding task ID will be returned. |
|Types |Array of String |No |["PrecheckDataPlane"] |Task type. Valid values:<br><br><br>* **PrecheckDataPlane**: Data plane upgrade precheck<br><br>* **UpgradeDataPlane**: Data plane upgrade<br><br>* **PrechekControlPlane**: Control plane upgrade precheck<br><br>* **UpgradeControlPlane**: Control plane upgrade |
|Groups |Array of String |No |["Cluster"] |Task group. Valid values:<br><br><br>* **Cluster**<br><br>* **NodePool**<br><br>* **Node**: Node |
|NodeIds |Array of String |No |["n\-\*\*\*\*\*\*\*\*"] |A list of node IDs.<br><br>You can call the [ListNodes](https://docs.byteplus.com/en/docs/vke/ListNodes) API to obtain the node ID. At most 100 node IDs can be specified per call. |
|Sources |Array of String |No |["Plan"] |Task source. Valid values:<br><br><br>* **Plan**: Scheduled task<br><br>* **Task**: Instant task |
|Statuses |Array of [TaskStatusFilter](https://docs.byteplus.com/en/docs/90/120400#taskstatusfilter) |No |\- |Filter by task status. |
|ClusterIds |Array of String |No |["ccjkl\*\*\*\*\*\*"] |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. A single call can include at most 100 cluster IDs. |
|NodePoolIds |Array of String |No |["phjh\*\*\*\*\*\*"] |The node pool ID.<br><br>You can call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain node pool IDs. At most 100 node pool IDs can be specified per call. |


<span id="taskstatusfilter"></span>
### TaskStatusFilter


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Phase |String |No |Running |Task status. Values:<br><br><br>* **Running**: It is running.<br><br>* **Succeeded**: Succeeded<br><br>* **Failed**: Failed<br><br>* **Aborted**: Aborted<br><br>* **Paused**: Paused<br><br>* **Pending**: Pending<br><br>* **Approving**: Approving<br><br>* **Waiting**: Waiting to be executed |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=ListTasks&Version=2022-05-12
Content-Type: application/json
{
    "AccountId": 2**,
    "Filter": {
        "Ids": [
            "taskxj******"
        ],
        "Types": [
            "PrecheckDataPlane"
        ],
        "Groups": [
            "Cluster"
        ],
        "NodeIds": [
            "n-********"
        ],
        "Sources": [
            "Plan"
        ],
        "Statuses": [
            {
                "Phase": "Running"
            }
        ],
        "ClusterIds": [
            "ccjkl******"
        ],
        "NodePoolIds": [
            "phjh******"
        ]
    },
    "PageNumber": 1,
    "PageSize": 10
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Items |Array of [Task](https://docs.byteplus.com/en/docs/90/120400#task) |\- |Task details. |
|TotalCount |Integer |1 |Total number of tasks. |
|PageNumber |Integer |1 |The current page number. |
|PageSize |Integer |10 |Number of tasks displayed per page. |


<span id="task"></span>
### Task


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Type |String |PrecheckDataPlane |Task type. Valid values:<br><br><br>* **PrecheckDataPlane**: Data plane upgrade precheck<br><br>* **UpgradeDataPlane**: Data plane upgrade<br><br>* **PrechekControlPlane**: Control plane upgrade precheck<br><br>* **UpgradeControlPlane**: Control plane upgrade |
|Group |String |Cluster |Task group. Valid values:<br><br><br>* **Cluster**<br><br>* **NodePool**<br><br>* **Node**: Node |
|Steps |Array of [TaskStepResponse](https://docs.byteplus.com/en/docs/90/120400#taskstepresponse) |\- |Task step information. |
|Source |String |Plan |Task source. Valid values:<br><br><br>* **Plan**: Scheduled task<br><br>* **Task**: Instant task |
|Status |Object of [TaskStatusResponse](https://docs.byteplus.com/en/docs/90/120400#taskstatusresponse) |\- |Task status. |
|Target |String |metrics\-server |Change object, i.e., the resource on which the task acts. |
|TaskId |String |tcax\*\*\*\*\*\* |Task ID. |
|EndTime |String |2026\-08\-27T07:36:56Z |Task end time.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|ClusterId |String |chkjl\*\*\*\*\*\*\* |Cluster ID. |
|ExtraArgs |String |{"promoted":true} |Task extra parameters. |
|StartTime |String |2023\-10\-27T07:26:56Z |Task start time.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|Exceptions |Array of [TaskExceptionResponse](https://docs.byteplus.com/en/docs/90/120400#taskexceptionresponse) |\- |Task exception content. |
|NodePoolId |String |phj\*\*\*\*\*\* |The node pool ID. |
|Parameters |String |{"accountID":210\*\*\*\*,"clusterID":"cda7u\*\*\*\*"} |Task metadata. |
|PlanStartTime |String |2024\-10\-27T07:36:56Z |The scheduled time for executing the task.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |


<span id="taskstepresponse"></span>
### TaskStepResponse


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Type |String |UpdateNodes |Task step type. Valid values:<br><br><br>* **PrecheckControlPlane**: Control plane upgrade precheck<br><br>* **UpgradeControlPlane**: Upgrade the control plane<br><br>* **PostcheckControlPlane**: Control plane upgrade postcheck<br><br>* **PrecheckDataPlane**: Data plane upgrade precheck<br><br>* **UpgradeDataPlane**: Upgrade the data plane<br><br>* **PostcheckDataPlane**: Data plane upgrade postcheck |
|Status |String |Running |Task step status. Valid values:<br><br><br>* **Waiting**: The task is waiting to be executed<br><br>* **Running**: The task is in progress<br><br>* **Succeeded**: The task executed successfully<br><br>* **Failed**: The task execution failed |
|EndTime |String |2023\-10\-27T07:26:56Z |Task step end time.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|Message |String |precheck failed |Supplementary information for task steps. |
|StartTime |String |2023\-10\-27T07:26:56Z |Task step start time.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |


<span id="taskstatusresponse"></span>
### TaskStatusResponse


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Phase |String |Running |Task status. Valid values:<br><br><br>* **Running**: It is running.<br><br>* **Succeeded**: Succeeded<br><br>* **Failed**: Failed<br><br>* **Aborted**: Aborted<br><br>* **Paused**: Paused<br><br>* **Pending**: Pending<br><br>* **Approving**: Approving<br><br>* **Waiting**: Waiting to be executed |


<span id="taskexceptionresponse"></span>
### TaskExceptionResponse


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Message |String |Pod is still pending |Task exception information. |
|Resources |Array of [TaskResourceResponse](https://docs.byteplus.com/en/docs/90/120400#taskresourceresponse) |\- |List of abnormal resources. |


<span id="taskresourceresponse"></span>
### TaskResourceResponse


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Ids |Array of String |["nhj\*\*\*\*\*\*"] |Abnormal resource ID. |
|Type |String |Node |Abnormal resource type. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420**********",
        "Action": "ListTasks",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Items": [
            {
                "Type": "PrecheckDataPlane",
                "Group": "Cluster",
                "Steps": [
                    {
                        "Type": "UpdateNodes",
                        "Status": "Running",
                        "EndTime": "2023-10-27T07:26:56Z",
                        "Message": "precheck failed",
                        "StartTime": "2023-10-27T07:26:56Z"
                    }
                ],
                "Source": "Plan",
                "Status": {
                    "Phase": "Running"
                },
                "Target": "metrics-server",
                "TaskId": "tcax******",
                "EndTime": "2026-08-27T07:36:56Z",
                "ClusterId": "chkjl***********",
                "ExtraArgs": "{"promoted":true}",
                "StartTime": "2023-10-27T07:26:56Z",
                "Exceptions": [
                    {
                        "Message": "Pod is still pending",
                        "Resources": [
                            {
                                "Ids": [
                                    "nhj******"
                                ],
                                "Type": "Node"
                            }
                        ]
                    }
                ],
                "NodePoolId": "phj******",
                "Parameters": "{"accountID":210****,"clusterID":"cda7u****"}",
                "PlanStartTime": "2024-10-27T07:36:56Z"
            }
        ],
        "TotalCount": 1,
        "PageNumber": 1,
        "PageSize": 10
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no proprietary error codes for this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details about public error codes.
