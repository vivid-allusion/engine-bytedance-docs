---
title: "ListAlerts"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/ListAlerts"
---

Obtain the alert list.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an access point that is the most optimal for the region of your services according to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) document.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=ListAlerts&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListAlerts |API name. The API name is `ListAlerts`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Limit |Long |No |10 |Alerts per page:<br><br><br>* The default value is 10.<br><br>* It can be any integer from 0 to 100. |
|SearchAfter |String |No |\*\*\*\*\*\*\*\*\* |Page token. |
|Filter |Object of [AlertFilter](https://docs.byteplus.com/en/docs/vmp/ListAlerts#alertfilter) |No |\- |Alert filter condition. |
|OrderBy |String |No |InitialAlertTimestamp |Specify a value for sorting order. The only supported value is InitialAlertTimestamp. |
|Desc |Boolean |No |true |Whether to sort results in descending order:<br><br><br>* **true**: apply descending order.<br><br>* **false**: Do not apply descending order. |


<span id="AlertFilter"></span>
### AlertFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Ids |Array of String |No |["e28ae750\-bbb8\-4ff4\-abf4\*\*\*"] |Exact query by alert IDs. |
|CurrentPhase |String |No |Active |Exact query by current statuses of alerts:<br><br><br>* **Pending**: The threshold is reached but the alert duration has not yet elapsed.<br><br>* **Active**: alert has been raised<br><br>* **Resolved**: cleared automatically<br><br>* **Disabled**: cleared by humans |
|Level |String |No |P0 |Exact query by alert levels. Available levels: P0, P1, and P2. |
|AlertingRuleIds |Array of String |No |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |Exact query by alert rule IDs. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=ListAlerts&Version=2021-03-03
Content-Type: application/json
{
    "Limit": 10,
    "SearchAfter": "*********",
    "Filter": {
        "Ids": [
            "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
        ],
        "Level": "P0",
        "CurrentPhase": "Active",
        "AlertingRuleIds": [
            "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
        ]
    },
    "OrderBy": "InitialAlertTimestamp",
    "Desc": true
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Total |Long |100 |Total number of alerts. |
|ContinueToken |String |\*\*\*\*\*\*\* |The page token used to mark one of the segments in a list. |
|Items |Array of [Alert](https://docs.byteplus.com/en/docs/vmp/ListAlerts#alert) |\- |Alert list. |


<span id="Alert"></span>
### Alert


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |The alert ID. |
|AlertingRuleId |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Alert rule ID. |
|Levels |Array of [AlertingRuleLevel](https://docs.byteplus.com/en/docs/vmp/ListAlerts#alertingrulelevel) | |Alert level configurations. |
|InitialAlertTimestamp |String |2020\-01\-01T00:00:00Z |The start of a time range for alert statistics. It is presented in RFC3339 format. |
|LastAlertTimestamp |String |2020\-01\-01T00:00:00Z |The time of the latest alert that has been raised. It is presented in RFC3339 format. |
|ResolveTimestamp |String |2020\-01\-01T00:00:00Z |The end of a time range for alert statistics. It is presented in RFC3339 format. |
|CurrentPhase |String |Active |Alert status:<br><br><br>* **Pending**: The threshold is reached but the alert duration has not yet elapsed.<br><br>* **Active**: alert has been raised<br><br>* **Resolved**: cleared automatically<br><br>* **Disabled**: cleared by humans |
|CurrentLevel |String |P0 |Levels of alerts. Level P0, P1, and P2 are available currently. |
|AlertingRuleType |String |vmp/PromQL |Alert rule type. Available value is `vmp/PromQL`. |
|AlertingRuleQuery |Object of [AlertingRuleQuery](https://docs.byteplus.com/en/docs/vmp/ListAlerts#alertingrulequery) |\- |Alert configuration. |
|Resource |Object of [AlertResource](https://docs.byteplus.com/en/docs/vmp/ListAlerts#alertresource) |\- |Alert resource. |


<span id="AlertingRuleLevel"></span>
### AlertingRuleLevel


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Level |String |P0 |Levels of alerts. Level P0, P1, and P2 are available currently. |
|For |String |5 minutes |How long the state of meeting alert conditions needs to last before raising alerts:<br><br><br>* **0s**: raise immediately<br><br>* **1m**: 1 minute<br><br>* **2m**: 2 minutes<br><br>* **5m**: 5 minutes<br><br>* **10m**: 10 minutes |
|Comparator |String |\> |Operators used in alert rules:<br><br><br>*  **\>** : greater than<br><br>*  **\>=** : greater than or equal to<br><br>*  **<** : less than<br><br>*  **<=** : less than or equal to<br><br>*  **==** : equal to<br><br>*  **!=** : not equal to |
|Threshold |Double |1.0 |The threshold of the alert. |


<span id="AlertingRuleQuery"></span>
### AlertingRuleQuery


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|WorkspaceId |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Workspace ID |
|PromQL |String |sum(up) |Query statement. |


<span id="AlertResource"></span>
### AlertResource


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Labels |Array of [LabelKeyValuePair](https://docs.byteplus.com/en/docs/vmp/ListAlerts#labelkeyvaluepair) |\- |* A list of resource labels.<br><br>* Each element in the list is a key\-value pair.<br><br>* The key represents the resource label (e.g. Pod).<br><br>* The value represents the resource name (e.g. Pod Name). |


<span id="LabelKeyValuePair"></span>
### LabelKeyValuePair


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Key |String |key |Key |
|Value |String |value |Value |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListAlerts",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 100,
        "ContinueToken": "*******",
        "Items": [
            {
                "Id": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
                "Levels": [
                    {
                        "For": "5m",
                        "Level": "P0",
                        "Threshold": 1,
                        "Comparator": ">"
                    }
                ],
                "Resource": {
                    "Labels": [
                        {
                            "Key": "key",
                            "Value": "value"
                        }
                    ]
                },
                "CurrentLevel": "P0",
                "CurrentPhase": "Active",
                "AlertingRuleId": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
                "AlertingRuleType": "vmp/PromQL",
                "ResolveTimestamp": "2020-01-01T00:00:00Z",
                "AlertingRuleQuery": {
                    "PromQL": "sum(up)",
                    "WorkspaceId": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
                },
                "LastAlertTimestamp": "2020-01-01T00:00:00Z",
                "InitialAlertTimestamp": "2020-01-01T00:00:00Z"
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
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |The specified parameter is invalid. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |
