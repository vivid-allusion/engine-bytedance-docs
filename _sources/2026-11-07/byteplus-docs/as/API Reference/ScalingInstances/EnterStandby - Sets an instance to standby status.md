---
title: "EnterStandby - Sets an instance to standby status"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/EnterStandby"
---

Set an ECS instance in a scaling group to standby status. For more information, see [Setting instances to standby status](https://docs.byteplus.com/en/docs/as/Setting-instance-standby).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=EnterStandby&groupName=%E5%AE%9E%E4%BE%8B%E7%AE%A1%E7%90%86&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|8ALM9q">必选</span> `Sample value: EnterStandby`

The operation that you want to perform. Valid value: EnterStandby.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|Z6jv0B">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**InstanceIds.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: i-ybmike5l70l8j1ha****`

The instance ID. You can call [DescribeScalingInstances](https://docs.byteplus.com/en/docs/as/DescribeScalingInstances) to query instance IDs.


* Parameter \- N: Specifies the serial number of the instance. Valid value: 1–20.

* Separate multiple instance IDs with &.



**ScalingGroupId ** <span data-label="purple">string </span><span data-api-tag="require|eH4Zud">必选</span> `Sample value: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 333456899ff****`

ClientToken is used to ensure the idempotency of the request. The client can automatically generate a token, but you need to ensure that it is unique across requests. This prevents duplicate operations caused by multiple retries when the API request times out or an internal server error occurs. Values:


* Not more than 64 ASCII characters.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=EnterStandby&ScalingGroupId=scg-ybmssdnnhn5pkgyd****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T112538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240507192544216205087112979139",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {}
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
|404 |InvalidInstanceId.NotFound |The specified InstanceId [%s] does not exist. |The specified instance does not exist. |
|404 |InvalidScalingGroupId.NotFound |The specified ScalingGroup [%s] does not exist. |The specified scaling group does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
