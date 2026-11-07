---
title: "GetRuleFile"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/GetRuleFile"
---

Obtain the details of a RecordingRule file.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide to provide you with a more stable, lower\-latency experience. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=GetRuleFile&Version=2021\-03\-03


<span id="4nOhG8nB"></span>
## Debugging

[去调试]()


&nbsp;

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Use either <code>Id</code> or <code>WorkspaceId + Name</code> as parameters, which means you can:</div>



* <div data-tips="true" data-tips-type="tip">find a rule file by <code>Id</code>,</div>


* <div data-tips="true" data-tips-type="tip">or find a rule file by <code>WorkspaceId + Name</code>, i.e., a workspace ID and a file name in it.</div>




|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |GetRuleFile |API name. The API name is `GetRuleFile`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Id |String |No |1c3f6e48\-b5e1\-4832\-8564\-10eaac12a22c |Rule file ID. |
|WorkspaceId |String |No |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Workspace ID. It is always used together with `Name`. |
|Name |String |No |test |Rule file name. It is always used together with `WorkspaceId`. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=GetRuleFile&Version=2021-03-03
Content-Type: application/json
{
    "Id": "1c3f6e48-b5e1-4832-8564-10eaac12a22c",
    "WorkspaceId": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
    "Name": "test"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Rule file ID. |
|CreateTime |String |2022\-01\-01T00:00:00Z |The creation date of the rule file. It is presented in RFC3339 format. |
|LastUpdateTime |String |2022\-01\-01T00:00:00Z |The latest date the rule file was updated. It is presented in RFC3339 format. |
|Name |String |test |Rule file name. |
|Description |String |This is a description |Description of the rule file. |
|Content |String |```yaml```<br>```groups:```<br>```- name: example```<br>```  rules:```<br>```    - record: test```<br>```      expr: up```<br> |Rule file content. |
|Status |String |Running |Status of rule file:<br><br><br>* **Creating**: in the process of creating<br><br>* **Running**: in the process of running<br><br>* **Updating**: in the process of updating<br><br>* **OverdueShutted**: suspended for overdue payment<br><br>* **Resuming**: in the process of reactivating |
|RuleCount |Long |2 |Number of rules in the rule file. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202211302208xxxx",
        "Action": "GetRuleFile",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": " 1c3f6e48-b5e1-4832-8564-10eaac12a22c",
        "CreateTime": "2022-01-01T00:00:00Z",
        "LastUpdateTime": "2022-01-01T00:00:00Z",
        "Name": "test",
        "description": "this is a description",
        "content": "groups:\n- name: example\n  rules:\n  - expr: up\n    record: test\n",
        "Status": "Running",
        "RuleCount": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The error codes for current API only are listed in the table below. See [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes) to view error codes for any APIs.


|HTTP status codes |Error codes |Error message |Description |
|---|---|---|---|
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |
|404 |NotFound.Workspace |The specified Workspace {{id}} is not found. |The workspace with the ID was not found. |
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |An invalid parameter was found. For example, an invalid workspace name was included in requests. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing necessary parameters. |
