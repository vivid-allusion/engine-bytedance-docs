---
title: "DescribeScalingPolicies - Queries scaling rules"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/DescribeScalingPolicies"
---

Query scaling rules. If there is no matching scaling rule, the non\-matching item will be automatically ignored and the query of other scaling rules will continue.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeScalingPolicies&groupName=%E4%BC%B8%E7%BC%A9%E8%A7%84%E5%88%99&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|DmEJXM">必选</span> `Sample value: DescribeScalingPolicies`

The operation that you want to perform. Valid value: DescribeScalingPolicies.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|fBPiVp">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ScalingGroupId ** <span data-label="purple">string </span><span data-api-tag="require|x5Ozjv">必选</span> `Sample value: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group. You can call [DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) to query the scaling group ID.



**ScalingPolicyIds.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: sp-ybmvamf8uql8j1fl****`

The list of scaling rule IDs.


* Parameter \- N: Specifies the serial number of the scaling rule. Valid values: 1\-10.



**PageNumber ** <span data-label="purple">integer </span>`Optional Sample value: 1`

The page number of the scaling rule list. Default value: 1.



**PageSize**<span data-label="purple"> integer </span>`Optional Sample value: 10`

The number of entries on each page in a pagination query. Valid values: 1–100.

Default value: 10.



**ScalingPolicyNames.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: test-1`

The list of scaling rule names.


* Parameter \- N: Specifies the serial number of the scaling rule. Valid value: 1\-10.



**ScalingPolicyType ** <span data-label="purple">string </span>`Optional` `Sample value: Scheduled`

The type of the scaling rule. Valid values:


* Scheduled: Scheduled task.

* Recurrence: Periodic task.

* Alarm: Alert task.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageNumber ** <span data-label="purple">integer </span>`Sample value: 1`

The current page number.



**PageSize ** <span data-label="purple">integer </span>`Sample value: 10`

The number of entries per page.



**ScalingPolicies ** <span data-label="purple">object[] </span>`Sample value: --`

The information of scaling rules that meet the conditions.


**ScalingGroupId ** <span data-label="purple">string </span>`Sample value: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group to which the scaling rule belongs.



**ScalingPolicyId ** <span data-label="purple">string </span>`Sample value: sp-ybmvamf8uql8j1fl****`

The ID of the scaling rule.



**ScalingPolicyName ** <span data-label="purple">string </span>`Sample value: test-1`

The name of the scaling rule.



**AlarmPolicy ** <span data-label="purple">object </span>`Sample value: --`

The detailed information of the alert task.


**ConditionOperator ** <span data-label="purple">string </span>`Sample value: ||`

The conditions for determining whether a multi\-metric alert is triggered.


* &&: An alert is triggered only when all metrics meet the conditions simultaneously.

* || (default): An alert is triggered when any metric meets the condition.



**Conditions ** <span data-label="purple">object[]</span>

The detailed information of the monitoring metrics for multi\-metric monitoring.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when ScalingPolicyType is set to Alarm.</div>



**Threshold ** <span data-label="purple">string </span>`Sample value: 10`

The threshold of the monitoring metric.



**MetricUnit ** <span data-label="purple">string </span>`Sample value: Percent`

The unit of the monitoring metric threshold. Valid values:


* Percent.

* Bytes/Second(IEC).

* Count/Second.

* Count.

* Bits/Second(IEC).

* Packet/Second.



**MetricName ** <span data-label="purple">string </span>`Sample value: CpuTotal_Max`

The name of the monitoring metric. Valid values:


* CpuTotal_Max: The maximum in\-band CPU usage, which specifies the maximum CPU usage among all instances in the scaling group.

* CpuTotal_Min: The minimum in\-band CPU usage.

* CpuTotal_Avg: The average in\-band CPU usage.

* MemoryUsedUtilization_Max: The maximum in\-band memory usage.

* MemoryUsedUtilization_Min: The minimum in\-band memory usage.

* MemoryUsedUtilization_Avg: The average in\-band memory usage.

* Instance_CpuBusy_Max: The maximum out\-of\-band CPU usage.

* Instance_CpuBusy_Min: The minimum out\-of\-band CPU usage.

* Instance_CpuBusy_Avg: The average out\-of\-band CPU usage.

* Instance_NetTxBits_Avg: The average out\-of\-band network outbound rate.

* Instance_NetRxBits_Avg: The average out\-of\-band network inbound rate.

* Instance_NetTxPackets_Avg: The average out\-of\-band network packet sending rate.

* Instance_NetRxPackets_Avg: The average out\-of\-band network packet receiving rate.

* SystemDiskReadBytes_Avg: The average in\-band system disk read bandwidth.

* SystemDiskWriteBytes_Avg: The average in\-band system disk write bandwidth.

* SystemDiskReadIOPS_Avg: The average in\-band system disk read IOPS.

* SystemDiskWriteIOPS_Avg: The average in\-band system disk write IOPS.

* NetTcpConnection_Avg: The average in\-band TCP connections.



**ComparisonOperator ** <span data-label="purple">string </span>`Sample value: >`

The rule expression object.


* \>: Greater than

* <: Less than

* =: Equal to




**Effective ** <span data-label="purple">string</span>

The effective time period for the alert task.



**EvaluationCount ** <span data-label="purple">integer </span>`Sample value: 3`

The consecutive number of times that the monitoring metric data must meet the threshold to trigger an adjustment.



**RuleType ** <span data-label="purple">string </span>`Sample value: Static`

The type of the alert task. Valid values:


* Static: Static monitoring metrics collected by the agent.



**Condition ** <span data-label="purple">object </span>`Sample value: --`

The detailed information of the monitoring metric for single\-metric monitoring.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when ScalingPolicyType is set to Alarm.</div>



**Threshold ** <span data-label="purple">string </span>`Sample value: 10`

The threshold of the monitoring metric.



**MetricUnit ** <span data-label="purple">string </span>`Sample value: Percent`

The unit of the monitoring metric threshold. Valid values:


* Percent.

* Bytes/Second(IEC).

* Count/Second.

* Count.

* Bits/Second(IEC).

* Packet/Second.



**MetricName ** <span data-label="purple">string </span>`Sample value: CpuTotal_Max`

The name of the monitoring metric. Valid values:


* CpuTotal_Max: The maximum in\-band CPU usage, which specifies the maximum CPU usage among all instances in the scaling group.

* CpuTotal_Min: The minimum in\-band CPU usage.

* CpuTotal_Avg: The average in\-band CPU usage.

* MemoryUsedUtilization_Max: The maximum in\-band memory usage.

* MemoryUsedUtilization_Min: The minimum in\-band memory usage.

* MemoryUsedUtilization_Avg: The average in\-band memory usage.

* Instance_CpuBusy_Max: The maximum out\-of\-band CPU usage.

* Instance_CpuBusy_Min: The minimum out\-of\-band CPU usage.

* Instance_CpuBusy_Avg: The average out\-of\-band CPU usage.

* Instance_NetTxBits_Avg: The average out\-of\-band network outbound rate.

* Instance_NetRxBits_Avg: The average out\-of\-band network inbound rate.

* Instance_NetTxPackets_Avg: The average out\-of\-band network packet sending rate.

* Instance_NetRxPackets_Avg: The average out\-of\-band network packet receiving rate.

* SystemDiskReadBytes_Avg: The average in\-band system disk read bandwidth.

* SystemDiskWriteBytes_Avg: The average in\-band system disk write bandwidth.

* SystemDiskReadIOPS_Avg: The average in\-band system disk read IOPS.

* SystemDiskWriteIOPS_Avg: The average in\-band system disk write IOPS.

* NetTcpConnection_Avg: The average in\-band TCP connections.



**ComparisonOperator ** <span data-label="purple">string </span>`Sample value: >`

The rule expression object.


* \>: Greater than

* <: Less than

* =: Equal to





**AdjustmentValue ** <span data-label="purple">integer </span>`Sample value: 1`

The value for the adjustment.



**Cooldown ** <span data-label="purple">integer </span>`Sample value: 60`

The cooldown time of the scaling rule in seconds.



**ScalingPolicyType ** <span data-label="purple">string </span>`Sample value: Scheduled`

The type of the scaling rule. Valid values:


* Scheduled: Scheduled task.

* Recurrence: Periodic task.

* Alarm: Alert task.



**ScheduledPolicy ** <span data-label="purple">object </span>`Sample value: --`

The detailed information about the scheduled task or periodic task.


**LaunchTime ** <span data-label="purple">string </span>`Sample value: 2022-04-01T16:00Z`

The trigger time of the task. By default, the trigger time is the current time.


* When ScalingPolicyType is set to Scheduled, this parameter specifies the trigger time of the scheduled task.

* When ScalingPolicyType is set to Recurrence:

   * If ScheduledPolicy.RecurrenceType is not specified, the task will be executed only once at the specified date and time.

   * If ScheduledPolicy.RecurrenceType is specified, this parameter specifies the start time of the periodic task.



**RecurrenceEndTime ** <span data-label="purple">string </span>`Sample value: 2022-04-02T16:00Z`

The end time of the periodic task.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid when ScalingPolicyType is set to Recurrence.</div>




**RecurrenceValue ** <span data-label="purple">string </span>`Sample value: 3`

The value for recurring execution of periodic tasks.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid when ScalingPolicyType is set to Recurrence.</div>




**RecurrenceType ** <span data-label="purple">string </span>`Sample value: Daily`

The recurrence cycle of the periodic task. Valid values:


* Daily: Execute once every XX days.

* Weekly: Select specific days of the week to execute once per day.

* Monthly: Select specific dates from XX to XX of each month to execute once per day.

* Cron: Execute based on the specified Cron expression.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid when ScalingPolicyType is set to Recurrence.</div>




**RecurrenceStartTime ** <span data-label="purple">string </span>`Sample value: 2022-04-01T16:00Z`

The start time for executing the periodic task.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid when ScalingPolicyType is set to Recurrence.</div>





**AdjustmentType ** <span data-label="purple">string </span>`Sample value: QuantityChangeInCapacity`

The adjustment of the scaling rule, applicable to simple and step rules. Valid values:


* QuantityChangeInCapacity: Increase or decrease the specified number of instances.

* PercentChangeInCapacity: Increase or decrease the specified percentage of instances.

* TotalCapacity: Adjust the number of instances in the current scaling group to the specified quantity.



**Status ** <span data-label="purple">string </span>`Sample value: Active`

The status of the scaling rule. Valid values:


* Active: enabled.

* Inactive: disabled.




**TotalCount ** <span data-label="purple">integer </span>`Sample value: 20`

The total number of scaling rules that meet the conditions.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeScalingPolicies&ScalingGroupId=scg-ybmssdnnhn5pkgyd****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T111034Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240507191044074190125159D96104",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "PageNumber": 1,
    "PageSize": 10,
    "ScalingPolicies": [
      {
        "ScalingGroupId": "scg-ybmssdnnhn5pkgyd****",
        "ScalingPolicyId": "sp-ybmvamf8uql8j1fl****",
        "ScalingPolicyName": "test-1",
        "AlarmPolicy": {
          "EvaluationCount": 3,
          "RuleType": "Static",
          "Condition": {
            "Threshold": "10",
            "MetricUnit": "Percent",
            "MetricName": "CpuTotal_Max",
            "ComparisonOperator": ">"
          }
        },
        "AdjustmentValue": 1,
        "Cooldown": 60,
        "ScalingPolicyType": "Scheduled",
        "ScheduledPolicy": {
          "LaunchTime": "2022-04-01T16:00Z",
          "RecurrenceEndTime": "2022-04-02T16:00Z",
          "RecurrenceValue": "3",
          "RecurrenceType": "Daily",
          "RecurrenceStartTime": "2022-04-01T16:00Z"
        },
        "AdjustmentType": "QuantityChangeInCapacity",
        "Status": "Active"
      },
    ],
    "TotalCount": 20
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/as/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.ScalingGroupId |The required parameter ScalingGroupId is not supplied. |The scaling group ID cannot be empty. |
|400 |LimitExceeded.ScalingPolicyId |You've reached the limit on the number of ScalingPolicyId. |The number of scaling rule IDs has reached the upper limit. |
|400 |LimitExceeded.ScalingPolicyNames |You've reached the limit on the number of ScalingPolicyNames. |The number of scaling rule names has reached the upper limit. |
|400 |InvalidScalingPolicyType |The specified ScalingPolicyType is unsupported. |The specified scaling rule type is invalid. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
