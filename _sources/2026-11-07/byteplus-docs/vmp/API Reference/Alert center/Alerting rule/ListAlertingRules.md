---
title: "ListAlertingRules"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/ListAlertingRules"
---

Obtain the list of alerting rules.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=ListAlertingRules&Version=2021\-03\-03


<span id="nmuoE7PD"></span>
## Debugging

[去调试]()


&nbsp;

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListAlertingRules |API name. The API name is `ListAlertingRules`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|PageNumber |Long |No |1 |Current page number. The minimum and default values are both 1. |
|PageSize |Long |No |10 |Results per page:<br><br><br>* A number from 0 to 100.<br><br>* The default value is 10. |
|Filter |Object of [AlertingRuleFilter](https://docs.byteplus.com/en/docs/vmp/ListAlertingRules#alertingrulefilter) |No |\- |Filter conditions for alerting rules. |
|SortBy |String |No |CreatedAt |Whether to perform query result sorting:<br><br><br>* The value `CreatedAt` indicates the results will be sorted. <br><br>* Absence of this parameter indicates no sorting. |
|SortOrder |String |No |Asc |Sorting order of query results:<br><br><br>* **Asc**: indicates sorting in ascending order.<br><br>* **Desc**: indicates sorting in descending order. |


<span id="AlertingRuleFilter"></span>
### AlertingRuleFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Ids |Array of String |No |["90b5a3da\-3464\-4718\-92e4\-039bf41d3cff"] |Exact query by alerting rule IDs. |
|Name |String |No |alert\-rule\-demo |Fuzzy query by the names of alerting rules. |
|Type |String |No |vmp/PromQL |Exact query by alerting rule types. |
|WorkspaceId |String |No |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Exact query by workspace IDs. |
|NotifyPolicyIds |Array of String |No |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |Exact query by IDs of alerting notification policies. |
|NotifyGroupPolicyIds |Array of String |No |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |Exact query by IDs of alerting aggregation policies. |
|Status |String |No |Running |Filter by alerting rule status:<br><br><br>* **Running**: rules that are enabled<br><br>* **Disabled**: rules that are disabled |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=ListAlertingRules&Version=2021-03-03
Content-Type: application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filter": {
        "Ids": [
            "90b5a3da-3464-4718-92e4-039bf41d3cff"
        ],
        "Name": "alert-rule-demo",
        "Type": "vmp/PromQL",
        "Status": "Running",
        "WorkspaceId": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
        "NotifyPolicyIds": [
            "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
        ],
        "NotifyGroupPolicyIds": [
            "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
        ]
    },
    "SortBy": "CreatedAt",
    "SortOrder": "Asc"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Total |Long |100 |Total number of alerting rules. |
|Items |Array of [AlertingRule](https://docs.byteplus.com/en/docs/vmp/ListAlertingRules#alertingrule) |\- |Alerting rule list. |


<span id="AlertingRule"></span>
### AlertingRule


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |90b5a3da\-3464\-4718\-92e4\-039bf41d3cff |Alerting rule ID. |
|CreateTime |String |2020\-01\-01T00:00:00Z |The creation date of the alerting rule. |
|UpdateTime |String |2020\-01\-01T00:00:00Z |The update date of the alerting rule. |
|Name |String |alert\-rule\-demo |The name of the alerting rule. |
|Description |String |this is a alert rule demo |Description of the alerting rule. |
|Type |String |vmp/PromQL |Alerting rule type. Available value is `vmp/PromQL`. |
|Query |Object of [AlertingRuleQuery](https://docs.byteplus.com/en/docs/vmp/ListAlertingRules#alertingrulequery) |\- |Alert configuration. |
|Levels |Array of [AlertingRuleLevel](https://docs.byteplus.com/en/docs/vmp/ListAlertingRules#alertingrulelevel) |\- |The alert level. |
|NotifyPolicyId |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Alerting notification policy ID. |
|NotifyGroupPolicyId |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Alerting aggregation policy ID. |
|Status |String |Running |Alerting rule status:<br><br><br>* **Running**: rules that are enabled<br><br>* **Disabled**: rules that are disabled |
|Labels |Array of [TemplateKV](https://docs.byteplus.com/en/docs/vmp/ListAlertingRules#templatekv) |\- |Labels to be added to the alert. |
|Annotations |Array of [TemplateKV](https://docs.byteplus.com/en/docs/vmp/ListAlertingRules#templatekv) |\- |Annotations added to the alert. |


<span id="AlertingRuleQuery"></span>
### AlertingRuleQuery


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|WorkspaceId |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Workspace ID. |
|PromQL |String |sum(up) |Query statement. |


<span id="AlertingRuleLevel"></span>
### AlertingRuleLevel


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Level |String |P0 |Alerting rule level. Level P0, P1, and P2 are available currently. |
|For |String |5m |How long the state of meeting alerting conditions needs to last before raising alerts:<br><br><br>* **0s**: raise immediately<br><br>* **1m**: 1 minute<br><br>* **2m**: 2 minutes<br><br>* **5m**: 5 minutes<br><br>* **10m**: 10 minutes |
|Comparator |String |\> |Operators used in alerting rules:<br><br><br>*  **\>** : greater than<br><br>*  **\>=** : greater than or equal to<br><br>*  **<** : less than<br><br>*  **<=** : less than or equal to<br><br>*  **==** : equal to<br><br>*  **!=** : not equal to |
|Threshold |Double |1.0 |The threshold of the alert. |


<span id="TemplateKV"></span>
### TemplateKV


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Name |String |key1 |Key of label or annotation. |
|Value |String |value1 |Value of label or annotation. Leaving it empty means the key will be deleted correspondingly. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListAlertingRules",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 100,
        "Items": [
            {
                "Id": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
                "Name": "alert-rule-demo",
                "Description": "this is an alert rule demo",
                "Type": "vmp/PromQL",
                "Query": {
                    "PromQL": "sum(up)",
                    "WorkspaceId": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
                },
                "Levels": [
                    {
                        "For": "5m",
                        "Level": "P0",
                        "Threshold": 1,
                        "Comparator": ">"
                    }
                ],
                "Labels": [
                    {
                        "Name": "key1",
                        "Value": "value1"
                    }
                ],
                "annotations": [
                    {
                        "Name": "key1",
                        "Value": "value1"
                    }
                ],
                "Status": "Running",
                "CreateTime": "2020-01-01T00:00:00Z",
                "UpdateTime": "2020-01-01T00:00:00Z",
                "NotifyPolicyId": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
                "NotifyGroupPolicyId": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The error codes for current API only are listed in the table below. See [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes) to view error codes for any APIs.


|HTTP status codes |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |An invalid parameter was found. For example, an invalid workspace name was included in requests. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |
