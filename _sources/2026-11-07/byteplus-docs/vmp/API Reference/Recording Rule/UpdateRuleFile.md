---
title: "UpdateRuleFile"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/UpdateRuleFile"
---

Update the RecordingRule file.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide to provide you with a more stable, lower\-latency experience. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=UpdateRuleFile&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request descriptions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Use either <code>Id</code> or <code>WorkspaceId + Name</code> as parameters.</div>



* <div data-tips="true" data-tips-type="tip">Update a rule file by <code>ID</code>.</div>


* <div data-tips="true" data-tips-type="tip">or update a rule file by <code>WorkspaceId + Name</code>, i.e., a workspace ID and a file name in it.</div>




|Parameters |Types |Required or Not |Sample Values |Descriptions |
|---|---|---|---|---|
|Action |String |Yes |UpdateRuleFile |interface name. The API name is `UpdateRuleFile`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Id |String |No |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Rule file ID. |
|WorkspaceId |String |No |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Workspace ID. It is always used together with `Name`. |
|Name |String |No |test |Rule file name. It is always used together with `WorkspaceId`. |
|Description |String |No |This is a description |Description of rule file. |
|Content |String |No |{"groups": [{"name": "my_first_recording_rule", "rules": [{"expr": "up", "record": "up"}], "interval": "30s"}]} |Rule file content. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=UpdateRuleFile&Version=2021-03-03
Content-Type: application/json
{
    "Id": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
    "WorkspaceId": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
    "Name": "test",
    "Description": "This is a description",
    "Content": "{\"groups\": [{\"name\": \"my_first_recording_rule\", \"rules\": [{\"expr\": \"up\", \"record\": \"up\"}], \"interval\": \"30s\"}]}"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Request parameters


|Parameters |Type |Value examples |Descriptions |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Rule file ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateRuleFile",
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
## Error code  

The following table lists the error codes specific to this API. For public error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).


|HTTP status codeS |Error code |Error messages |DescriptionS |
|---|---|---|---|
|400 |QuotaExceeded.RuleGroupCount |Rule Group count has exceeded the quota. |The number of rule files has reached the upper limit. |
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |An invalid parameter was found. For example, an invalid workspace name was included in requests. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing necessary parameters. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP service. |
|403 |OperationDenied.Create |Operation is denied because RuleFile cannot be created in Workspace`s current status. |It is not allowed to create any rule files on the current status of the workspace. |
|404 |NotFound.Workspace |The specified Workspace {{id}} is not found. |The workspace with the ID was not found. |
|404 |NotFound.Name |The specified RuleFile {{name}} is not found in Workspace {{workspaceID}}. |The rule file was not found in the specified workspace. |
