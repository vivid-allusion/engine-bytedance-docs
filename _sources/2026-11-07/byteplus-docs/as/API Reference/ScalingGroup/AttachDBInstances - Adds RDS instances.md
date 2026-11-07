---
title: "AttachDBInstances - Adds RDS instances"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/AttachDBInstances"
---

Associate one or multiple RDS instances with a scaling group.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|RechaI">必选</span> `Sample value: AttachDBInstances`

The action that you want to perform. Value: AttachDBInstances.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|UPN0E9">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ScalingGroupId ** <span data-label="purple">string </span><span data-api-tag="require|TJkgu4">必选</span> `Sample value: scg-3ty5i3vde54bwbh****`

The ID of the scaling group.



**DBInstanceIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|HGrFRq">必选</span> `Sample value: rds-mysql-42b38c76****`

The list of RDS instance IDs.


* Parameter \- N: Indicates the serial number of the RDS instance. Valid range: 1–40.

* Separate the port numbers of multiple database instances with &.



**ForceAttach ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

Specifies whether to add private IPs of all instances in the current scaling group to the IP allowlist of the RDS instance:


* true: Adds

* false (default): Does not add



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ScalingGroupId ** <span data-label="purple">string </span>`Sample value: scg-3ty5i3vde54bwbh5****`

The ID of the scaling group.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=AttachDBInstances&DBInstanceIds.1=rds-mysql-42b38c76****&ScalingGroupId=scg-3ty5i3vde54bwbh****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T094003Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240507174010025154061064E2B8B9",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "ScalingGroupId": "scg-3ty5i3vde54bwbh5****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/as/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidScalingGroup.InvalidStatus |The specified ScalingGroup is not in the correct status. |The current status of the specified scaling group does not support this operation. |
|400 |MissingParameter.ScalingGroupId |The required parameter ScalingGroupId is not supplied. |The scaling group ID cannot be empty. |
|400 |MissingParameter.DBInstanceIds |The required parameter DBInstanceIds is not supplied. |The list of RDS instance IDs cannot be empty. |
|400 |LimitExceeded.DBInstanceIds |You've reached the limit on the number of DBInstanceIds that you can attach. |The upper limit on the number of associable RDS databases is reached. |
|400 |MissingParameter.DBInstanceId |The required parameter DBInstanceId is empty. |RDS instance ID cannot be empty. |
|400 |InvalidDBInstanceId.InvalidStatus |The specified DBInstance [%s] is not in the correct status. |The status of the specified RDS instance is not supported. |
|400 |InvalidDBInstanceID.InvalidVersion |The specified DBInstance [%s] is not in the correct WhiteList Version. |The specified RDS instance version is not supported. |
|404 |InvalidScalingGroupId.NotFound |The specified ScalingGroup [%s] does not exist. |The specified scaling group does not exist. |
|404 |InvalidDBInstanceId.NotFound |The specified DBInstanceId [%s] does not exist. |The specified RDS instance ID does not exist. |
|409 |InvalidDBInstanceId.Conflict |The specified DBInstanceId [%s] already exists. |The specified RDS instance ID exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
