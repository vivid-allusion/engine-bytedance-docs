---
title: "DetachDBInstances - Removes RDS instances"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/DetachDBInstances"
---

Disassociate one or multiple RDS instances from a scaling group.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|MtKSzo">必选</span> `Sample value: DetachDBInstances`

The action that you want to perform. Value: DetachDBInstances.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|VqmjL6">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ScalingGroupId ** <span data-label="purple">string </span><span data-api-tag="require|w7YTQs">必选</span> `Sample value: scg-3ty5i3vde54bwbh5****`

The scaling group ID.



**DBInstanceIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|6t2FPP">必选</span> `Sample value: rds-mysql-42b38c76****`

The ID of the RDS instance.


* Parameter \- N: Indicates the serial number of the RDS instance. Valid range: 1–40.

* Separate the port numbers of multiple RDS instances with &.



**ForceDetach ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Specifies whether to remove private IP addresses of all instances in the current scaling group from the IP allowlist of the RDS instance: Valid values:


* true: Removes

* false (default): Does not remove



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
GET /?Action=DetachDBInstances&DBInstanceIds.1=rds-mysql-42b38c76%2A%2A%2A%2A&ScalingGroupId=scg-3ty5i3vde54bwbh5****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T093925Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "2024050717393318821420014248180F",
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
|400 |MissingParameter.DBInstanceId |The required parameter DBInstanceId is empty. |RDS instance ID cannot be empty. |
|400 |LimitExceeded.DBInstanceIds |You've reached the limit on the number of DBInstanceIds that you can attach. |The upper limit on the number of associable RDS databases is reached. |
|404 |InvalidScalingGroupId.NotFound |The specified ScalingGroup [%s] does not exist. |The specified scaling group does not exist. |
|404 |InvalidDBInstanceId.NotFound |The specified DBInstanceId [%s] does not exist. |The specified RDS instance ID does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
