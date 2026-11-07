---
title: "AttachInstances - Manually adds instances to a scaling group"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/AttachInstances"
---

Manually add one or more instances to a scaling group. For operation instructions and precautions, see [Manually adding instances](https://docs.byteplus.com/en/docs/as/Adding-instances-manually).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=AttachInstances&groupName=%E5%AE%9E%E4%BE%8B%E7%AE%A1%E7%90%86&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|IpeVCT">必选</span> `Sample value: AttachInstances`

The operation that you want to perform. Value: AttachInstances.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|QOi5fT">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ScalingGroupId ** <span data-label="purple">string </span><span data-api-tag="require|opIPbD">必选</span> `Sample value: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group. You can call [DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) to query the scaling group ID.



**InstanceIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|laKo5l">必选</span> `Sample value: i-ybmike5l70l8j1ha****`

The list of instance IDs. You can call [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) to query instance IDs.


* Parameter \- N: Specifies the serial number of the scaling group. Valid value: 1\-20.

* Separate multiple instance IDs with &.



**LifecycleHook ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to trigger the scale\-out lifecycle hook when instances are added to the scaling group. Value range:


* true: Trigger the scale\-out lifecycle hook.

* false (default): Do not trigger the scale\-out lifecycle hook.



**Entrusted ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to place the instance under the management of the scaling group. Valid values:


* true: enable the scaling group to manage the lifecycle of an instance when the instance is added to the scaling group.

* false (default): does not enable the scaling group to manage the lifecycle of an instance when the instance is added to the scaling group.



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
GET /?Action=AttachInstances&InstanceIds.1=i-ybmike5l70l8j1ha****&ScalingGroupId=scg-ybmssdnnhn5pkgyd****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T112932Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240507192941234170194230F2025B",
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
|400 |InvalidInstance.VPCMismatch |The primary network interface of specified Instance [%s] does not match the VPC of the scaling group. |​The network interface of the specified instance does not match the VPC of the scaling group. |
|400 |InvalidInstance.InvalidChargeType |The ChargeType of the specified Instance [%s] does not support this operation. |The billing method of the specified instance does not support this operation. |
|400 |InvalidInstance.InUse |The specified Instance [%s] is already in use. |The specified instance is already in use. |
|400 |IncorrectInstanceNumber.MaxInstanceNumber |The attached ECS instances make Total InstanceNumber exceed MaxInstanceNumber. |Adding ECS instances causes the number of instances in the scaling group to exceed the configured maximum instance count. |
|400 |InvalidOperation.Suspended |The specific operation is rejected by the suspended processes. |The specified operation is rejected by the scaling group suspension process. |
|404 |InvalidInstanceId.NotFound |The specified InstanceId [%s] does not exist. |The specified instance does not exist. |
|404 |InvalidScalingGroupId.NotFound |The specified ScalingGroup [%s] does not exist. |The specified scaling group does not exist. |
|412 |InvalidScalingGroup.LockFailed |The specified operation is denied as the scaling group lock failed. |Failed to lock the scaling group. |
|429 |LimitExceeded.OperateScalingGroupInstances |You've reach the limit on request rate of operating the specified scaling group instances. |Frequent changes are made to instances in the specified scaling group. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
