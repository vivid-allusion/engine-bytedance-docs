---
title: "DescribeLifecycleHooks - Queries lifecycle hooks"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/DescribeLifecycleHooks"
---

Query lifecycle hooks.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeLifecycleHooks&groupName=%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E6%8C%82%E9%92%A9&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|uMu6xK">必选</span> `Sample value: DescribeLifecycleHooks`

The action that you want to perform. Value: DescribeLifecycleHooks.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|OlLpoB">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ScalingGroupId ** <span data-label="purple">string </span><span data-api-tag="require|JfDZkY">必选</span> `Sample value: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group. You can call [DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) to query the scaling group ID.



**LifecycleHookIds.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: sgh-ybrzhc5ht08hccnm****`

The list of lifecycle hook IDs.


* Parameter \- N: Indicates the serial number of the lifecycle hook. Value: 1–20.

* Separate multiple lifecycle hook IDs with &.



**LifecycleHookName ** <span data-label="purple">string </span>`Optional` `Sample value: hook01`

The name of the lifecycle hook.



**PageNumber ** <span data-label="purple">integer </span>`Optional Sample value: 1`

The page number of the list. The default value is 1.



**PageSize**<span data-label="purple"> integer </span>`Optional Sample value: 10`

The number of entries on each page in a pagination query. Valid values: 1–50. Default value: 10.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**LifecycleHooks ** <span data-label="purple">object[] </span>`Sample value: --`

The information on lifecycle hooks that meet the conditions.


**LifecycleHookId ** <span data-label="purple">string </span>`Sample value: sgh-ybrzhc5ht08hccnm****`

The ID of the lifecycle hook.



**ScalingGroupId ** <span data-label="purple">string </span>`String example: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group.



**LifecycleHookName ** <span data-label="purple">string </span>`Sample value: hook01`

The name of the lifecycle hook.



**LifecycleHookTimeout ** <span data-label="purple">integer </span>`Sample value: 30`

The duration for which the ECS instance remains in the suspended state.



**LifecycleHookType ** <span data-label="purple">string </span>`Sample value: SCALE_IN`

The scaling activity type. When a scaling activity of the specified type occurs, a lifecycle hook is triggered and the target ECS instance enters a suspended status. Valid values:


* SCALE_IN: Scale\-in event.

* SCALE_OUT: Scale\-out event.



**LifecycleHookPolicy ** <span data-label="purple">string </span>`Sample value: CONTINUE`

The execution policy after the instance's suspended status ends. Valid values:


* CONTINUE: Execution continues.

* REJECT: Subsequent execution is discontinued.

* ROLLBACK: For scale\-in operations, ECS instances are not released but rolled back. For scale\-out operations, the logic is the same as that of REJECT.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details about the instance change process after execution, see <a href="https://docs.byteplus.com/en/docs/as/Overview-of-lifecycle-hooks#.5omn6KGM5rWB56iL5ZKM562W55Wl">Execution processes and policies</a>.</div>




**LifecycleCommand ** <span data-label="purple">object </span>`Sample value: --`

Information about the cloud assistant command.


**CommandId ** <span data-label="purple">string </span>`Sample value: cmd-4302d02424c5c8e10281e3a31****`

The cloud assistant command ID.



**Parameters ** <span data-label="purple">string </span>`Sample value: "username":"root"`

The custom parameter in the cloud assistant command.





**PageNumber ** <span data-label="purple">integer </span>`Sample value: 1`

The current page number.



**PageSize ** <span data-label="purple">integer </span>`Sample value: 10`

The number of entries per page.



**TotalCount ** <span data-label="purple">integer </span>`Sample value: 20`

The total number of lifecycle hooks that meet the conditions.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeLifecycleHooks&ScalingGroupId=scg-ybmssdnnhn5pkgyd****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T112127Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240507192156069141091045DAD848",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "LifecycleHooks": [
      {
        "LifecycleHookId": "sgh-ybrzhc5ht08hccnm****",
        "ScalingGroupId": "scg-ybmssdnnhn5pkgyd****",
        "LifecycleHookName": "hook01",
        "LifecycleHookTimeout": 30,
        "LifecycleHookType": "SCALE_IN",
        "LifecycleHookPolicy": "CONTINUE",
        "LifecycleCommand": {
          "CommandId": "cmd-4302d02424c5c8e10281e3a31****",
          "Parameters": "\"username\":\"root\""
        }
      }
    ],
    "PageNumber": 1,
    "PageSize": 10,
    "TotalCount": 20
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/as/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.ScalingGroupId |The required parameter ScalingGroupId is not supplied. |The scaling group ID cannot be empty. |
|400 |LimitExceeded.LifecycleHookIds |You've reached the limit on the number of LifecycleHookIds. |The upper limit on the number of lifecycle hook IDs has been reached. |
|404 |InvalidScalingGroupId.NotFound |The specified ScalingGroup [%s] does not exist. |The specified scaling group does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
