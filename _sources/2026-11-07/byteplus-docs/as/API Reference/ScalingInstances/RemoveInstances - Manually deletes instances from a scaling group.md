---
title: "RemoveInstances - Manually deletes instances from a scaling group"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/RemoveInstances"
---

Delete instances in a scaling group. For operation instructions and precautions, see [Manually deleting instances](https://docs.byteplus.com/en/docs/as/Deleting-instances-manually).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=RemoveInstances&groupName=%E5%AE%9E%E4%BE%8B%E7%AE%A1%E7%90%86&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|zyN3yf">必选</span> `Sample value: RemoveInstances`

The operation that you want to perform. Valid value: RemoveInstances.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|m3ur10">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ScalingGroupId ** <span data-label="purple">string </span><span data-api-tag="require|UtZpYW">必选</span> `Sample value: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group. You can call [DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) to query the scaling group ID.



**LifecycleHook ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to trigger the scale\-in lifecycle hook when instances are deleted from the scaling group. Value range:


* true: Trigger the scale\-out lifecycle hook.

* false (default): Do not trigger the scale\-out lifecycle hook.



**ForceDelete ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Specifies whether to forcibly delete the instances when `DecreaseDesiredCapacity` is set to false and the number of instances in the scaling group is less than the minimum instance count after instance deletion. Valid value:


* false (default): Do not force delete the instances.

* true: Force delete the instances.



**RemoveMode ** <span data-label="purple">string </span>`Optional` `Sample value: release`

The operation mode for manually deleting instances. Valid values:


* release (default): The selected instances are directly released.

* recycle: The selected instances are changed to "no billing during downtime" mode.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect only when <code>ScalingMode</code> is also set to recycle.</div>


The actual deletion operation depends on the scaling group's instance reclaim mode, `ScalingMode`. You can call [DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) to query the instance reclaim mode of the scaling group.


* When `ScalingMode` is set to release and `RemoveMode` is set to release: The instances are released.

* When `ScalingMode` is set to release and `RemoveMode` is set to recycle: The instances are released.

* When `ScalingMode` is set to recycle and `RemoveMode` is set to release: The instances are released.

* When `ScalingMode` is set to recycle and `RemoveMode` is set to recycle: The instances are changed to "no billing during downtime" mode.



**DecreaseDesiredCapacity ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

Whether to modify the expected instance count. This parameter is valid only when the expected instance count is configured for the selected scaling group.


* true (default): The expected instance count will be automatically updated to the actual instance count in the scaling group after the instances are deleted. For example, if the original expected instance count is 5 and you delete 2 instances, the expected instance count will be changed to 3 after the instances are deleted.

* false: The expected instance count remains unchanged. When the instance count check is performed again after the instances are deleted, the scaling group will automatically scale out until the expected instance count is reached.



**InstanceIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|24D2Na">必选</span> `Sample value: i-ybmike5l70l8j1ha****`

The list of instance IDs. You can call [DescribeScalingInstances](https://docs.byteplus.com/en/docs/as/DescribeScalingInstances) to query the instance IDs in the specified scaling group.


* Parameter \- N: Specifies the serial number of the scaling group. Valid value: 1\-20.

* Separate multiple instance IDs with &.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ScalingActivityId ** <span data-label="purple">string </span>`Sample value: sga-ybn0mwfy1yl8j1f6****`

The ID of the scaling log.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=RemoveInstances&InstanceIds.1=i-ybmike5l70l8j1ha****&ScalingGroupId=scg-ybmssdnnhn5pkgyd****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T112809Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202405071928192410022181941EF6A7",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "ScalingActivityId": "sga-ybn0mwfy1yl8j1f6****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/as/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidInstance.InvalidStatus |The specified Instance [%s] is not in the correct status. |The status of the specified instance does not support this operation. |
|400 |InvalidScalingGroup.InvalidStatus |The specified ScalingGroup is not in the correct status. |The current status of the specified scaling group does not support this operation. |
|400 |MissingParameter.ScalingGroupId |The required parameter ScalingGroupId is not supplied. |The scaling group ID cannot be empty. |
|400 |InvalidInstanceIds.Malformed |The specified amount of InstanceIds is malformed. |The number of specified instance IDs exceeds the upper limit. |
|400 |InvalidRemoveMode.Malformed |The specified RemoveMode is malformed. |The specified RemoveMode is invalid. |
|400 |InvalidInstanceId.RecycleModeMismatch |The specified InstanceId [%s] does not match RecycleMode. |The specified instance does not support the "no billing during downtime" mode. |
|400 |IncorrectInstanceNumber.MinInstanceNumber |The removed or detached ECS instances make Total InstanceNumber less than MinInstanceNumber. |Deleting ECS instances results in the number of instances in the scaling group falling below the configured minimum instance count. |
|400 |InvalidOperation.Suspended |The specific operation is rejected by the suspended processes. |The specified operation is rejected by the scaling group suspension process. |
|404 |InvalidInstanceId.NotFound |The specified InstanceId [%s] does not exist. |The specified instance does not exist. |
|404 |InvalidScalingInstance.NotFound |The specified Instance [%s] does not exsit. |The specified instance does not exist. |
|412 |InvalidScalingGroup.LockFailed |The specified operation is denied as the scaling group lock failed. |Failed to lock the scaling group. |
|429 |LimitExceeded.OperateScalingGroupInstances |You've reach the limit on request rate of operating the specified scaling group instances. |Frequent changes are made to instances in the specified scaling group. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
