---
title: "ListDiagnosticTaskResults"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ListDiagnosticTaskResults"
---

Queries the results of a diagnostic task.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point based on the region where your business is located.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListDiagnosticTaskResults&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListDiagnosticTaskResults&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameter

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListDiagnosticTaskResults |The API name. The API name is `ListDiagnosticTaskResults`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Id |String |Yes |task\-202303\*\*\*\* |The ID of the diagnostic task.<br><br>You can call the [ListDiagnosticTask](https://docs.byteplus.com/en/docs/vke/ListDiagnosticTask?lang=en) API to obtain the diagnostic task ID. |
|Filter |Object of [DiagnoseTaskResultFilter](https://docs.byteplus.com/en/docs/90/120595#diagnosetaskresultfilter) |No |\- |The diagnostic task filter parameter. It intersects the value ranges of query parameters and returns matching results. |
|PageNumber |Long |No |1 |The starting page number for paginated queries. The value starts at 1 and defaults to 1. |
|PageSize |Long |No |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |


<span id="diagnosetaskresultfilter"></span>
### DiagnoseTaskResultFilter


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Results |Array of String |No |["Failed"] |The result of the diagnostic event. Valid values:<br><br><br>* **Succeeded**: Diagnosis passed<br><br>* **Waiting**: Diagnosis warning<br><br>* **Failed**: Diagnosis failed<br><br>* **Error**: Diagnosis error |
|Rule.Names |Array of String |No |["CheckK8sControlStatus"] |The check rule names. |
|ResourceIds |Array of String |No |["ccbm7\*\*\*\*", "ccdhm\*\*\*\*"] |The resource IDs that correspond to the diagnostic task. |
|ResourceTypes |Array of String |No |["VkeCluster"] |The resource types that correspond to the diagnostic task. Valid values:<br><br><br>* **VkeCluster**: Cluster<br><br>* **VkeNodePool**: Node pool<br><br>* **VkeNode**: Node<br><br>* **VkeAddon**: Add\-on<br><br>* **VkePod**: Pod |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=ListDiagnosticTaskResults&Version=2022-05-12
Content-Type: application/json
{
    "Id": "task-20********",
    "Filter": {
        "Results": [
            "Failed"
        ],
        "Rule.Names": [
            "CheckK8sControlStatus"
        ],
        "ResourceIds": [
            "ccbm7****",
            "ccdhm****"
        ],
        "ResourceTypes": [
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
|Items |Array of [DiagnoseTaskResult](https://docs.byteplus.com/en/docs/90/120595#diagnosetaskresult) |10 |Task details. |
|PageNumber |Long |1 |The current page number. |
|PageSize |Long |10 |Number of tasks displayed per page. |
|TotalCount |Long |178 |The total number of data entries that match the query conditions. |


<span id="diagnosetaskresult"></span>
### DiagnoseTaskResult


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Rule |Object of [DiagnoseRule](https://docs.byteplus.com/en/docs/90/120595#diagnoserule) |\- |The diagnostic rule information. |
|Reason |String |The Kube\-apiserver is in the Down state |The diagnostic analysis result. |
|Result |String |Failed |The result of the diagnostic event. Valid values:<br><br><br>* **Succeeded**: Diagnosis passed<br><br>* **Waiting**: Diagnosis warning<br><br>* **Failed**: Diagnosis failed<br><br>* **Error**: Diagnosis error |
|Affection |String |This status causes API request errors. |The description of the affected scope when the diagnosis fails. |
|ResourceId |String |ccbm7\*\*\*\* |The resource ID. |
|Suggestion |String |Restart the Pod to resolve the issue. |The fixing suggestion when the diagnosis fails. |
|ErrorMessage |String |\- |The error details when the diagnostic task fails. |
|ResourceType |String |VKECluster |The resource type. Valid values:<br><br><br>* **VkeCluster**: Cluster<br><br>* **VkeNodePool**: Node pool<br><br>* **VkeNode**: Node<br><br>* **VkeAddon**: Add\-on<br><br>* **VkePod**: Pod |
|TaskResultDetails |Array of [DiagnoseTaskSubResult](https://docs.byteplus.com/en/docs/90/120595#diagnosetasksubresult) |\- |The detailed result of the diagnostic event. |


<span id="diagnoserule"></span>
### DiagnoseRule


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Name |String |vkepod\-podload\-pod\-cpu\-usage |The name of the diagnostic rule. |
|Group |String |Pod diagnosis |The rule group information. |
|SubGroup |String |Container load |The secondary rule group information. |
|Description |String |Pod CPU utilization |The rule description. |


<span id="diagnosetasksubresult"></span>
### DiagnoseTaskSubResult


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Result |String |Succeeded |The result of the diagnostic event. Valid values:<br><br><br>* **Succeeded**: Diagnosis passed<br><br>* **Waiting**: Diagnosis warning<br><br>* **Failed**: Diagnosis failed<br><br>* **Error**: Diagnosis error |
|IsSilenced |Boolean |true |Whether it is silenced. Valid values:<br><br><br>* **true**: Yes<br><br>* **false**: No |
|ResourceId |String |ccbm7\*\*\*\* |The resource ID. |
|ResourceType |String |VKECluster |The resource type. Valid values:<br><br><br>* **VkeCluster**: Cluster<br><br>* **VkeNodePool**: Node pool<br><br>* **VkeNode**: Node<br><br>* **VkeAddon**: Add\-on<br><br>* **VkePod**: Pod |
|ResourceLabels |Array of String |["k8s\-app=kube\-apiserver"] |The resource label. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420**********",
        "Action": "ListDiagnosticTaskResults",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Items": [
            {
                "Rule": {
                    "Name": "vkepod-podload-pod-cpu-usage",
                    "Group": "Pod diagnosis",
                    "SubGroup": "Container load",
                    "Description": "Pod CPU utilization"
                },
                "Reason": "The Kube-apiserver is in the Down state",
                "Result": "Failed",
                "Affection": "This status causes API request errors",
                "ResourceId": "ccbm*****",
                "Suggestion": "Restart the Pod to resolve the issue",
                "ErrorMessage": "-",
                "ResourceType": "VKECluster",
                "TaskResultDetails": [
                    {
                        "Result": "Succeeded",
                        "IsSilenced": true,
                        "ResourceId": "ccbm*****",
                        "ResourceType": "VKECluster",
                        "ResourceLabels": [
                            "k8s-app=kube-apiserver"
                        ]
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
