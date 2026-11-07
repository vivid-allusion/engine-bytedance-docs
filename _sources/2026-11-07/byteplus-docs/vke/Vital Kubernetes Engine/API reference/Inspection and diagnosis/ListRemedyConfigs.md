---
title: "ListRemedyConfigs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/listremedyconfigs"
---

Queries self\-healing configurations.

## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. See [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) and select the most suitable endpoint for the region where your business operates.

* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListRemedyConfigs&Version=2022\-05\-12

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListRemedyConfigs&serviceCode=vke&version=2022-05-12&groupName=)

## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListRemedyConfigs |The API name. The API name is `ListRemedyConfigs`. |
|Version |String |Yes |May 12, 2022 |The API version. The current version of the API is `2022-05-12`. |
|Filter |Object of [RemedyConfigFilter](https://docs.byteplus.com/en/docs/90/124349#remedyconfigfilter) |No |\- |The self\-healing configuration. |
|PageNumber |Long |No |1 |The starting page number for paginated queries. The value starts at 1 and defaults to 1. |
|PageSize |Long |No |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |

### RemedyConfigFilter

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Ids |Array of String |No |R202609\*\*\*\*\* |The ID of the check and self\-healing rule. |
|Name |String |No |Remedy\-Node |The name of the check and self\-healing rule. |
|ClusterIds |Array of String |No |cda5\*\*\*\*\* |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. |
|ResourceIds |Array of String |No |["pc51i0\*\*\*\*\*"] |The node pool ID.<br><br>You can call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools?lang=en) API to obtain the node pool ID. |
|ResourceType |String |No |VkeNodePool |The bound resource type. Currently, only VkeNodePool is supported. |

## Sample requests

```JSON
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=ListRemedyConfigs&Version=2022-05-12
Content-Type: application/json
{
    "Filter": {
        "Ids": [
            ""
        ],
        "Name": "Remedy-Node",
        "ClusterIds": [
            ""
        ],
        "ResourceIds": [
            "pc51i0*****"
        ],
        "ResourceType": null
    },
    "PageNumber": 1,
    "PageSize": 10
}
```

## Response parameter

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Items |Array of [RemedyConfigResult](https://docs.byteplus.com/en/docs/90/124349#remedyconfigresult) |\- |The self\-healing configuration list. |
|PageNumber |Long |1 |The current page number. |
|PageSize |Long |10 |Number of tasks displayed per page. |
|TotalCount |Long |178 |The total number of data entries that match the query conditions. |

### RemedyConfigResult

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |R2026\*\*\*\*\*\* |The ID of the check and self\-healing rule. |
|Name |String |Remedy\-Node |The name of the check and self\-healing rule. |
|Rules |Array of [RemedyRule](https://docs.byteplus.com/en/docs/90/124349#remedyrule) |\- |The check and self\-healing rule. |
|ClusterId |String |ccbm7\*\*\*\* |Cluster ID. |
|CreateTime |String |2021\-01\-01T00:00:00Z |The creation time.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|UpdateTime |String |2021\-01\-01T00:00:00Z |Update time.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|ClientToken |String |BC028527\-33B9\-4990\-A633\-84E9F9xxxx |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |
|ResourceIds |Array of String |["pc51i0\*\*\*\*\*"] |The resource object ID list. |
|ResourceType |Integer |VkeNodePool |The bound resource type. Currently, only VkeNodePool is supported. |

### RemedyRule

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|FaultType |String |NodeFault |The failure type. Valid values:<br><br><br>* **GPUFault:**  GPU failure<br><br>* **NodeFault:**  Node failure<br><br>* **SystemFault:**  System and add\-on failure<br><br>* **RegisteredFault:**  Custom failure<br><br>* **XidFault:**  XID exception |
|IncidentTypes |Array of String |["NodeNotReady","NodeFailure"] |The self\-healing check item. Different types of failures support different check items. You need to fill in the Kubernetes event here. For details, see [Check and self-healing overview](https://docs.byteplus.com/en/docs/vke/Check_and_self-healing_overview). |
|RemedyStrategy |Object of [RemedyStrategy](https://docs.byteplus.com/en/docs/90/124349#remedystrategy) |\- |The check and self\-healing policy. |

### RemedyStrategy

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Type |String |Remedy |The policy type. Valid values:<br><br><br>* **Notify**: Prompt for exception<br><br>* **CordonNode**: Cordon nodes<br><br>* **DrainNode**: Drain nodes<br><br>* **Remedy**: Self\-healing<br><br><br>> Description<br><br><br><br>* > This parameter can be set to `Remedy` only if `RemedyRule.FaultType` is set to `RegisteredFault`.<br><br><br>* > This parameter can be set to `DrainNode` or `Remedy` only if `RemedyRule.FaultType` is set to `XidFault`.<br> |
|Config |Object of [StrategyConfig](https://docs.byteplus.com/en/docs/90/124349#strategyconfig) |\- |The self\-healing policy configuration. |

### StrategyConfig

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Drain |Object of [DrainConfig](https://docs.byteplus.com/en/docs/90/124349#drainconfig) |\- |The drain configuration. |
|Action |Object of [RemedyAction](https://docs.byteplus.com/en/docs/90/124349#remedyaction) |\- |The self\-healing operation. |
|IaasEvents |Array of String |["SystemMaintenance_Redeploy"] |IaaS event filtering. Valid values:<br><br><br>* **SystemMaintenance_Redeploy**: Instance redeployed due to system maintenance.<br><br>* **InfrastructureUpgrade_Redeploy**: Instance redeployed due to infrastructure upgrade.<br><br>* **SystemFailure_Redeploy**: Instance redeployed due to system failure.<br><br>* **DiskErrorDetected**: Disk error.<br><br>* **SystemMaintenance_StopAndRepair**: Instance stopped due to system maintenance. |
|InterveneDrain |Object of [RemedyIntervention](https://docs.byteplus.com/en/docs/90/124349#remedyintervention) |\- |Intervention drain. |
|InterveneCordon |Object of [RemedyIntervention](https://docs.byteplus.com/en/docs/90/124349#remedyintervention) |\- |Intervention cordon. |
|AutoRestoreSchedule |Boolean |true |Whether to enable self\-healing restoration. Valid values:<br><br><br>* **true**: Enabled.<br><br>* **false**: Disabled. |

### DrainConfig

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|WaitFor |Integer |10800 |The wait time before draining. Unit: seconds. |

### RemedyAction

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|WaitFor |Integer |10800 |The wait time before self\-healing. Unit: seconds. |
|RebootEcs |Boolean |true |Whether to restart ECS. Valid values:<br><br><br>* **true**: Restart.<br><br>* **false**: Do not restart. |

### RemedyIntervention

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Label |Object of [InterventionLabel](https://docs.byteplus.com/en/docs/90/124349#interventionlabel) |\- |Intervention label. |
|Enabled |Boolean |true |Whether to enable intervention. Valid values:<br><br><br>* **true**: Enabled.<br><br>* **false**: Disabled. |

### InterventionLabel

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |example\-key |The tag key. Length limit: 1\-256 characters. |
|Value |String |example\-value |The label value. Length limit: 0 to 256 characters. |

## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListRemedyConfigs",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Items": [
            {
                "Id": "R2026******",
                "Name": "Remedy-Node",
                "Rules": [
                    {
                        "FaultType": "NodeFault",
                        "IncidentTypes": [
                            "NodeNotReady",
                            "NodeFailure"
                        ],
                        "RemedyStrategy": {
                            "Type": "Remedy",
                            "Config": {
                                "Drain": {
                                    "WaitFor": 10800
                                },
                                "Action": {
                                    "WaitFor": 10800,
                                    "RebootEcs": true
                                },
                                "IaasEvents": [
                                    "SystemMaintenance_Redeploy"
                                ],
                                "InterveneDrain": {
                                    "Label": {
                                        "Key": "example-key",
                                        "Value": "example-value"
                                    },
                                    "Enabled": true
                                },
                                "InterveneCordon": {
                                    "Label": {
                                        "Key": "example-key",
                                        "Value": "example-value"
                                    },
                                    "Enabled": true
                                },
                                "AutoRestoreSchedule": true
                            }
                        }
                    }
                ],
                "ClusterId": "ccbm7****",
                "CreateTime": "2021-01-01T00:00:00Z",
                "UpdateTime": "2021-01-01T00:00:00Z",
                "ClientToken": "BC028527-33B9-4990-A633-84E9F9xxxx",
                "ResourceIds": [
                    "pc51i0*****"
                ],
                "ResourceType": null
            }
        ],
        "PageNumber": 1,
        "PageSize": 10,
        "TotalCount": 178
    }
}
```

## Error code

This API has no API\-specific error codes. For details about common error codes, see [Common error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes).
