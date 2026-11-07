---
title: "UpdateAlertingRuleTemplate"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/UpdateAlertingRuleTemplate"
---

Updates an alert template.

## Request description

* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn?Action=UpdateAlertingRuleTemplate&Version=2021\-03\-03

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpdateAlertingRuleTemplate&serviceCode=vmp&version=2021-03-03&groupName=)

## Request parameters

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdateAlertingRuleTemplate |The API name. The API name is `UpdateAlertingRuleTemplate`. |
|Version |String |Yes |2021\-03\-03 |The API version. The API version is `2021-03-03`. |
|Id |String |Yes |e28a\-\*\*\*\*\-8808\*\*\*\* |Alert template ID. |
|Name |String |No |test |The name of an alert rule template. |
|Description |String |No |\- |The description. |
|Items |Array of [AlertingRuleTemplateItem](https://docs.byteplus.com/en/docs/88/123602#alertingruletemplateitem) |No |\- |The alert rule list. |
|Variables |Array of [VariableWithoutId](https://docs.byteplus.com/en/docs/88/123602#variablewithoutid) |No |\- |The variable list. |
|Labels |Array of [TemplateKV](https://docs.byteplus.com/en/docs/88/123602#templatekv) |No |\- |The global labels of alert rule templates. They can be attached to alerts and have a higher priority than those configured for an individual rule in templates. |

### AlertingRuleTemplateItem

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Id |Long |No |1 |The serial number of the alert rule template item. |
|Name |String |Yes |test5 |The names of items in alert rule templates. |
|Labels |Array of [TemplateKV](https://docs.byteplus.com/en/docs/88/123602#templatekv) |No |\- |The labels attached to alert rules. |
|Levels |Array of [AlertingRuleLevel](https://docs.byteplus.com/en/docs/88/123602#alertingrulelevel) |No |\- |The alert level. |
|PromQL |String |Yes |my_metrics{cluster=~"$Cluster"} |PromQL statements based on alert rules. |
|Annotations |Array of [TemplateKV](https://docs.byteplus.com/en/docs/88/123602#templatekv) |No |\- |The annotations attached to alert rules. |
|Description |String |No |\- |The description of an alert rule. |

### VariableWithoutId

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Name |String |Yes |Cluster |The variable name, which is used in PromQL. |
|Type |String |Yes |Query |The variable type. Valid values: Query and Custom. Query indicates that values are obtained through PromQL queries. Custom indicates that values are taken from Values. |
|Alias |String |No |Cluster |The variable alias, which is displayed in the variable selector. |
|Multi |Boolean |Yes |true |Whether multiple values can be selected. Values:<br><br><br>* **true**: Supported.<br><br>* **false**: Not supported. |
|Query |String |Yes |kube_pod_info |The variable value query statement. It is only applicable to Query\-type variables. |
|Regex |String |No |/.*pod="(.* ?)".\* |The regular expression for extracting variable values. It is only applicable to Query\-type variables. |
|Values |Array of String |No |\- |The list of fixed variable values. It is only applicable to Custom\-type variables. |
|Default |Array of String |No |\- |The default value of the variable.<br><br>> **tip**<br><br><br>> When it is left empty:<br><br><br>> If `IncludeAll` is set to `False`, it indicates that none are selected. If `IncludeAll` is set to `True`, it indicates that all are selected.<br> |
|IncludeAll |Boolean |Yes |true |Whether all values can be selected.<br><br><br>* **true**: Supported.<br><br>* **false**: Not supported. |

### TemplateKV

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Name |String |Yes |key1 |The label key. |
|Value |String |No |value1 |The label value. If this parameter is left empty, it indicates that the key will be deleted. |

### AlertingRuleLevel

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Level |String |Yes |P0 |The alert rule level. Level P0, P1, and P2 are available. |
|For |String |Yes |5 minutes |Alert duration, value:<br><br><br>* **0s**: raise immediately<br><br>* **1m**: 1 minute<br><br>* **2m**: 2 minutes<br><br>* **5m**: 5 minutes<br><br>* **10m**: 10 minutes |
|Comparator |String |Yes |\> |Operators used in alert rules:<br><br><br>*  **\>** : greater than<br><br>*  **\>=** : greater than or equal to<br><br>*  **<** : less than<br><br>*  **<=** : less than or equal to<br><br>*  **==** : equal to<br><br>*  **!=** : not equal to |
|Threshold |Double |No |1.0 |Threshold of the alert rule. |

## Sample request

```JSON
POST https://vmp.cn-beijing.byteplusapi.com.cn?Action=UpdateAlertingRuleTemplate&Version=2021-03-03
Content-Type: application/json
{
    "Id": "e28a-****-8808****",
    "Name": "test",
    "Description": "-",
    "Items": [
        {
            "Id": 1,
            "Name": "test5",
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
            "PromQL": "my_metrics{cluster=~\"$Cluster\"}",
            "Annotations": [
                {
                    "Name": "key1",
                    "Value": "value1"
                }
            ],
            "Description": "-"
        }
    ],
    "Variables": [
        {
            "Name": "Cluster",
            "Type": "Query",
            "Alias": "Cluster",
            "Multi": true,
            "Query": "kube_pod_info",
            "Regex": "/.*pod=\\\"(.*?)\\\".*",
            "Values": [
                ""
            ],
            "Default": [
                ""
            ],
            "IncludeAll": true
        }
    ],
    "Labels": [
        {
            "Name": "key1",
            "Value": "value1"
        }
    ]
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |e28a\-\*\*\*\*\-808c\*\*\*\* |Alert template ID. |

## Sample response

```JSON
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateAlertingRuleTemplate",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "e28a-****-808c****"
    }
}
```

## Error codes

The following table lists the error codes of the API. For common error codes, see [Common error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).

|**HTTP status codes** |**Error codes** |**Error messages** |**Description** |
|---|---|---|---|
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The current account is not subscribed to the VMP service. |
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |The input is invalid. For example, the workspace name does not meet the requirements. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |A required parameter is missing. |
