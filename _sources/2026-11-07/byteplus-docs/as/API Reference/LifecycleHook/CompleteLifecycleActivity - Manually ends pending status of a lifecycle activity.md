---
title: "CompleteLifecycleActivity - Manually ends pending status of a lifecycle activity"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/CompleteLifecycleActivity"
---

Manually end the suspended status of a lifecycle activity. For instructions and precautions, refer to [Manually ending suspension](https://docs.byteplus.com/en/docs/as/Ending-the-pending-state-of-instances-manually).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=CompleteLifecycleActivity&groupName=%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E6%8C%82%E9%92%A9&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|N1PDA5">必选</span> `Sample value: CompleteLifecycleActivity`

The action that you want to perform. Value: CompleteLifecycleActivity.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|MK6chR">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 333456899ff****`

ClientToken is used to ensure the idempotency of the request. The client can automatically generate a token, but you need to ensure that it is unique across requests. This prevents duplicate operations caused by multiple retries when the API request times out or an internal server error occurs. Values:


* Not more than 64 ASCII characters.



**LifecycleHookId ** <span data-label="purple">string </span>`Optional` `Sample value: sgh-ybrzhc5ht08hccnm****`

The ID of the lifecycle hook. You can call [DescribeLifecycleHooks](https://docs.byteplus.com/en/docs/as/DescribeLifecycleHooks) to query the lifecycle hook ID.



**LifecycleActivityId ** <span data-label="purple">string </span><span data-api-tag="require|mj97qJ">必选</span> `Sample value: sgha-ybw2idr7kogsnzd9****`

The ID of the lifecycle activity. You can call [DescribeLifecycleActivities](https://docs.byteplus.com/en/docs/as/DescribeLifecycleActivities) to query the lifecycle activity ID.



**LifecycleActivityPolicy ** <span data-label="purple">string </span>`Optional` `Sample value: CONTINUE`

The execution policy after the instance's suspended status ends. When this parameter is not provided, the policy of the associated lifecycle hook is used. Valid values:


* CONTINUE: Execution continues.

* REJECT: Subsequent adjustment is discontinued.

* ROLLBACK: For scale\-in operations, ECS instances are not released but rolled back. For scale\-out operations, the logic is the same as that of REJECT.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details about the instance change process after execution, see <a href="https://docs.byteplus.com/en/docs/as/Overview-of-lifecycle-hooks#.5omn6KGM5rWB56iL5ZKM562W55Wl">Execution processes and policies</a>.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceId ** <span data-label="purple">string </span>`Sample value: i-ybmike5l70l8j1ha****`

The instance ID.



**LifecycleActivityId ** <span data-label="purple">string </span>`Sample value: sgha-ybw2idr7kogsnzd9****`

The ID of the lifecycle activity.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=CompleteLifecycleActivity&LifecycleActivityId=sgha-ybw2idr7kogsnzd9****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T111847Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240507191856180215118241AEA56D",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "InstanceId": "i-ybmike5l70l8j1ha****",
    "LifecycleActivityId": "sgha-ybw2idr7kogsnzd9****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/as/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |The request uses the same client token as a previous, but non\-identical request.Do not reuse a client token with different requests, unless the requests are identical. |The idempotent parameters are inconsistent. |
|400 |MissingParameter.LifecycleActivityId |The required parameter LifecycleActivityId is not supplied. |The lifecycle activity ID cannot be empty. |
|400 |InvalidLifecycleHookPolicy.Malformed |The specified LifecycleHookPolicy is malformed. |The specified lifecycle hook policy is invalid. |
|400 |InvalidLifecycleActivityStatus.Completed |The specified LifecycleActivity is already completed. |The specified lifecycle activity was completed. |
|404 |InvalidLifecycleActivityId.NotFound |The specified LifecycleActivityId does not exist. |The specified lifecycle activity ID does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
