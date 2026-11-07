---
title: "ListRules"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/ListRules"
---

Retrieve the list of RecordingRules.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide to provide you with a more stable, lower\-latency experience. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=ListRules&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListRules |API name. The API name is `ListRules`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|PageNumber |Long |No |1 |Current page number. The minimum and default values are both 1. |
|PageSize |Long |No |10 |Results per page:<br><br><br>* A number from 0 to 100.<br><br>* The default number is 10. |
|Filter |Object of [RuleFilter](https://docs.byteplus.com/en/docs/vmp/ListRules#rulefilter) |No |\- |Filter conditions for rules. |


<span id="RuleFilter"></span>
### RuleFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Kind |String |Yes |Recording |Filter by rule type. Available value is Recording. |
|Name |String |No |test |Fuzzy query by the name of a rule. |
|Status |Array of String |No |["Running"] |Exact query by rule statuses. |
|WorkspaceId |String |Yes |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Exact query by workspace IDs. |
|RuleFileNames |Array of String |No |["test"] |Fuzzy query by names of rule files. |
|RuleGroupNames |Array of String |No |["test"] |Fuzzy query by names of rule groups. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=ListRules&Version=2021-03-03
Content-Type: application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filter": {
        "Kind": "Recording",
        "Name": "test",
        "Status": [
            "Running"
        ],
        "WorkspaceId": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
        "RuleFileNames": [
            "test"
        ],
        "RuleGroupNames": [
            "test"
        ]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Total |Long |100 |Total number of rules. |
|Items |Array of [Rule](https://docs.byteplus.com/en/docs/vmp/ListRules#rule) |\- |A list of rules. |


<span id="Rule"></span>
### Rule


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Expr |String |sum(rate(container_cpu_usage_seconds_total[5m])) by (pod) |The PromQL expression of a rule. |
|Kind |String |Recording |Rule type. Available value is Recording. |
|Name |String |my_first_recording_rule |Rule name. Fuzzy query can be applied to it. |
|Labels |Array of [LabelKeyValuePair](https://docs.byteplus.com/en/docs/vmp/ListRules#labelkeyvaluepair) |source:recordingRule |Labels that are added or overwritten before metrics are stored. |
|Reason |String |internal error |The reason that the status changes to error. |
|Status |String |Running |Rule status\n\- Running\n\- Updating\n\- OverdueShutted (shutdown due to overdue payment)\n\- Resuming\n\- Error\n\- Pending |
|RuleFileName |String |test |The name of the rule file to which the rule belongs |
|RuleGroupName |String |test |The name of the rule group to which the rule belongs |
|LastEvaluation |String |2022\-01\-01T00:00:00Z |The latest execution time, in RFC3339 format. |


<span id="LabelKeyValuePair"></span>
### LabelKeyValuePair


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Key |String |key |The key of a label |
|Value |String |value |The value of a label |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListRules",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 100,
        "Items": [
            {
                "Expr": "sum(rate(container_cpu_usage_seconds_total[5m])) by (pod)",
                "Kind": "Recording",
                "Name": "my_first_recording_rule",
                "Labels": [
                    {
                        "Key": "key",
                        "Value": "value"
                    }
                ],
                "Reason": "internal error",
                "Status": "Running",
                "RuleFileName": "test",
                "RuleGroupName": "test",
                "LastEvaluation": "2022-01-01T00:00:00Z"
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
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing required parameters. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |
|404 |NotFound.Workspace |The specified Workspace {{id}} is not found. |The workspace with the ID was not found. |
