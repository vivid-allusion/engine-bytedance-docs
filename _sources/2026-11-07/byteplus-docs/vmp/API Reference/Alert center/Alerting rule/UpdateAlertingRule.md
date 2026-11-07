---
title: "UpdateAlertingRule"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/UpdateAlertingRule"
---

Update an alerting rule.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=UpdateAlertingRule&Version=2021\-03\-03


<span id="G5QXsYMg"></span>
## Debugging

[去调试]()


&nbsp;

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The parameters type and query need to be used in pairs.</div>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Make sure there are no duplicate level values when multiple levels need to be configured under the parameter Levels in a single request.</div>



|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |UpdateAlertingRule |API name. The API name is `UpdateAlertingRule`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Id |String |Yes |90b5a3da\-3464\-4718\-92e4\-039bf41d3cff |Alerting rule ID. |
|Name |String |No |alert\-rule\-demo |The name of the alerting rule. |
|Description |String |No |This is an alert rule demo |Description of the alerting rule. |
|Type |String |No |vmp/PromQL |Alerting rule type. Available value is `vmp/PromQL`. |
|Query |Object of [AlertingRuleQuery](https://docs.byteplus.com/en/docs/vmp/UpdateAlertingRule#alertingrulequery) |No |\- |Alerting configurations. |
|Levels |Array of [AlertingRuleLevel](https://docs.byteplus.com/en/docs/vmp/UpdateAlertingRule#alertingrulelevel) |No |\- |Alerting level. |
|NotifyPolicyId |String |No |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Alerting notification policy ID. |
|NotifyGroupPolicyId |String |No |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Alert aggregation policy ID. |
|Annotations |Array of [TemplateKV](https://docs.byteplus.com/en/docs/vmp/UpdateAlertingRule#templatekv) |No |\- |Annotations added to the alert. |
|Labels |Array of [TemplateKV](https://docs.byteplus.com/en/docs/vmp/UpdateAlertingRule#templatekv) |No |\- |The labels to be added to an alert. |


<span id="AlertingRuleQuery"></span>
### AlertingRuleQuery


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|WorkspaceId |String |Yes |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Workspace ID. |
|PromQL |String |Yes |sum(up) |Query statement. |


<span id="AlertingRuleLevel"></span>
### AlertingRuleLevel


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Level |String |Yes |P0 |Alerting rule level. Level P0, P1, and P2 are available currently. |
|For |String |Yes |5m |How long the state of meeting alerting conditions needs to last before raising alerts:<br><br><br>* **0s**: raise immediately<br><br>* **1m**: 1 minute<br><br>* **2m**: 2 minutes<br><br>* **5m**: 5 minutes<br><br>* **10m**: 10 minutes |
|Comparator |String |Yes |\> |Operators used in alerting rules:<br><br><br>*  **\>** : greater than<br><br>*  **\>=** : greater than or equal to<br><br>*  **<** : less than<br><br>*  **<=** : less than or equal to<br><br>*  **==** : equal to<br><br>*  **!=** : not equal to |
|Threshold |Double |No |1.0 |Threshold of the alerting rule. |


<span id="TemplateKV"></span>
### TemplateKV


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Name |String |Yes |key1 |Key of label or annotation. |
|Value |String |No |value1 |Value of label or annotation. Leaving it empty means the key will be deleted correspondingly. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=UpdateAlertingRule&Version=2021-03-03
Content-Type: application/json
{
    "Id": "90b5a3da-3464-4718-92e4-039bf41d3cff",
    "Name": "alert-rule-demo",
    "Description": "this is a alert rule demo",
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
    "Annotations": [
        {
            "Name": "key1",
            "Value": "value1"
        }
    ],
    "NotifyPolicyId": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
    "NotifyGroupPolicyId": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |90b5a3da\-3464\-4718\-92e4\-039bf41d3cff |Alerting rule ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateAlertingRule",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "90b5a3da-3464-4718-92e4-039bf41d3cff"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The error codes for current API only are listed in the table below. See [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes) to view error codes for any APIs.


|HTTP status codes |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |An invalid parameter was found. For example, an invalid workspace name was included in requests. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing necessary parameters. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |
|404 |NotFound.Id |The specified Contact/ContactGroup {{Id}} is not found. |The specified contact person/group is not found. |
|409 |Conflict.Name |The specified name conflicts with existing {{resource}}. |The specified name has already been used by an existing resource. |
