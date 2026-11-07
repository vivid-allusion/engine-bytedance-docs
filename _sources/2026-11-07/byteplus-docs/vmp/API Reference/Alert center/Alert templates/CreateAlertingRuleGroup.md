---
title: "CreateAlertingRuleGroup"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/CreateAlertingRuleGroup"
---

Create an alerting rule group.

## Request description

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide to provide you with a more stable, lower\-latency experience. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.

* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn?Action=CreateAlertingRuleGroup&Version=2021\-03\-03

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateAlertingRuleGroup&serviceCode=vmp&version=2021-03-03&groupName=)

## Request parameters

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateAlertingRuleGroup |The API name. The API name is `CreateAlertingRuleGroup`. |
|Version |String |Yes |2021\-03\-03 |The API version. The API version is `2021-03-03`. |
|Name |String |Yes |test |The name of the alert rule group.<br><br><br>* It is a string consisting of 1 to 64 characters.<br><br>* The name cannot start with a digit, a hyphen (`-`), an underscore (`_`), or other special characters.<br><br>* It can only contain uppercase and lowercase letters, Chinese characters, digits, hyphens (`-`), and underscores (`_`). |
|Description |String |No |\- |Description of alerting rule group.<br><br>It is a string that can be up to 4096 characters in length. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/88/123597#tag) |No |\- |Resource label of alerting rule group. |
|AlertingRuleTemplateId |String |Yes |421d\-\*\*\*\*\-ba4d\*\*\* |The ID of an alerting rule template.<br><br>You can call the [ListAlertingRuleTemplates](https://docs.byteplus.com/en/docs/vmp/Volcengine-Managed-Service-for-Prometheus) API to obtain the alert rule template ID. |
|AlertingRuleTemplateVersion |String |No |1.0.1 |Version of alerting rule template. Leaving it empty indicates the latest version. |
|WorkspaceId |String |Yes |421d\-\*\*\*\*\-ba4d\*\*\* |Workspace ID<br><br>You can call the [ListWorkspaces](https://docs.byteplus.com/en/docs/vmp/ListWorkspaces) API to obtain the workspace ID. |
|Items |Array of [AlertingRuleGroupItemValue](https://docs.byteplus.com/en/docs/88/123597#alertingrulegroupitemvalue) |No |\- |A list of associated alerting rules. |
|NotifyPolicyId |String |No |421dce0a\-784e\-4091\-ba4d\*\*\* |Alert notification policy ID. |
|NotifyGroupPolicyId |String |Yes |421dce0a\-784e\-4091\-ba4d\*\*\* |ID of alerting aggregation policy. |
|Variables |Array of [VariableValue](https://docs.byteplus.com/en/docs/88/123597#variablevalue) |No |\- |Variable configuration. |
|AlertingRuleTags |Array of [Tag](https://docs.byteplus.com/en/docs/88/123597#tag) |No |\- |The tag of the alert rule. |
|AlertingRuleProjectName |String |No |default |The project name. |
|NotifyGroupPolicySource |String |No |VMP |The source of the alert aggregation policy. |
|NotifyPolicySource |String |No |VMP |The source of the alert notification policy. |

### Tag

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |doc |Tag key. |
|Value |String |No |demo |Tag value. |

### AlertingRuleGroupItemValue

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Id |Long |Yes |1 |The serial number of the alert rule template item. |
|Enable |Boolean |Yes |true |Status of alerting rule. Available values:<br><br><br>* **true**: enable<br><br>* **false**: disable |
|Labels |Array of [TemplateKV](https://docs.byteplus.com/en/docs/88/123597#templatekv) |No |\- |labels in alerting notifications. |
|Levels |Array of [AlertingRuleLevel](https://docs.byteplus.com/en/docs/88/123597#alertingrulelevel) |No |\- |Alerting level. |
|Annotations |Array of [TemplateKV](https://docs.byteplus.com/en/docs/88/123597#templatekv) |No |\- |Annotations in alerting notifications. |

### VariableValue

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Id |Long |No |1 |ID of variable.<br><br>You can call the [ListAlertingRuleTemplates](https://docs.byteplus.com/en/docs/vmp/Volcengine-Managed-Service-for-Prometheus) API to obtain the variable ID in the alert template. |
|Name |String |No |Cluster |The variable name. It corresponds to the Name in AlertingRuleTemplate.Variables. It can be used to replace the ID for stable matching during upgrades or variable reordering. |
|Values |Array of String |No |demo |Default value of variable. If the value is left empty:<br><br><br>* When the parameter `IncludeAll` with value `False` is received by API `ListAlertingRuleTemplates`, it means none of the templates will be selected.<br><br>* When the parameter `IncludeAll` with value `True` is received by API `ListAlertingRuleTemplates`, it means all of the templates will be selected. |

### TemplateKV

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Name |String |Yes |key1 |Tag key. |
|Value |String |No |value1 |The value of the label. Leaving it empty means the key will be deleted correspondingly. |

### AlertingRuleLevel

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Level |String |Yes |P0 |Alerting rule level. Level P0, P1, and P2 are available currently. |
|For |String |Yes |5 minutes |Alert duration, value:<br><br><br>* **0s**: raise immediately<br><br>* **1m**: 1 minute<br><br>* **2m**: 2 minutes<br><br>* **5m**: 5 minutes<br><br>* **10m**: 10 minutes |
|Comparator |String |Yes |\> |Operators used in alert rules:<br><br><br>*  **\>** : greater than<br><br>*  **\>=** : greater than or equal to<br><br>*  **<** : less than<br><br>*  **<=** : less than or equal to<br><br>*  **==** : equal to<br><br>*  **!=** : not equal to |
|Threshold |Double |No |1.0 |Threshold of the alert rule. |

## Sample request

```JSON
POST https://vmp.cn-beijing.byteplusapi.com.cn?Action=CreateAlertingRuleGroup&Version=2021-03-03
Content-Type: application/json
{
    "Name": "test",
    "Description": "-",
    "Tags": [
        {
            "Key": "doc",
            "Value": "demo"
        }
    ],
    "AlertingRuleTemplateId": "421d-****-ba4d***",
    "AlertingRuleTemplateVersion": "1.0.1",
    "WorkspaceId": "421d-****-ba4d***",
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
            ]
        }
    ],
    "NotifyPolicyId": "421dce0a-784e-4091-ba4d***",
    "NotifyGroupPolicyId": "421dce0a-784e-4091-ba4d***",
    "Variables": [
        {
            "Id": 1,
            "Name": "Cluster",
            "Values": [
                ""
            ]
        }
    ],
    "AlertingRuleProjectName": "default",
    "AlertingRuleTags": [
        {
            "Key": "doc",
            "Value": "demo"
        }
    ],
    "NotifyGroupPolicySource": "VMP",
    "NotifyPolicySource": "VMP"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |e28a\-\*\*\*\*\-abf4\*\*\* |ID of the alert rule group. |

## Sample response

```JSON
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateAlertingRuleGroup",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "e28a-****-abf4***"
    }
}
```

## Error codes

The following table lists the error codes of the API. For public error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).

|**HTTP status codes** |**Error codes** |**Error messages** |**Description** |
|---|---|---|---|
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The current account is not subscribed to the VMP service. |
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |The input is invalid. For example, the workspace name does not meet the requirements. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |A required parameter is missing. |
