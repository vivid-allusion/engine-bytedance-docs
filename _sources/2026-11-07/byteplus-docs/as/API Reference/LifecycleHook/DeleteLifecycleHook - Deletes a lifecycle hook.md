---
title: "DeleteLifecycleHook - Deletes a lifecycle hook"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/DeleteLifecycleHook"
---

Delete a lifecycle hook. For operation instruction and precautions, see [Deleting lifecycle hooks](https://docs.byteplus.com/en/docs/as/Deleting-a-lifecycle-hook).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteLifecycleHook&groupName=%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E6%8C%82%E9%92%A9&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|q3ksvi">必选</span> `Sample value: DeleteLifecycleHook`

The action that you want to perform. Value: DeleteLifecycleHook.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|YiX9iI">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**LifecycleHookId ** <span data-label="purple">string </span><span data-api-tag="require|xaCWPK">必选</span> `Sample value: sgh-ybrzhc5ht08hccnm****`

The ID of the lifecycle hook. You can call [DescribeLifecycleHooks](https://docs.byteplus.com/en/docs/as/DescribeLifecycleHooks) to query the lifecycle hook ID.



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
GET /?Action=DeleteLifecycleHook&LifecycleHookId=sgh-ybrzhc5ht08hccnm****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T112053Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202405071921002020410910771C7C61",
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
|400 |InvalidScalingGroup.InvalidStatus |The specified ScalingGroup is not in the correct status. |The current status of the specified scaling group does not support this operation. |
|400 |MissingParameter.LifecycleHookId |The required parameter LifecycleHookId is not supplied. |The lifecycle hook ID cannot be empty. |
|404 |InvalidLifecycleHookId.NotFound |The specified LifecycleHookId does not exist. |The specified lifecycle hook ID does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
