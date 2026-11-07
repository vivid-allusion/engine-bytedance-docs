---
title: "ListAlertingRuleGroups"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/ListAlertingRuleGroups"
---

Obtain a list of alerting rule groups.

## Request description

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide to provide you with a more stable, lower\-latency experience. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.

* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn?Action=ListAlertingRuleGroups&Version=2021\-03\-03

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListAlertingRuleGroups&serviceCode=vmp&version=2021-03-03&groupName=)

## Request parameters

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListAlertingRuleGroups |The API name. The API name is `ListAlertingRuleGroups`. |
|Version |String |Yes |2021\-03\-03 |The API version. The API version is `2021-03-03`. |
|Filter |Object of [AlertingRuleGroupFilter](https://docs.byteplus.com/en/docs/88/123600#alertingrulegroupfilter) |No |\- |Filter conditions for alerting rule groups. |
|SortBy |String |No |CreatedAt |Whether to conduct query result sorting:<br><br><br>* The value `CreatedAt` indicates the results will be sorted. <br><br>* Absence of this parameter indicates no sorting. |
|SortOrder |String |No |Asc |Sorting order of query results:<br><br><br>* **Asc**: indicates ascending order sorting.<br><br>* **Desc**: indicates sorting in descending order. |
|PageNumber |Long |No |1 |Current page number. The minimum and default values are both 1. |
|PageSize |Long |No |10 |Results per page:<br><br><br>* The value ranges from 0 to 100.<br><br>* Default value is 10. |

### AlertingRuleGroupFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Ids |Array of String |No |["e28a\-\*\*\*\*\-abf4\*\*\*\*"] |Exact query by the IDs of alerting rule groups. |
|Name |String |No |test |Filter by names of alerting rule groups. |
|WorkspaceIds |Array of String |No |["e28a\-\*\*\*\*\-abf4\*\*\*\*"] |Exact query by workspace IDs. |
|AlertingRuleTemplateIds |Array of String |No |["e28a\-\*\*\*\*\-abf4\*\*\*\*"] |Exact query by IDs of alerting rule templates. |

## Sample request

```JSON
POST https://vmp.cn-beijing.byteplusapi.com.cn?Action=ListAlertingRuleGroups&Version=2021-03-03
Content-Type: application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filter": {
        "Ids": [
            "e28a-****-abf4****"
        ],
        "Name": "alert-group-demo",
        "WorkspaceIds": [
            "e28a-****-abf4****"
        ],
        "AlertingRuleTemplateIds": [
            "e28a-****-abf4****"
        ]
    },
    "SortBy": "CreatedAt",
    "SortOrder": "Asc"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Total |Long |100 |Total number of resources meeting filter conditions. |
|Items |Array of [AlertingRuleGroup](https://docs.byteplus.com/en/docs/88/123600#alertingrulegroup) |\- |A list of alerting rule groups. |

### AlertingRuleGroup

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |421d\-\*\*\*\*\-ba4d\*\*\* |ID of alerting rule group. |
|Name |String |test |Name of alerting rule group. |
|Items |Array of [AlertingRuleGroupItem](https://docs.byteplus.com/en/docs/88/123600#alertingrulegroupitem) |\- |A list of associated alerting rules. |
|Variables |Array of [VariableValue](https://docs.byteplus.com/en/docs/88/123600#variablevalue) |\- |Variable configuration. |
|CreateTime |String |2020\-01\-01T00:00:00Z |The creation date of the alerting rule group. |
|UpdateTime |String |2020\-01\-01T00:00:00Z |The update date of the alerting rule group. |
|Description |String |\- |Description of alerting rule group. |
|WorkspaceId |String |421d\-\*\*\*\*\-ba4d\*\*\*\* |Workspace ID |
|NotifyPolicyId |String |421d\-\*\*\*\*\-ba4d\*\*\*\* |Alert notification policy ID. |
|NotifyPolicySource |String |VMP |The source of the alert notification policy. |
|NotifyGroupPolicyId |String |421d\-\*\*\*\*\-ba4d\*\*\*\* |Alert aggregation policy ID. |
|AlertingRuleTemplateId |String |421d\-\*\*\*\*\-ba4d\*\*\*\* |Associated Alarm Template ID. |
|NotifyGroupPolicySource |String |VMP |The source of the alert aggregation policy. |
|AlertingRuleTemplateVersion |String |1.0.1 |Version of associated alarm template. |

### AlertingRuleGroupItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |Long |1 |The serial number of the alert rule template item. |
|Enable |Boolean |true |Status of alerting rule. Available values:<br><br><br>* **true**: enable<br><br>* **false**: disable |
|Labels |Array of [TemplateKV](https://docs.byteplus.com/en/docs/88/123600#templatekv) |\- |The labels to be added to an alert. |
|Levels |Array of [AlertingRuleLevel](https://docs.byteplus.com/en/docs/88/123600#alertingrulelevel) |\- |Alerting condition. |
|Annotations |Array of [TemplateKV](https://docs.byteplus.com/en/docs/88/123600#templatekv) |\- |Comments added to an alert. |
|AlertingRuleId |String |421d\-\*\*\*\*\-4d0b |Alerting rule ID. |

### VariableValue

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |Long |1 |ID of variable.<br><br>You can call the [ListAlertingRuleTemplates](https://docs.byteplus.com/en/docs/vmp/Volcengine-Managed-Service-for-Prometheus) API to obtain the variable ID in the alert template. |
|Name |String |Cluster |The variable name. It corresponds to the Name in AlertingRuleTemplate.Variables. It can be used to replace the ID for stable matching during upgrades or variable reordering. |
|Values |Array of String |demo |Default value of variable. If the value is left empty:<br><br><br>* When the parameter `IncludeAll` with value `False` is received by API `ListAlertingRuleTemplates`, it means none of the templates will be selected.<br><br>* When the parameter `IncludeAll` with value `True` is received by API `ListAlertingRuleTemplates`, it means all of the templates will be selected. |

### TemplateKV

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Name |String |key1 |Key of tag. |
|Value |String |value1 |The value of the label. Leaving it empty means the key will be deleted correspondingly. |

### AlertingRuleLevel

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Level |String |P0 |Alerting rule level. Level P0, P1, and P2 are available currently. |
|For |String |5 minutes |Alert duration, value:<br><br><br>* **0s**: raise immediately<br><br>* **1m**: 1 minute<br><br>* **2m**: 2 minutes<br><br>* **5m**: 5 minutes<br><br>* **10m**: 10 minutes |
|Comparator |String |\> |Operators used in alert rules:<br><br><br>*  **\>** : Greater than<br><br>*  **\>=** : greater than or equal to<br><br>*  **<** : Less than<br><br>*  **<=** : less than or equal to<br><br>*  **==** : equal to<br><br>*  **!=** : not equal to |
|Threshold |Double |1.0 |Threshold of the alert rule. |

## Sample response

```JSON
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListAlertingRuleGroups",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 100,
        "Items": [
            {
                "Id": "421d-****-ba4d***",
                "Name": "test",
                "Items": [
                    {
                        "Id": 1,
                        "Enable": true,
                        "Labels": [
                            {
                                "Name": "key1",
                                "Value": "value1"
                            }
                        ],
                        "Levels": [
                            {
                                "For": "5m",
                                "Level": "P0",
                                "Threshold": 1,
                                "Comparator": "\\>"
                            }
                        ],
                        "Annotations": [
                            {
                                "Name": "key1",
                                "Value": "value1"
                            }
                        ],
                        "AlertingRuleId": "421d-****-4d0b"
                    }
                ],
                "Variables": [
                    {
                        "Id": 1,
                        "Name": "Cluster",
                        "Values": [
                            ""
                        ]
                    }
                ],
                "CreateTime": "2020-01-01T00:00:00Z",
                "UpdateTime": "2020-01-01T00:00:00Z",
                "Description": "-",
                "WorkspaceId": "421dce0a-784e-4091-ba4d-6037e43a266a",
                "NotifyPolicyId": "421dce0a-784e-4091-ba4d-6037e43a266a",
                "NotifyPolicySource": "VMP",
                "NotifyGroupPolicyId": "421dce0a-784e-4091-ba4d-6037e43a266a",
                "AlertingRuleTemplateId": "421dce0a-784e-4091-ba4d-6037e43a266a",
                "NotifyGroupPolicySource": "VMP",
                "AlertingRuleTemplateVersion": "421dce0a-784e-4091-ba4d-6037e43a266a"
            }
        ]
    }
}
```

## Error codes

The error codes for this API are listed in the table below. For a list of error codes for other APIs, see [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).

|**HTTP status codes** |**Error codes** |**Error messages** |**Description** |
|---|---|---|---|
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The current account is not subscribed to the VMP service. |
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |The input is invalid. For example, the workspace name does not meet the requirements. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |A required parameter is missing. |
