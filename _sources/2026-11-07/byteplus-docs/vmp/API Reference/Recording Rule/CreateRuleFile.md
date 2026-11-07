---
title: "CreateRuleFile"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/CreateRuleFile"
---

Create a RecordingRule file.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide to provide you with a more stable, lower\-latency experience. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=CreateRuleFile&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameters |Type |Required or Not |Sample Values |Descriptions |
|---|---|---|---|---|
|Action |String |Yes |CreateRuleFile |interface name. The API name is `CreateRuleFile`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|WorkspaceId |String |Yes |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Workspace ID. You can call the [ListWorkspaces](https://docs.byteplus.com/en/docs/vmp/ListWorkspaces) API to obtain the workspace ID. |
|Name |String |Yes |test |Rule file name:<br><br><br>* A valid Linux file name with a length less than 255.<br><br>* It needs to be unique in the workspace. |
|Description |String |No |This is a description |Description of the rule file. It can contain 200 characters at most.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">An English letter, a Chinese word, or any single symbol is counted as a character.</div><br> |
|Content |String |Yes |{"groups": [{"name": "my_first_recording_rule", "rules": [{"expr": "up", "record": "up"}], "interval": "30s"}]} |Rule file content in yaml format with the following requirements:<br><br><br>* A single `expr` can be up to 16 KB in size.<br><br>* A single `record` can be up to 2,048 bytes in size.<br><br>* A single `labelname` can be up to 256 bytes in size.<br><br>* A single `labelvalue` can be up to 2,048 bytes in size |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=CreateRuleFile&Version=2021-03-03
Content-Type: application/json
{
    "WorkspaceId": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
    "Name": "test",
    "Description": "This is a description",
    "Content": "{\"groups\": [{\"name\": \"my_first_recording_rule\", \"rules\": [{\"expr\": \"up\", \"record\": \"up\"}], \"interval\": \"30s\"}]}"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameters |Type |Value example |Descriptions |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |RecordingRule rule file ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateRuleFile",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The following table lists the error codes specific to this API. For public error codes, see [public error code](https://docs.byteplus.com/en/docs/vmp/Common-error-codes)s.


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |QuotaExceeded.RuleGroupCount |Rule Group count has exceeded the quota. |The number of rule files has reached the upper limit. |
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |An invalid parameter was found. For example, an invalid workspace name was included in requests. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing necessary parameters. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP service. |
|403 |OperationDenied.Create |Operation is denied because RuleFile cannot be created in Workspace`s current status |It is not allowed to create any rule files on the current status of the workspace. |
|404 |NotFound.Workspace |The specified Workspace {{id}} is not found. |The workspace with the ID was not found. |
|409 |Conflict.Name |The specified name conflicts with existing {{resource}}. |The specified name has already been used by an existing resource. |
