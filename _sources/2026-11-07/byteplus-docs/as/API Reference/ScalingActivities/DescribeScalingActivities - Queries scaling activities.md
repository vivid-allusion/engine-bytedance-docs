---
title: "DescribeScalingActivities - Queries scaling activities"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/DescribeScalingActivities"
---

Query scaling logs.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeScalingActivities&groupName=%E4%BC%B8%E7%BC%A9%E6%97%A5%E5%BF%97&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|hJliYd">必选</span> `Sample value: DescribeScalingActivities`

The action that you want to perform. Value: DescribeScalingActivities.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|cw8jL8">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ScalingGroupId ** <span data-label="purple">string </span><span data-api-tag="require|3uLjYy">必选</span> `Sample value: scg-yblhryq64wgh9zmp****`

The ID of the scaling group. You can call [DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) to query the scaling group ID.



**EndTime ** <span data-label="purple">string </span>`Optional` `Sample value: 2021-09-06T07:40Z`

The end date of the scaling log.



**PageNumber ** <span data-label="purple">integer </span>`Optional Sample value: 1`

The page number of the list. The default value is 1.



**PageSize**<span data-label="purple"> integer </span>`Optional Sample value: 10`

The number of entries on each page in a pagination query. Valid values: 1–50. Default value: 10.



**ScalingActivityIds.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: sga-ybn0mwfy1yl8j1f6****`

The list of scaling log IDs.


* Parameter \- N: Specifies the serial number of the scaling log. Valid value: 1\-20.

* Separate multiple scaling logs with ampersands (&).



**StartTime ** <span data-label="purple">string </span>`Optional` `Sample value: 2021-09-06T07:37Z`

The start date of the scaling log.



**StatusCode ** <span data-label="purple">string </span>`Optional` `Sample value: Success`

The execution result in the scaling log. Valid values:


* Init: Initialization.

* Running: Running.

* Success: Success.

* PartialSuccess: Partial success.

* Error: All failed.

* Rejected: Denied execution.

* Exception: Exception.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageNumber ** <span data-label="purple">integer </span>`Sample value: 1`

The current page number.



**PageSize ** <span data-label="purple">integer </span>`Sample value: 10`

The number of entries per page.



**ScalingActivities ** <span data-label="purple">object[] </span>`Sample value: --`

Information on scaling logs that meet the conditions.


**ScalingActivityId ** <span data-label="purple">string </span>`Sample value: sga-ybn0mwfy1yl8j1f6****`

The ID of the scaling log.



**CreatedAt ** <span data-label="purple">string </span>`Sample value: 2022-05-11T03:15:26Z`

The start time in the scaling log.



**ExpectedRunTime ** <span data-label="purple">string </span>`Sample value: 2022-05-11T03:15:24Z`

The scheduled execution time in the scaling log.



**ScalingGroupId ** <span data-label="purple">string </span>`String example: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group.



**ResultMsg ** <span data-label="purple">string </span>`Sample value: This is a scaling log.`

Description of the scaling log.



**MaxInstanceNumber ** <span data-label="purple">integer </span>`Sample value: 100`

The maximum number of instances in the scaling group.



**MinInstanceNumber ** <span data-label="purple">integer </span>`Sample value: 10`

The minimum number of instances in the scaling group.



**CurrentInstanceNumber ** <span data-label="purple">integer </span>`Sample value: 20`

The number of instances currently running in the scaling group.



**ActualAdjustInstanceNumber ** <span data-label="purple">integer </span>`Sample value: 3`

The actual adjusted instance count in the scaling log.



**Cooldown ** <span data-label="purple">integer </span>`Sample value: 300`

The cooldown time in the scaling log after execution completion.



**StatusCode ** <span data-label="purple">string </span>`Sample value: Init`

The execution result in the scaling log. Valid values:


* Init: Initialization.

* Running: Running.

* Success: Success.

* PartialSuccess: Partial success.

* Error: All failed.

* Rejected: Denied execution.

* Exception: Exception.



**RelatedInstances ** <span data-label="purple">object[]</span>

Instance\-related information in the scaling log.


**Message ** <span data-label="purple">string </span>`Sample value: Error.`

Description or error information.



**InstanceId ** <span data-label="purple">string </span>`Sample value: i-ybmike5l70l8j1ha****`

The instance ID.



**OperateType ** <span data-label="purple">string </span>`Sample value: Add`

The instance\-targeted adjustment type. Valid values:


* Add: Increases instances.

* Remove: Removes instances.



**Status ** <span data-label="purple">string </span>`Sample value: Success`

The scaling status of the instance. Valid values:


* Success: Success.

* Error: An error occurred.




**ActivityType ** <span data-label="purple">string </span>`Sample value: SCALE_OUT`

The scaling log type. Valid values:


* SCALE_OUT: Scale\-out.

* SCALE_IN: Scale\-in.

* SYNC_INSTANCES: Instance state synchronization.



**StoppedAt ** <span data-label="purple">string </span>`Sample value: 2022-05-11T03:15:51Z`

The stop time in the scaling log.



**TaskCategory ** <span data-label="purple">string </span>`Sample value: Manual`

The operation type in the scaling log. Valid values:


* Manual: Manual execution.

* Scheduled: Scheduled execution.

* Recurrence: Periodic execution.

* Alarm: Alert task.

* HealthCheck: Health check.




**TotalCount ** <span data-label="purple">integer </span>`Sample value: 100`

The total number of scaling logs that meet the conditions.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeScalingActivities&ScalingGroupId=scg-yblhryq64wgh9zmp****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T113028Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240507193036074006150039D52A15",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "PageNumber": 1,
    "PageSize": 10,
    "ScalingActivities": [
      {
        "ScalingActivityId": "sga-ybn0mwfy1yl8j1f6****",
        "CreatedAt": "2022-05-11T03:15:26Z",
        "ExpectedRunTime": "2022-05-11T03:15:24Z",
        "ScalingGroupId": "scg-ybmssdnnhn5pkgyd****",
        "ResultMsg": "This is a scaling activity.",
        "MaxInstanceNumber": 100,
        "MinInstanceNumber": 10,
        "CurrentInstanceNumber": 20,
        "ActualAdjustInstanceNumber": 3,
        "Cooldown": 300,
        "StatusCode": "Init",
        "RelatedInstances": [
          {
            "Message": "Error.",
            "InstanceId": "i-ybmike5l70l8j1ha****",
            "OperateType": "Add",
            "Status": "Success"
          }
        ],
        "ActivityType": "SCALE_OUT",
        "StoppedAt": "2022-05-11T03:15:51Z",
        "TaskCategory": "Manual"
      }
    ],
    "TotalCount": 100
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/as/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.ScalingGroupId |The required parameter ScalingGroupId is not supplied. |The scaling group ID cannot be empty. |
|400 |InvalidScalingActivityStartTime.Malformed |The specified ScalingActivity StartTime is malformed. |The specified start time of the scaling activity is invalid. |
|400 |InvalidScalingActivityEndTime.Malformed |The specified ScalingActivity EndTime is malformed. |The specified end time of the scaling activity is invalid. |
|400 |LimitExceeded.ScalingActivityIds |You've reached the limit on the number of ScalingActivityIds that you can set. |The number of scaling activity IDs reaches the upper limit. |
|404 |InvalidScalingGroupId.NotFound |The specified ScalingGroup [%s] does not exist. |The specified scaling group does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
