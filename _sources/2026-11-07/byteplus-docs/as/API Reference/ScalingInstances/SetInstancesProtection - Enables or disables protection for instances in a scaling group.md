---
title: "SetInstancesProtection - Enables or disables protection for instances in a scaling group"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/SetInstancesProtection"
---

You can set instances that you do not want to be automatically deleted or removed in a scaling group to protected status. For operation instructions and precautions, see [Configuring instance protection](https://docs.byteplus.com/en/docs/as/Setting-instance-scale-in-protection).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=SetInstancesProtection&groupName=%E5%AE%9E%E4%BE%8B%E7%AE%A1%E7%90%86&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|lY0xkj">必选</span> `Sample value: SetInstancesProtection`

The operation that you want to perform. Valid value: SetInstancesProtection.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|nJhcRr">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ScalingGroupId ** <span data-label="purple">string </span><span data-api-tag="require|oXk7xM">必选</span> `Sample value: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group. You can call [DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) to query the scaling group ID.



**InstanceIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|q4jegV">必选</span> `Sample value: i-ybmike5l70l8j1ha****`

The list of instance IDs. You can call [DescribeScalingInstances](https://docs.byteplus.com/en/docs/as/DescribeScalingInstances) to query the instance IDs in the specified scaling group.


* Parameter \- N: Specifies the serial number of the scaling group. Valid value: 1\-20.

* Separate multiple instance IDs with &.



**ProtectedFromScaleIn ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

The instance protection status.


* true: Enable instance protection.

* false (default): Disable instance protection.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceProtectionResults ** <span data-label="purple">object[] </span>`Sample value: --`

The result of setting instance protection for each instance.


**Code ** <span data-label="purple">string </span>`Sample value: InvalidInstance.NotFound`

The error code that occurs when enabling or disabling protection for the instances fails. Valid values:


* InvalidInstance.NotFound

* ErrUnProtectedPrePaidInstance

* ErrProtectInstanceStatusInvalid


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A return value is provided only when <code>Result</code> is set to Fail.</div>




**InstanceId ** <span data-label="purple">string </span>`Sample value: i-ybmike5l70l8j1ha`

The instance ID.



**Message ** <span data-label="purple">string </span>`Sample value: The specified instance [i-ybmike5l70l8j1ha****] does not exist.`

The error message that appears when enabling or disabling instance protection for the instances fails. Valid values:


* When `Code` is set to InvalidInstance.NotFound: The specified instance [%s] does not exist.

* When `Code` is set to ErrProtectInstanceStatusInvalid: The current status of the instance does not support this operation.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A return value is provided only when <code>Result</code> is set to Fail.</div>




**Result ** <span data-label="purple">string </span>`Sample value: Success`

The result of enabling or disabling protection for the instances. Valid values:


* Success: Succeeded.

* Fail: Failed.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=SetInstancesProtection&InstanceIds.1=i-ybmike5l70l8j1ha****&ScalingGroupId=scg-ybmssdnnhn5pkgyd****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T112722Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202405071927290150451670784B245B",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "InstanceProtectionResults": [
      {
        "Code": "InvalidInstance.NotFound",
        "InstanceId": "i-ybmike5l70l8j1ha",
        "Message": "The specified instance [i-ybmike5l70l8j1ha****] does not exist.",
        "Result": "Success"
      }
    ]
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
|400 |MissingParameter.InstanceIds |The required parameter InstanceIds is not supplied. |The instance ID cannot be empty. |
|400 |InvalidInstanceIds.Malformed |The specified amount of InstanceIds is malformed. |The number of specified instance IDs exceeds the upper limit. |
|404 |InvalidInstanceId.NotFound |The specified InstanceId [%s] does not exist. |The specified instance does not exist. |
|404 |InvalidScalingGroupId.NotFound |The specified ScalingGroup [%s] does not exist. |The specified scaling group does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again. If multiple attempts fail, submit a ticket. |
