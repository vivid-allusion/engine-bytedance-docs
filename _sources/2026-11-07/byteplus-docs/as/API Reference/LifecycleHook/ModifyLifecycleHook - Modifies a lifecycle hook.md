---
title: "ModifyLifecycleHook - Modifies a lifecycle hook"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/ModifyLifecycleHook"
---

Modify a lifecycle hook. If optional parameters are not provided, they will not be modified.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyLifecycleHook&groupName=%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E6%8C%82%E9%92%A9&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|L5j7Mr">必选</span> `Sample value: ModifyLifecycleHook`

The action that you want to perform. Value: ModifyLifecycleHook.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|C5aTgI">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**LifecycleHookId ** <span data-label="purple">string </span><span data-api-tag="require|TnAnaR">必选</span> `Sample value: sgh-ybrzhc5ht08hccnm****`

The ID of the lifecycle hook. You can call [DescribeLifecycleHooks](https://docs.byteplus.com/en/docs/as/DescribeLifecycleHooks) to query the lifecycle hook ID.



**LifecycleCommand.CommandId ** <span data-label="purple">string </span>`Optional` `Sample value: cmd-4302d02424c5c8e10281e3a31****`

The ID of the cloud assistant command. After the lifecycle hook is triggered, the specified cloud assistant command is executed in the target instance.


* If the command execution succeeds, the execution will continue based on the "CONTINUE" policy after suspension ends.

* If the command execution fails, times out, or the lifecycle hook times out, the corresponding execution policy takes effect based on the `LifecycleHookPolicy` parameter after suspension ends.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before enabling cloud assistant, you need to first create the required O&M commands and confirm that the related instances have cloud assistant Agent installed. For detailed operations, refer to <a href="https://docs.byteplus.com/en/docs/as/Overview-of-lifecycle-hooks#.55u45YWz5Yqf6IO9">Introduction to associating lifecycle hooks with cloud assistant</a>.</div>




**LifecycleCommand.Parameters ** <span data-label="purple">string </span>`Optional` `Sample value: "username":"root","password":"123456"`

Indicates the parameter and parameter value in the cloud assistant command.

Parameter count range: 0 ~ 60. Note:


* The parameter can not be an empty string and can be up to 64 characters in length.

* The value can be an empty string.

* After Base64 encoding, the combined length of the parameter and original command content can not exceed 16KB.

* The set of parameter names configured is required to be a subset of the parameter set defined when the command is created. For the parameter not provided, the default parameter value is used.



**LifecycleHookPolicy ** <span data-label="purple">string </span>`Optional` `Sample value: CONTINUE`

The execution policy after the instance's suspended status ends. Valid values:


* CONTINUE: Execution continues.

* REJECT: Subsequent adjustment is discontinued.

* ROLLBACK: For scale\-in operations, ECS instances are not released but rolled back. For scale\-out operations, the logic is the same as that of REJECT.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details about the instance change process after execution, see <a href="https://docs.byteplus.com/en/docs/as/Overview-of-lifecycle-hooks#.5omn6KGM5rWB56iL5ZKM562W55Wl">Execution processes and policies</a>.</div>




**LifecycleHookTimeout ** <span data-label="purple">integer </span>`Optional` `Sample value: 3600`

The duration for which an ECS instance remains in the suspended status. After the hook times out, the suspended status ends automatically, and the scaling operations continue based on the execution policy. After you evaluate the execution time of your custom actions, set an appropriate timeout period. Value: 30 ~ 21600 (6 hours). Unit: seconds. The value must be an integer.



**LifecycleHookType ** <span data-label="purple">string </span>`Optional` `Sample value: SCALE_IN`

The scaling activity type. When a scaling activity of the specified type occurs, a lifecycle hook is triggered and the target ECS instance enters a suspended status. Valid values:


* SCALE_IN: Scale\-in event.

* SCALE_OUT: Scale\-out event.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**LifecycleHookId ** <span data-label="purple">string </span>`Sample value: sgh-ybrzhc5ht08hccnm****`

The ID of the lifecycle hook.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ModifyLifecycleHook&LifecycleHookId=sgh-ybrzhc5ht08hccnm****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T112252Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240507192301201017167101BCB161",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "LifecycleHookId": "sgh-ybrzhc5ht08hccnm****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/as/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.LifecycleHookId |The required parameter LifecycleHookId is not supplied. |The lifecycle hook ID cannot be empty. |
|400 |LimitExceeded.LifecycleHookName |You've reached the limit on the length of LifecycleHookName. |The lifecycle hook name has reached the upper limit in length. |
|400 |InvalidLifecycleHookTimeout.Malformed |The specified LifecycleHookTimeout is malformed. |The specified timeout period of the lifecycle hook is invalid. |
|400 |InvalidLifecycleHookType.Malformed |The specified LifecycleHookType is malformed. |The specified adjustment type associated with the lifecycle hook is invalid. |
|400 |InvalidLifecycleHookPolicy.Malformed |The specified LifecycleHookPolicy is malformed. |The specified lifecycle hook policy is invalid. |
|400 |InvalidLifecycleCommandParameters.Malformed |The specified LifecycleCommand Parameters are malformed. |The specified cloud assistant command parameters are invalid. |
|400 |MissingParameter.LifecycleCommandParameters |The required parameter LifecycleCommand Parameters[%s] is not supplied. |The parameter of the specified cloud assistant command cannot be empty. |
|400 |ErrInvalidLifecycleCommandParameters |The specified LifecycleCommand Parameters [%s] is unsupported. |The specified parameter of the cloud assistant command is invalid. |
|400 |InvalidLifecycleCommandParametersValue |The specified value of LifecycleCommand Parameters [%s] is unsupported. |The specified value of the cloud assistant command parameter is invalid. |
|404 |InvalidLifecycleHookId.NotFound |The specified LifecycleHookId does not exist. |The specified lifecycle hook ID does not exist. |
|404 |InvalidLifecycleCommand.NotFound |The specified LifecycleCommand does not exist. |The specified cloud assistant command does not exist. |
|409 |InvalidLifecycleHookName.Conflict |The specified LifecycleHookeName already exists. |The specified lifecycle hook name already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
