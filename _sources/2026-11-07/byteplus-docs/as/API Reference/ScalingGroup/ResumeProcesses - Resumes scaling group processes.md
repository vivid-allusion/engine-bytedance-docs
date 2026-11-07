---
title: "ResumeProcesses - Resumes scaling group processes"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/ResumeProcesses"
---

Resume paused processes in a scaling group. About [Pausing/Resuming scaling group processes](https://docs.byteplus.com/en/docs/as/suspensionresumption-of-scaling-group-processes).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ResumeProcesses&groupName=%E4%BC%B8%E7%BC%A9%E7%BB%84&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|bGiOLP">必选</span> `Sample value: ResumeProcesses`

The action that you want to perform. Value: ResumeProcesses.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|OHN3qG">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ScalingGroupId ** <span data-label="purple">string </span><span data-api-tag="require|JJvXEL">必选</span> `Sample value: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group. You can call [DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) to query the scaling group ID.



**Processes.N ** <span data-label="purple">string[] </span><span data-api-tag="require|9eylnB">必选</span> `Sample value: ScaleIn`

Specifies the type of process to be resumed.


* Parameter \- N: Indicates the serial number of the process type. Value range: 1 ~ 5.

* Separate multiple process types with &. Valid values:

   * ScaleIn: Scale\-in process.

   * ScaleOut: Scale\-out process.

   * HealthCheck: Health check.

   * AlarmNotification: Alert task.

   * ScheduledAction: Scheduled task.



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
GET /?Action=ResumeProcesses&Processes.1=ScaleIn&ScalingGroupId=scg-ybmssdnnhn5pkgyd****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T092822Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240507172833057015127244C5888F",
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
|400 |MissingParameter.ScalingGroupId |The required parameter ScalingGroupId is not supplied. |The scaling group ID cannot be empty. |
|400 |MissingParameter.Processes |The required parameter Processes is not supplied. |The required parameter Processes cannot be empty. |
|400 |InvalidProcess.Malformed |The specified Process is malformed. |The specified process is invalid. |
|404 |InvalidScalingGroupId.NotFound |The specified ScalingGroup [%s] does not exist. |The specified scaling group does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
