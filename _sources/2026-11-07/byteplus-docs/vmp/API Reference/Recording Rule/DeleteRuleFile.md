---
title: "DeleteRuleFile"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/DeleteRuleFile"
---

Delete a RecordingRule rule file.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide to provide you with a more stable, lower\-latency experience. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=DeleteRuleFile&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Use either <code>Id</code> or <code>WorkspaceId + Name</code> as parameters. </div>



* <div data-tips="true" data-tips-type="tip">Delete a rule file by <code>ID</code>.</div>


* <div data-tips="true" data-tips-type="tip">or delete a rule file by <code>WorkspaceId + Name</code>, i.e., a workspace ID and a file name in it.</div>




|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |DeleteRuleFile |API name. The API name is `DeleteRuleFile`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Id |String |No |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Rule file ID. |
|WorkspaceId |String |No |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Workspace ID. It is always used together with `Name`. |
|Name |String |No |test |Rule file name. It is always used together with `WorkspaceId`. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=DeleteRuleFile&Version=2021-03-03
Content-Type: application/json
{
    "Id": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
    "WorkspaceId": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
    "Name": "test"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
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
        "Action": "DeleteRuleFile",
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
## Error codes

The following table lists the error codes specific to this API. For public error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).


|HTTP status codes |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |An invalid parameter was found. For example, an invalid workspace name was included in requests. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing required parameters. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |
|403 |OperationDenied.Update |Operation is denied because RuleFile cannot be updated in Workspace`s current status. |It is not allowed to update any rule files on the current status of the workspace. |
|404 |NotFound.Name |The specified RuleFile {{name}} is not found in Workspace {{workspaceID}}. |The rule file was not found in the specified workspace. |
