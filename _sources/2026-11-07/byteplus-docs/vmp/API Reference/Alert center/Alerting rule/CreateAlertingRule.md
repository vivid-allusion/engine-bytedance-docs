---
title: "CreateAlertingRule"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/CreateAlertingRule"
---

Creating an alerting rule.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn?Action=CreateAlertingRule&Version=2021\-03\-03


<span id="INgA1Itx"></span>
## Debugging

[去调试]()


&nbsp;

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Make sure there are no duplicate level values when multiple levels need to be configured under the parameter Levels in a single request.</div>



|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateAlertingRule |API name. The API name is `CreateAlertingRule`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Name |String |Yes |alert\-rule\-demo |The name of the alerting rule. It needs to be unique under the same account. |
|Description |String |No |This is an alerting rule demo |Description of the alerting rule. |
|Type |String |Yes |vmp/PromQL |Alerting rule type. Available value is `vmp/PromQL`. |
|Query |Object of [AlertingRuleQuery](https://docs.byteplus.com/en/docs/vmp/CreateAlertingRule#alertingrulequery) |Yes |\- |Alert configuration. |
|Levels |Array of [AlertingRuleLevel](https://docs.byteplus.com/en/docs/vmp/CreateAlertingRule#alertingrulelevel) |Yes |\- |The alert level. |
|NotifyPolicyId |String |No |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Alerting notification policy ID. |
|NotifyGroupPolicyId |String |Yes |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Alerting aggregation policy ID. |
|Annotations |Array of [TemplateKV](https://docs.byteplus.com/en/docs/vmp/CreateAlertingRule#templatekv) |No |\- |Annotations added to the alert. |
|Labels |Array of [TemplateKV](https://docs.byteplus.com/en/docs/vmp/CreateAlertingRule#templatekv) |No |\- |Labels to be added to the alert. |


<span id="AlertingRuleQuery"></span>
### AlertingRuleQuery


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|WorkspaceId |String |Yes |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Workspace ID |
|PromQL |String |Yes |sum(up) |Query statement. |


<span id="AlertingRuleLevel"></span>
### AlertingRuleLevel


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Level |String |Yes |P0 |Alerting rule level. Level P0, P1, and P2 are available currently. |
|For |String |Yes |5 minutes |How long the state of meeting alerting conditions needs to last before raising alerts:<br><br><br>* **0s**: raise immediately<br><br>* **1m**: 1 minute<br><br>* **2m**: 2 minutes<br><br>* **5m**: 5 minutes<br><br>* **10m**: 10 minutes |
|Comparator |String |Yes |\> |Operators used in alerting rules:<br><br><br>*  **\>** : greater than<br><br>*  **\>=** : greater than or equal to<br><br>*  **<** : less than<br><br>*  **<=** : less than or equal to<br><br>*  **==** : equal to<br><br>*  **!=** : not equal to |
|Threshold |Double |No |1.0 |The threshold of the alert. |


<span id="TemplateKV"></span>
### TemplateKV


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Name |String |Yes |key1 |Key of label or annotation. |
|Value |String |No |value1 |Value of label or annotation. Leaving it empty means the key will be deleted correspondingly. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=ListWorkspaces&Version=2021-03-03
Content-Type: application/json
{
    "Name": "alert-rule-demo",
    "Description": "this is a alert rule demo",
    "Type": "vmp/PromQL",
    "Query": {
        "WorkspaceId": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
        "PromQL": "sum(up)"
    },
    "Levels": [
        {
            "Level": " P0",
            "For": " 5m",
            "Comparator": " >",
            "Threshold": 1.0
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
    "NotifyPolicyId": "8cd7b480-6387-44e5-aea4-db4ca2c4b47a",
    "NotifyGroupPolicyId": "ce4d942a-bac3-4ef6-b3a0-b7845b3b53bf"
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
        "RequestId": "202211302208xxxx",
        "Action": "CreateAlertingRule",
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

The following table lists the error codes specific to this API. For public error codes, see[ Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).


|HTTP status codes |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |An invalid parameter was found. For example, an invalid workspace name was included in requests. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing required parameters. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |
|409 |Conflict.Name |The specified name conflicts with existing {{resource}}. |The specified name has already been used by an existing resource. |
