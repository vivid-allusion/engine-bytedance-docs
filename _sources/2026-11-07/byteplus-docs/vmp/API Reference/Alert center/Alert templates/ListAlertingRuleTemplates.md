---
title: "ListAlertingRuleTemplates"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Volcengine-Managed-Service-for-Prometheus"
---

Obtain a list of alerting rule templates of the latest versions.

## Request description

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide to provide you with a more stable, lower\-latency experience. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.

* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn?Action=ListAlertingRuleTemplates&Version=2021\-03\-03

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListAlertingRuleTemplates&serviceCode=vmp&version=2021-03-03&groupName=)

## Request parameters

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListAlertingRuleTemplates |The API name. The API name is `ListAlertingRuleTemplates`. |
|Version |String |Yes |2021\-03\-03 |The API version. The API version is `2021-03-03`. |
|PageNumber |Long |No |1 |Current page number, minimum or default value is 1. |
|PageSize |Long |No |10 |Number per page:<br><br><br>* The value ranges from 0 to 100.<br><br>* Default value is 10. |
|Filter |Object of [AlertingRuleTemplateFilter](https://docs.byteplus.com/en/docs/88/123595#alertingruletemplatefilter) |No |\- |Filter conditions for alerting rule templates. |
|SortBy |String |No |CreatedAt |Whether to perform query result sorting:<br><br><br>* The value `CreatedAt` indicates the results will be sorted. <br><br>* Absence of this parameter indicates no sorting. |
|SortOrder |String |No |Asc |Sorting order of query results:<br><br><br>* **Asc**: indicates ascending order sorting.<br><br>* **Desc**: indicates sorting in descending order. |

### AlertingRuleTemplateFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Ids |Array of String |No |["e28\-\*\*\*\*\-abf4\*\*\*\*"] |Exact query by the IDs of alerting rule templates. |
|Categories |Array of String |No |["VKE"] |Exact query by product categories of alerting rule templates. For example, using the product category `VKE` in queries indicates looking for the alerting rule templates designed for Vital Kubernetes Engine (VKE). |

## Sample request

```JSON
POST https://vmp.cn-beijing.byteplusapi.com.cn?Action=ListAlertingRuleTemplates&Version=2021-03-03
Content-Type: application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filter": {
        "Ids": [
            "e28-****-abf4****"
        ],
        "Categories": [
            "VKE"
        ]
    },
    "SortBy": "CreatedAt",
    "SortOrder": "Asc"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Total |Long |100 |Total number of alerting rule templates that met the filter conditions. |
|Items |Array of [AlertingRuleTemplate](https://docs.byteplus.com/en/docs/88/123595#alertingruletemplate) |\- |A list of alert rule templates. |

### AlertingRuleTemplate

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |e28a\-\*\*\*\*\-abf4\*\*\* |The ID of an alerting rule template. |
|Name |String |test |The name of an alerting rule template. |
|Description |String |\- |Descriptions of alerting rule templates. |
|Items |Array of [AlertingRuleTemplateItem](https://docs.byteplus.com/en/docs/88/123595#alertingruletemplateitem) |\- |A list of alert rule templates. |
|Labels |Array of [TemplateKV](https://docs.byteplus.com/en/docs/88/123595#templatekv) |\- |Global labels of alerting rule templates. They can be attached to alerts and have a higher priority than that configured for an individual rule in templates. |
|Version |String |1.0.1 |The version of the alert rule template. |
|Category |String |VKE |The product to which alerting rule templates belong. |
|Variables |Array of [Variable](https://docs.byteplus.com/en/docs/88/123595#variable) |\- |Variables included in alert rules. |
|CreateTime |String |2020\-01\-01T00:00:00Z |The time when the alert rule template was created. |
|UpdateTime |String |2020\-01\-01T00:00:00Z |The time when the alert rule template was updated. |

### AlertingRuleTemplateItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |Long |1 |The serial number of the alert rule template item. |
|Name |String |test5 |The items' names in alerting rule templates. |
|Labels |Array of [TemplateKV](https://docs.byteplus.com/en/docs/88/123595#templatekv) |\- |labels attached to alerting rules. |
|Levels |Array of [AlertingRuleLevel](https://docs.byteplus.com/en/docs/88/123595#alertingrulelevel) |\- |Alerting level. |
|PromQL |String |my_metrics{cluster=~"$Cluster"} |PromQL statements based on alerting rules. |
|Annotations |Array of [TemplateKV](https://docs.byteplus.com/en/docs/88/123595#templatekv) |\- |Annotations attached to alering rules. |
|Description |String |\- |The description of an alerting rule. |

### TemplateKV

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Name |String |key1 |Tag key. |
|Value |String |value1 |The value of the label. Leaving it empty means the key will be deleted correspondingly. |

### Variable

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |Long |1 |ID of variable. |
|Name |String |Cluster |The variable name that will be used in PromQL.<br><br>> **tip**<br><br><br><br>* > Variables are used for more specific filtering of cloud service resources in monitoring data. For example, you can find a specific VKE cluster or namespace in VKE products by using variables.<br><br><br>* > A variable name needs to start with an uppercase letter and use CamelCase convention. For example, `ClusterNode`.<br> |
|Type |String |Query |Variable type. Available values:<br><br><br>* **Query**: the dynamic PromQL variable. You can only define the name, not the value, for this type of variable. For example, cluster metrics such as cluster IDs and namespaces always have values generated dynamically. The values of dynamic variables can be obtained by specifying PromQL statements and regular expressions.<br><br>* **Custom**: a type of variables that have predefined values. For example, in cluster metrics, the workload type is fixed (such as Deployment, StatefulSet, DaemonSet) and can be directly specified. |
|Alias |String |test6 |Aliases of variables that will be displayed in the variable selector. |
|Multi |Boolean |true |Whether the variable can have multiple options enabled at the same time. Available values:<br><br><br>* **true**: enable multiple options at the same time.<br><br>* **false**: it can only enable a single option. |
|Query |String |kube_pod_info |A query by variables' values. The variables that are only applicable to the type Query. |
|Regex |String |/.*pod="(.* ?)".\* |A regular expression used to extract variables' values. The variables that are only applicable to the type Query. |
|Values |Array of String |Deployment |Predefined values of variables. The variables that are only applicable to the type Custom. |
|Default |Array of String |demo |Default value of variable. If the value is left empty:<br><br><br>* The parameter `IncludeAll` with value `False` means none of the templates will be selected.<br><br>* The parameter `IncludeAll` with value `True` means all of the templates will be selected. |
|QueryType |String |queryResult |The query types for Query variables. The variables that are only applicable to the type Query. |
|IncludeAll |Boolean |true |Whether the variable has the option **Select all**. Values:<br><br><br>* **true**: it has the option **Select all**.<br><br>* **false**: it does not have the option **Select all**. |

### AlertingRuleLevel

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Level |String |P0 |Alerting rule level. Level P0, P1, and P2 are available currently. |
|For |String |5 minutes |Alert duration, value:<br><br><br>* **0s**: raise immediately<br><br>* **1m**: 1 minute<br><br>* **2m**: 2 minutes<br><br>* **5m**: 5 minutes<br><br>* **10m**: 10 minutes |
|Comparator |String |\> |Operators used in alert rules:<br><br><br>*  **\>** : greater than<br><br>*  **\>=** : greater than or equal to<br><br>*  **<** : less than<br><br>*  **<=** : less than or equal to<br><br>*  **==** : equal to<br><br>*  **!=** : not equal to |
|Threshold |Double |1.0 |Threshold of the alert rule. |

## Sample response

```JSON
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListAlertingRuleTemplates",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 100,
        "Items": [
            {
                "Id": "e28a-****-abf4***",
                "Name": "test",
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
                "Labels": [],
                "Version": "1.0.1",
                "Category": "VKE",
                "Variables": [
                    {
                        "Id": 1,
                        "Name": "Cluster",
                        "Type": "Query",
                        "Alias": "test6",
                        "Multi": true,
                        "Query": "kube_pod_info",
                        "Regex": "/.*pod=\\\"(.*?)\\\".*",
                        "Values": [
                            ""
                        ],
                        "Default": [
                            ""
                        ],
                        "QueryType": "queryResult",
                        "IncludeAll": true
                    }
                ],
                "CreateTime": "2020-01-01T00:00:00Z",
                "UpdateTime": "2020-01-01T00:00:00Z",
                "Description": "-"
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
