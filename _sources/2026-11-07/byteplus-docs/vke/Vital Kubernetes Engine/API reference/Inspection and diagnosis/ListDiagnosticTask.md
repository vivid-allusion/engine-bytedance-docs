---
title: "ListDiagnosticTask"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ListDiagnosticTask"
---

Queries the list of diagnostic, inspection, or check tasks.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point based on the region where your business is located.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListDiagnosticTask&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListDiagnosticTask&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameter

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListDiagnosticTask |The API name. The API name is `ListDiagnosticTask`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Filter |Object of [DiagnoseTaskFilter](https://docs.byteplus.com/en/docs/90/120594#diagnosetaskfilter) |No |\- |The diagnostic task filter. It takes the intersection of the value ranges of all query parameters and returns the matching results. |
|PageNumber |Long |No |1 |The starting page number of the pagination query, starting from 1. Default value: 1. |
|PageSize |Long |No |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |


<span id="diagnosetaskfilter"></span>
### DiagnoseTaskFilter


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Ids |Array of String |No |["task\-202303\*\*\*\*", "task\-202204\*\*\*\*"] |The diagnostic task IDs. |
|Types |Array of String |No |["PrecheckControlPlane", "PrecheckDataPlane"] |The diagnostic task types. Valid values:<br><br><br>* **PrecheckControlPlane**: Control plane upgrade precheck<br><br>* **PrecheckDataPlane**: Data plane upgrade precheck<br><br>* **AddonPreCheck**: Add\-on pre\-check<br><br>* **AddonPostCheck**: Add\-on post\-check<br><br>* **AddonDiagnosis**: Add\-on inspection<br><br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter can be set to <code>AddonDiagnosis</code> only if the add\-on is <code>alb-ingress-controller</code><strong>.</strong></div><br><br><br><br>* **ClusterInspection**: Cluster inspection<br><br>* **NodePoolDiagnosis**: Node pool diagnosis<br><br>* **NodeDiagnosis**: Node diagnosis<br><br>* **PodDiagnosis**: Pod diagnosis<br><br>* **NodePoolScalingDiagnosis**: Node pool scaling diagnosis<br><br>* **PathAnalysis**: Path analysis |
|Params |Array of [DiagnoseTaskParamFilter](https://docs.byteplus.com/en/docs/90/120594#diagnosetaskparamfilter) |No |\- |Custom parameters. Keys in the list must be unique. |
|EndTime |String |No |2023\-03\-04T00:00:01Z |The end time when the diagnostic task was created.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|Statuses |Array of String |No |["Waiting", "Running", "Succeeded", "Warning", "Failed"] |The list of diagnostic task statuses. Valid values:<br><br><br>* **Waiting**: The task is waiting to be executed.<br><br>* **Running**: The task is in progress.<br><br>* **Succeeded**: The task is executed.<br><br>* **Warning**: The task is in the Warning state.<br><br>* **Failed**: The task execution failed. |
|StartTime |String |No |2023\-03\-03T00:00:01Z |The start time when the diagnostic task was created.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|TargetResources.ResourceIds |Array of String |No |["ccbm7\*\*\*\*", "ccdhm\*\*\*\*"] |The resource IDs that correspond to the diagnostic task. |
|TargetResources.ResourceTypes |Array of String |No |["VkeCluster"] |The resource types that correspond to the diagnostic task. Valid values:<br><br><br>* **VkeCluster**: cluster<br><br>* **VkeNodePool**: node pool<br><br>* **VkeNode**: node<br><br>* **VkeAddon**: add\-on<br><br>* **VkePod**: Pod |


<span id="diagnosetaskparamfilter"></span>
### DiagnoseTaskParamFilter


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |TargetKubernetesVersion |The key of the diagnostic task parameter. When `DiagnoseTaskFilter.Tpyes` is configured with different parameters, the available `Key` and `Value` differ. For details, see [CreateDiagnosticTask](https://docs.byteplus.com/en/docs/vke/CreateDiagnosticTask?lang=en#diagnosetaskparam). |
|Values |Array of String |Yes |v1.36.4‑vke.2 |The value of the diagnostic task parameter. When `DiagnoseTaskFilter.Tpyes` is configured with different parameters, the available `Key` and `Value` differ. For details, see [CreateDiagnosticTask](https://docs.byteplus.com/en/docs/vke/CreateDiagnosticTask?lang=en#diagnosetaskparam). |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=ListDiagnosticTask&Version=2022-05-12
Content-Type: application/json
{
    "Filter": {
        "Ids": [
            "task-202303****",
            "task-202204****"
        ],
        "Types": [
            "PrecheckControlPlane",
            "PrecheckDataPlane"
        ],
        "Params": [
            {
                "Key": "TargetKubernetesVersion",
                "Values": [
                    "v1.36.4‑vke.2"
                ]
            }
        ],
        "EndTime": "2023-03-04T00:00:01Z",
        "Statuses": [
            "Waiting",
            "Running",
            "Succeeded",
            "Warning",
            "Failed"
        ],
        "StartTime": "2023-03-03T00:00:01Z",
        "TargetResources.ResourceIds": [
            "ccbm7****",
            "ccdhm****"
        ],
        "TargetResources.ResourceTypes": [
            "VkeCluster"
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
|Items |Array of [DiagnoseTaskResponse](https://docs.byteplus.com/en/docs/90/120594#diagnosetaskresponse) |\- |Task details. |
|PageNumber |Long |1 |The current page number. |
|PageSize |Long |10 |Number of tasks displayed per page. |
|TotalCount |Long |178 |The total number of data entries that match the query conditions. |


<span id="diagnosetaskresponse"></span>
### DiagnoseTaskResponse


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |task\-202303\*\*\*\* |The ID of the diagnostic task. |
|Type |String |PrecheckControlPlane and PrecheckDataPlane |The diagnostic task type. Valid values:<br><br><br>* **PrecheckControlPlane**: Control plane upgrade precheck<br><br>* **PrecheckDataPlane**: Data plane upgrade precheck<br><br>* **AddonPreCheck**: Add\-on pre\-check<br><br>* **AddonPostCheck**: Add\-on post\-check<br><br>* **AddonDiagnosis**: Add\-on inspection<br><br>* **ClusterInspection**: Cluster inspection<br><br>* **NodePoolDiagnosis**: Node pool diagnosis<br><br>* **NodeDiagnosis**: Node diagnosis<br><br>* **PodDiagnosis**: Pod diagnosis<br><br>* **NodePoolScalingDiagnosis**: Node pool scaling diagnosis<br><br>* **PathAnalysis**: Path analysis |
|Params |Array of [DiagnoseTaskParam](https://docs.byteplus.com/en/docs/90/120594#diagnosetaskparam) |\- |The parameters of diagnostic tasks. |
|Reason |String |\- |The comprehensive inspection and diagnostic analysis result. |
|Status |Integer |Succeeded |The diagnostic type status. Valid values:<br><br><br>* **Waiting**: The task is waiting to be executed<br><br>* **Running**: The task is in progress.<br><br>* **Succeeded**: The task is executed.<br><br>* **Warning**: The task is in the Warning state.<br><br>* **Failed**: The task fails to be executed. |
|EndTime |String |2023\-03\-04T00:00:01Z |The task execution end time.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|StartTime |String |2023\-03\-03T00:00:01Z |The execution start time of the task.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|Suggestion |String |1) Readjust the Pod scheduling policy to schedule Pods to ECS instances that are running as expected. 2) Repair the ECS instance status. |Comprehensive inspection and diagnostic repair suggestions. |
|ResultSummaries |Array of [DiagnoseTaskResultSummary](https://docs.byteplus.com/en/docs/90/120594#diagnosetaskresultsummary) |\- |The execution status of diagnostic result rules. |
|TargetResources |Array of [DiagnoseResources](https://docs.byteplus.com/en/docs/90/120594#diagnoseresources) |\- |The list of target diagnostic resources. |
|ResourcesSummaries |Array of [DiagnoseTaskResourceSummary](https://docs.byteplus.com/en/docs/90/120594#diagnosetaskresourcesummary) |\- |The execution status of diagnostic resources. |


<span id="diagnosetaskparam"></span>
### DiagnoseTaskParam


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |CurrentKubernetesVersion |The key of the diagnostic task parameter. |
|Value |String |v1.34.6‑vke.8 |The value of the diagnostic task parameter. |


<span id="diagnosetaskresultsummary"></span>
### DiagnoseTaskResultSummary


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Rule |Object of [DiagnoseRule](https://docs.byteplus.com/en/docs/90/120594#diagnoserule) |\- |The diagnostic rule. |
|Count |Integer |8 |The number of diagnostic resources in this state. |
|Result |String |Succeeded |The check item status. Valid values:<br><br><br>* **Waiting**: Pending execution<br><br>* **Succeeded**: Executed<br><br>* **Failed**: Execution failed<br><br>* **Error**: Execution error |
|TargetResources |Array of [DiagnoseResources](https://docs.byteplus.com/en/docs/90/120594#diagnoseresources) |\- |The list of target diagnostic resources. |


<span id="diagnoserule"></span>
### DiagnoseRule


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Name |String |vkepod\-podload\-pod\-cpu\-usage |The name of the diagnostic rule. |
|Group |String |Pod diagnosis |The rule group information. |
|SubGroup |String |Container load |The secondary rule group information. |
|Description |String |Pod CPU utilization |The description of the rule. |


<span id="diagnoseresources"></span>
### DiagnoseResources


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ResourceIds |Array of String |["ccbm7\*\*\*\*", "ccdhm\*\*\*\*"] |The diagnostic resource IDs. |
|ResourceType |String |VkeCluster |The diagnostic resource type. Valid values:<br><br><br>* **VkeCluster**: cluster<br><br>* **VkeNodePool**: node pool<br><br>* **VkeNode**: node<br><br>* **VkeAddon**: add\-on<br><br>* **VkePod**: pod |


<span id="diagnosetaskresourcesummary"></span>
### DiagnoseTaskResourceSummary


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Count |Integer |8 |The number of diagnostic resources in this state. |
|Status |String |Succeeded |The check task status. Valid values:<br><br><br>* **Waiting**: The task is waiting to be executed<br><br>* **Running**: The task is in progress<br><br>* **Succeeded**: The task executed successfully<br><br>* **Failed**: The task execution failed |
|TargetResources |Array of [DiagnoseResources](https://docs.byteplus.com/en/docs/90/120594#diagnoseresources) |\- |The list of target diagnostic resources. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420**********",
        "Action": "ListDiagnosticTask",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Items": [
            {
                "Id": "task-20********",
                "Type": "PrecheckControlPlane、PrecheckDataPlane",
                "Params": [
                    {
                        "Key": "CurrentKubernetesVersion",
                        "Value": "1.24"
                    }
                ],
                "Reason": "-",
                "Status": null,
                "EndTime": "2023-03-04T00:00:01Z",
                "StartTime": "2023-03-03T00:00:01Z",
                "Suggestion": "1)请重调整 Pod 调度策略，将Pod调度到正常运行的ECS实例上;2)请修复ECS实例状态",
                "ResultSummaries": [
                    {
                        "Rule": {
                            "Name": "vkepod-podload-pod-cpu-usage",
                            "Group": "Pod诊断",
                            "SubGroup": "容器负载",
                            "Description": "Pod CPU 使用情况"
                        },
                        "Count": 8,
                        "Result": "Succeeded、Warning、Failed、Error",
                        "TargetResources": [
                            {
                                "ResourceIds": [
                                    "ccbm7****",
                                    "ccdhm****"
                                ],
                                "ResourceType": "VkeCluster"
                            }
                        ]
                    }
                ],
                "TargetResources": [
                    {
                        "ResourceIds": [
                            "ccbm7****",
                            "ccdhm****"
                        ],
                        "ResourceType": "VkeCluster"
                    }
                ],
                "ResourcesSummaries": [
                    {
                        "Count": 8,
                        "Status": "Succeeded",
                        "TargetResources": []
                    }
                ]
            }
        ],
        "PageNumber": 1,
        "PageSize": 10,
        "TotalCount": 178
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no proprietary error codes for this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details about public error codes.
