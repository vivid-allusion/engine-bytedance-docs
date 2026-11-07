---
title: "ModifyScalingPolicy - Modifies a scaling rule"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/ModifyScalingPolicy"
---

Modify a scaling rule. If optional parameters are not provided, they will not be modified.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyScalingPolicy&groupName=%E4%BC%B8%E7%BC%A9%E8%A7%84%E5%88%99&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|2TCJCt">必选</span> `Sample value: ModifyScalingPolicy`

The operation that you want to perform. Valid value: ModifyScalingPolicy.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|Rsg81J">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**AlarmPolicy.Effective ** <span data-label="purple">string </span>`Optional` `Sample value: \* * 3-5 * *`

The effective time period for the alert task.


* If you do not configure this parameter, it is effective at all times.

* To take effect at a specific time, please use the [Cron expression](https://docs.byteplus.com/en/docs/as/Cron-expressions) configuration, suitable for scenarios such as disabling scale\-in during peak business hours.



**ScalingPolicyId ** <span data-label="purple">string </span><span data-api-tag="require|rDLqyT">必选</span> `Sample value: sp-ybmvamf8uql8j1fl****`

The ID of the scaling rule. You can call [DescribeScalingPolicies](https://docs.byteplus.com/en/docs/as/DescribeScalingPolicies) to query the scaling rule ID.



**ScalingPolicyName ** <span data-label="purple">string </span>`Optional` `Sample value: test-policy`

The name of the scaling rule.



**AdjustmentType ** <span data-label="purple">string </span>`Optional` `Sample value: QuantityChangeInCapacity

`

The adjustment of the scaling rule, applicable to simple and step rules. Valid values:


* QuantityChangeInCapacity: Increase or decrease the specified number of instances.

* PercentChangeInCapacity: Increase or decrease the specified percentage of instances.

* TotalCapacity: Adjust the number of instances in the current scaling group to the specified quantity.



**AdjustmentValue ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

The value for the adjustment, applicable to simple rules and step rules. Valid values:


* When the AdjustmentType parameter is set to QuantityChangeInCapacity: \-100 to 100. 0 is not allowed. Unit: instances.

* When the AdjustmentType parameter is set to PercentChangeInCapacity: \-100 to 10000. 0 is not allowed. Unit: %.

* When the AdjustmentType parameter is set to TotalCapacity: The default value ranges from 0 to 100. Unit: instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The maximum number of instances that can be adjusted in a single call to this operation must not exceed 300.</div>




**Cooldown ** <span data-label="purple">integer </span>`Optional` `Sample value: 60`

The cooldown time of the scaling rule. Valid value: 0\-86400. Unit: seconds.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the cooldown time of the scaling rule conflicts with that of the scaling group, the cooldown time of the scaling rule takes precedence.</div>




**ScheduledPolicy.LaunchTime ** <span data-label="purple">string </span>`Optional` `Sample value: 2023\-02\-28T11:00Z

`

The trigger time of the task.


* When ScalingPolicyType is set to Scheduled, this parameter specifies the trigger time of the scheduled task.

* When ScalingPolicyType is set to Recurrence:

   * If ScheduledPolicy.RecurrenceType is not specified, the task will be executed only once at the specified date and time.

   * If ScheduledPolicy.RecurrenceType is specified, this parameter specifies the start time of the periodic task.

   * You can select a time within 90 days from the date of creation or modification.

* This parameter is invalid when ScalingPolicyType is set to Alarm.



**ScheduledPolicy.RecurrenceEndTime ** <span data-label="purple">string </span>`Optional` `Sample value: 2023-06-28T11:00Z`

The end time of the periodic task. Only a time within 365 days from the creation date is supported. Set to empty to indicate that this task will never stop.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid when ScalingPolicyType is set to Recurrence.</div>




**ScheduledPolicy.RecurrenceType ** <span data-label="purple">string </span>`Optional` `Sample value: Daily`

The recurrence cycle of the periodic task. Valid values:


* Daily: Execute once every XX days.

* Weekly: Select specific days of the week to execute once per day.

* Monthly: Select specific dates from XX to XX of each month to execute once per day.

* Cron: Execute based on the specified Cron expression.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid when ScalingPolicyType is set to Recurrence.</div>




**ScheduledPolicy.RecurrenceValue ** <span data-label="purple">string </span>`Optional` `Sample value: 3`

The value for recurring execution of periodic tasks.


* When the ScheduledPolicy.RecurrenceType parameter is set to Daily, only one value can be specified. Valid value: 1\-31.

* When the ScheduledPolicy.RecurrenceType parameter is set to Weekly, multiple values can be specified, separated by English commas (,). The corresponding values for Monday to Sunday are 1, 2, 3, 4, 5, 6, 7 in sequence.

* When the ScheduledPolicy.RecurrenceType parameter is set to Monthly, the format must be A\-B. The valid range for both A and B is 1\-31, and the value of B must be greater than or equal to the value of A.

* When the ScheduledPolicy.RecurrenceType parameter is set to Cron, the time is based on UTC+8. It supports a 5\-field expression covering minute, hour, day, month, and weekday, and allows the use of the following wildcards: English comma (,), English question mark (?), hyphen (\-), asterisk (\*), hash (#), slash (/), as well as L and W.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid when ScalingPolicyType is set to Recurrence.</div>




**AlarmPolicy.RuleType ** <span data-label="purple">string </span>`Optional` `Sample value: Static`

The type of the alert task. Valid values:


* Static: Static monitoring metrics collected by the agent.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid and required only when ScalingPolicyType is set to Alarm.</div>




**AlarmPolicy.EvaluationCount ** <span data-label="purple">integer </span>`Optional` `Sample value: 3`

The consecutive number of times that the monitoring metric data must meet the threshold to trigger an adjustment. Valid value: 1\-180.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid and required only when ScalingPolicyType is set to Alarm.</div>




**AlarmPolicy.Condition.MetricName ** <span data-label="purple">string </span>`Optional` `Sample value: CpuTotal_Max`

The monitoring metric name for single\-metric alert. Valid values:


* CpuTotal_Max: The maximum in\-band CPU usage, which specifies the maximum CPU usage among all instances in the scaling group.

* CpuTotal_Min: The minimum in\-band CPU usage.

* CpuTotal_Avg: The average in\-band CPU usage.

* MemoryUsedUtilization_Max: The maximum in\-band memory usage.

* MemoryUsedUtilization_Min: The minimum in\-band memory usage.

* MemoryUsedUtilization_Avg: The average in\-band memory usage.

* Instance_CpuBusy_Max: The maximum out\-of\-band CPU utilization.

* Instance_CpuBusy_Min: The minimum out\-of\-band CPU utilization.

* Instance_CpuBusy_Avg: The average out\-of\-band CPU utilization.

* Instance_NetTxBits_Avg: The average out\-of\-band network outbound rate.

* Instance_NetRxBits_Avg: The average out\-of\-band network inbound rate.

* Instance_NetTxPackets_Avg: The average out\-of\-band network packet sending rate.

* Instance_NetRxPackets_Avg: The average out\-of\-band network packet receiving rate.

* SystemDiskReadBytes_Avg: The average in\-band system disk read bandwidth.

* SystemDiskWriteBytes_Avg: The average in\-band system disk write bandwidth.

* SystemDiskReadIOPS_Avg: The average in\-band system disk read IOPS.

* SystemDiskWriteIOPS_Avg: The average in\-band system disk write IOPS.

* NetTcpConnection_Avg: The average in\-band TCP connections.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>ScalingPolicyType</code> is set to Alarm, and you must configure the relevant parameters for <code>AlarmPolicy.Condition.x</code> or <code>AlarmPolicy.Conditions.x</code>. If both parameters are configured, only <code>AlarmPolicy.Conditions.x</code> takes effect.</div>




**AlarmPolicy.Condition.Threshold ** <span data-label="purple">string </span>`Optional` `Sample value: 10`

The monitoring metric threshold for single\-metric alert. Valid values:


* When AlarmPolicy.Condition.MetricUnit is set to Percent: 1\-100.

* When AlarmPolicy.Condition.MetricUnit is set to Bytes/Second (IEC): an integer greater than 0.

* When AlarmPolicy.Condition.MetricUnit is set to Count/Second: an integer greater than 0.

* When AlarmPolicy.Condition.MetricUnit is set to Count: an integer greater than 0.

* When AlarmPolicy.Condition.MetricUnit is set to Bits/Second (IEC): an integer greater than 0.

* When AlarmPolicy.Condition.MetricUnit is set to Packet/Second: an integer greater than 0.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>ScalingPolicyType</code> is set to Alarm, and you must configure the relevant parameters for <code>AlarmPolicy.Condition.x</code> or <code>AlarmPolicy.Conditions.x</code>. If both parameters are configured, only <code>AlarmPolicy.Conditions.x</code> takes effect.</div>




**AlarmPolicy.Condition.MetricUnit ** <span data-label="purple">string </span>`Optional` `Sample value: Percent`

The unit of the threshold for monitoring metrics in single\-metric alerts. Valid values:


* When the AlarmPolicy.Condition.MetricName parameter is set to CPU/memory usage: Percent.

* When the AlarmPolicy.Condition.MetricName parameter is set to system disk read/write bandwidth: Bytes/Second (IEC).

* When the AlarmPolicy.Condition.MetricName parameter is set to system disk read/write IOPS: Count/Second.

* When the AlarmPolicy.Condition.MetricName parameter is set to TCP connections: Count.

* When the AlarmPolicy.Condition.MetricName parameter is set to network inbound/outbound rate: Bits/Second (IEC).

* When the AlarmPolicy.Condition.MetricName parameter is set to network packet rate: Packet/Second.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>ScalingPolicyType</code> is set to Alarm, and you must configure the relevant parameters for <code>AlarmPolicy.Condition.x</code> or <code>AlarmPolicy.Conditions.x</code>. If both parameters are configured, only <code>AlarmPolicy.Conditions.x</code> takes effect.</div>




**AlarmPolicy.Condition.ComparisonOperator ** <span data-label="purple">string </span>`Optional` `Sample value: \>`

The rule expression object for single\-metric alerts.


* \>: Greater than

* <: Less than

* =: equal to


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>ScalingPolicyType</code> is set to Alarm, and you must configure the relevant parameters for <code>AlarmPolicy.Condition.x</code> or <code>AlarmPolicy.Conditions.x</code>. If both parameters are configured, only <code>AlarmPolicy.Conditions.x</code> takes effect.</div>




**AlarmPolicy.Conditions.N.MetricName ** <span data-label="purple">string[] </span>`Optional` `Sample value: CpuTotal_Max`

The monitoring metric names in multi\-metric alerts.


* Valid values:

   * CpuTotal_Max: The maximum in\-band CPU usage.

   * CpuTotal_Min: The minimum in\-band CPU usage.

   * CpuTotal_Avg: The average in\-band CPU usage.

   * Instance_NetTxBits_Avg: The average out\-of\-band network outbound rate.

   * Instance_NetRxBits_Avg: The average out\-of\-band network inbound rate.

   * Instance_NetTxPackets_Avg: The average out\-of\-band network packet sending rate.

   * Instance_NetRxPackets_Avg: The average out\-of\-band network packet receiving rate.

   * MemoryUsedUtilization_Max: The maximum in\-band memory usage.

   * MemoryUsedUtilization_Min: The minimum in\-band memory usage.

   * MemoryUsedUtilization_Avg: The average in\-band memory usage.

   * Instance_CpuBusy_Max: The maximum out\-of\-band CPU utilization.

   * Instance_CpuBusy_Min: The minimum out\-of\-band CPU utilization.

   * Instance_CpuBusy_Avg: The average out\-of\-band CPU utilization.

   * SystemDiskReadBytes_Avg: The average in\-band system disk read bandwidth.

   * SystemDiskWriteBytes_Avg: The average in\-band system disk write bandwidth.

   * SystemDiskReadIOPS_Avg: The average in\-band system disk read IOPS.

   * SystemDiskWriteIOPS_Avg: The average in\-band system disk write IOPS.

   * NetTcpConnection_Avg: The average in\-band TCP connections.

* Parameter \- N: specifies the serial number of the metric. Valid value: 1 \- 5.

* Separate multiple instance types with &.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>ScalingPolicyType</code> is set to Alarm, and you must configure the relevant parameters for <code>AlarmPolicy.Condition.x</code> or <code>AlarmPolicy.Conditions.x</code>. If both parameters are configured, only <code>AlarmPolicy.Conditions.x</code> takes effect.</div>




**AlarmPolicy.Conditions.N.MetricUnit ** <span data-label="purple">string[] </span>`Optional` `Sample value: Percent`

The unit of the threshold for monitoring metrics in multi\-metric alerts.


* Valid values:

   * When the AlarmPolicy.Conditions.MetricName parameter is set to CPU/memory usage: Percent.

   * When the AlarmPolicy.Conditions.MetricName parameter is set to system disk read/write bandwidth: Bytes/Second (IEC).

   * When the AlarmPolicy.Conditions.MetricName parameter is set to system disk read/write IOPS: Count/Second.

   * When the AlarmPolicy.Conditions.MetricName parameter is set to TCP connections: Count.

   * When the AlarmPolicy.Condition.MetricName parameter is set to network inbound/outbound rate: Bits/Second (IEC).

   * When the AlarmPolicy.Condition.MetricName parameter is set to network packet rate: Packet/Second.

* Parameter \- N: specifies the serial number of the metric. Valid value: 1 \- 5.

* Separate multiple instance types with &.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>ScalingPolicyType</code> is set to Alarm, and you must configure the relevant parameters for <code>AlarmPolicy.Condition.x</code> or <code>AlarmPolicy.Conditions.x</code>. If both parameters are configured, only <code>AlarmPolicy.Conditions.x</code> takes effect.</div>




**AlarmPolicy.Conditions.N.Threshold ** <span data-label="purple">string[] </span>`Optional` `Sample value: 10`

The threshold for monitoring metrics in multi\-metric alerts.


* Valid values:

   * When AlarmPolicy.Conditions.MetricUnit is set to Percent: 1\-100.

   * When AlarmPolicy.Conditions.MetricUnit is set to Bytes/Second (IEC): an integer greater than 0.

   * When AlarmPolicy.Conditions.MetricUnit is set to Count/Second: an integer greater than 0.

   * When AlarmPolicy.Conditions.MetricUnit is set to Count: an integer greater than 0.

   * When AlarmPolicy.Condition.MetricUnit is set to Bits/Second (IEC): an integer greater than 0.

   * When AlarmPolicy.Condition.MetricUnit is set to Packet/Second: an integer greater than 0.

* Parameter \- N: specifies the serial number of the metric. Valid value: 1 \- 5.

* Separate multiple instance types with &.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>ScalingPolicyType</code> is set to Alarm, and you must configure the relevant parameters for <code>AlarmPolicy.Condition.x</code> or <code>AlarmPolicy.Conditions.x</code>. If both parameters are configured, only <code>AlarmPolicy.Conditions.x</code> takes effect.</div>




**AlarmPolicy.Conditions.N.ComparisonOperator ** <span data-label="purple">string[] </span>`Optional` `Sample value: \>`

The rule expression object for multi\-metric alerts.


* \>: greater than

* <: Less than

* =: equal to


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>ScalingPolicyType</code> is set to Alarm, and you must configure the relevant parameters for <code>AlarmPolicy.Condition.x</code> or <code>AlarmPolicy.Conditions.x</code>. If both parameters are configured, only <code>AlarmPolicy.Conditions.x</code> takes effect.</div>




**AlarmPolicy.ConditionOperator ** <span data-label="purple">string </span>`Optional` `Sample value: ||`

The conditions for determining whether a multi\-metric alert is triggered.


* &&: An alert is triggered only when all metrics meet the conditions simultaneously.

* || (default): An alert is triggered when any metric meets the condition.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>ScalingPolicyType</code> is set to Alarm and the relevant parameters for <code>AlarmPolicy.Conditions.x</code> are configured.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ScalingPolicyId ** <span data-label="purple">string </span>`Sample value: sp-ybmvamf8uql8j1fl****`

The ID of the scaling rule.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ModifyScalingPolicy&ScalingPolicyId=sp-ybmvamf8uql8j1fl****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T095835Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240507175843180059214177607C07",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "ScalingPolicyId": "sp-ybmvamf8uql8j1fl****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/as/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.ScalingPolicyId |The required parameter ScalingPolicyId is not supplied. |The scaling rule ID cannot be empty. |
|400 |InvalidCooldown.Malformed |The specified Cooldown is malformed. |The specified cooldown time is invalid. |
|400 |MissingParameter.ScheduledPolicyRecurrenceEndTime |The required parameter ScheduledPolicy RecurrenceEndTime is not supplied. |The end time of the periodic task cannot be empty. |
|400 |InvalidElasticScheduledInstanceType.ScalingGroupUnsupported |The specified ElasticScheduledInstanceType is unsupported with the ScalingGroup. |The scaling group does not support the specified Elastic Scheduled Instance type. |
|400 |InvalidScalingPolicyType.ScheduledInstanceMismatch |The scaling policy type is mismatch with scheduled instance. |The specified scaling rule type does not support Elastic Scheduled Instances (ESIs). |
|400 |InvalidScheduledPolicyRecurrenceType |The specified ScheduledPolicy RecurrenceType is unsupported. |The specified recurrence type for the periodic task is invalid. |
|400 |InvalidAlarmPolicyRuleType |The specified AlarmPolicy RuleType is unsupported. |The alert metric type configured in the specified alert policy is invalid. |
|400 |InvalidScheduledPolicy.RecurrenceValue |The specified ScheduledPolicy RecurrenceValue is malformed. |The specified recurrence value for the periodic task is invalid. |
|400 |InvalidScheduledPolicyRecurrenceEndTime.Malformed |The specified ScheduledPolicy RecurrenceEndTime is malformed. |The specified end time for the periodic task is invalid. |
|400 |InvalidScheduledPolicyRecurrenceStartTime.Malformed |The specified ScheduledPolicy RecurrenceStartTime is malformed. |The specified start time for the periodic task is invalid. |
|400 |InvalidScheduledPolicyLaunchTime.Malformed |The specified ScheduledPolicy LaunchTime is malformed. |The specified trigger time is invalid. |
|400 |InvalidAlarmPolicyConditionComparisonOperator |The specified AlarmPolicy Condition ComparisonOperator is unsupported. |The specified ComparisonOperator in the alert policy is not supported. |
|400 |InvalidAlarmPolicyConditionThreshold.Malformed |The specified AlarmPolicy Condition Threshold is malformed. |The specified monitoring metric threshold in the alert policy is invalid. |
|400 |InvalidAlarmPolicyConditionMetricName.Malformed |The specified AlarmPolicy Condition MetricName is malformed. |The specified monitoring metric in the alert policy is invalid. |
|400 |MissingParameter.AlarmPolicyCondition |The required parameter AlarmPolicy Condition is not supplied. |The trigger conditions for the alert policy cannot be empty. |
|400 |InvalidAlarmPolicy.EvaluationCount |The specified AlarmPolicy EvaluationCount is malformed. |The number of times the scaling rule is triggered by monitoring is invalid. |
|400 |InvalidAdjustmentType |The specified AdjustmentType is unsupported. |The adjustment specified by the scaling rule is not supported. |
|400 |LimitExceeded.AdjustmentValue |You've reached the limit on the size of AdjustmentValue. |The adjustment value has reached the limit. |
|400 |InvalidScalingPolicyType |The specified ScalingPolicyType is unsupported. |The specified scaling rule type is invalid. |
|400 |LimitExceeded.ScalingPolicyName |You've reached the limit on the length of ScalingPolicyName. |The scaling rule name has reached the upper limit in length. |
|400 |InvalidScalingPolicyName.Malformed |The specified ScalingPolicyName is malformed. |The specified scaling rule name is invalid. |
|400 |InvalidAlarmPolicyConditionMetricUnit.Malformed |The specified AlarmPolicy Condition MetricUnit is malformed. |The unit of the monitoring metric threshold specified in the alert policy is invalid. |
|400 |InvalidScheduledInstancePolicyStartDeliveryTime.Malformed |The specified ScheduledInstancePolicy StartDeliveryTime is malformed. |The specified start time for delivering Elastic Scheduled Instances (ESIs) is invalid. |
|400 |InvalidScheduledInstancePolicyEndDeliveryTime.Malformed |The specified ScheduledInstancePolicy EndDeliveryTime is malformed. |The specified end time for delivering Elastic Scheduled Instances (ESIs) is invalid. |
|400 |InvalidScheduledInstancePolicyAutoReleaseTime.Malformed |The specified ScheduledInstancePolicy AutoReleaseTime is malformed. |The specified automatic release time for Elastic Scheduled Instances (ESIs) is invalid. |
|400 |InvalidElasticScheduledInstanceType.Malformed |The specified ElasticScheduledInstanceType is malformed. |The specified ESI type is invalid. |
|400 |InvalidDeliveryType.Malformed |The specified DeliveryType is malformed. |The specified ESI delivery type is invalid. |
|400 |MissingParameter.HpcClusterId |The specified InstanceType [%s] required parameter HpcClusterId. |You must specify the ID of the HPC cluster for the specified instance type. |
|400 |InvalidAlarmPolicy.ModifyFailed |The specified AlarmPolicy is failed to modify on CloudMonitor. |Alert rule modification failed on the Cloud Monitor side. |
|400 |InvalidTargetTrackingPolicy.ScaleInEvaluationCount |The specified TargetTrackingPolicy ScaleInEvaluationCount is malformed. |The number of times the target tracking scaling rule triggers scaling in is invalid. |
|400 |InvalidTargetTrackingPolicy.ScaleOutEvaluationCount |The specified TargetTrackingPolicy ScaleOutEvaluationCount is malformed. |The number of times the target tracking scaling rule triggers scaling out is invalid. |
|400 |InvalidTargetTrackingPolicyMetricName.Malformed |The specified TargetTrackingPolicy MetricName is malformed. |The alert metrics configured for the target tracking scaling rule are not supported. |
|400 |InvalidTargetTrackingPolicyMetricUnit.Malformed |The specified TargetTrackingPolicy MetricUnit is malformed. |The alert metric unit configured for the target tracking scaling rule is invalid. |
|400 |InvalidTargetTrackingPolicyTargetValue.Malformed |The specified TargetTrackingPolicy TargetValue is malformed. |The target value of the target tracking scaling rule is invalid. |
|400 |InvalidTargetTrackingPolicyRuleType.Malformed |The specified TargetTrackingPolicy RuleType is malformed. |The alert metric type configured for the target tracking scaling rule is invalid. |
|400 |LimitExceeded.AlarmPolicyConditions |You've reached the limit on the number of AlarmPolicy Conditions. |The number of monitoring alert rules has reached the upper limit. |
|400 |InvalidAlarmPolicy.RuleType |The specified AlarmPolicy RuleType is malformed. |The alert metric type configured in the specified alert policy is invalid. |
|404 |InvalidScalingPolicyId.NotFound |The specified ScalingPolicyId does not exist. |The specified scaling rule ID does not exist. |
|409 |InvalidScalingPolicyName.Conflict |The specified ScalingPolicyName already exists. |The specified scaling rule name already exists. |
|409 |InvalidAlarmPolicyConditionMetricName.Conflict |The specified AlarmPolicy Condition MetricName already exists. |The specified alert metric is duplicated. |
|412 |OperationDenied.ResourceLocked |The specified operation is denied as your resource is locked for another operation. |The specified operation is rejected because your resource has been locked by another operation. |
|412 |InvalidHpcCluster.InstanceTypeIdMismatch |The specified HpcClusterId does not match the InstanceTypeId [%s]. |The specified HPC cluster ID does not match the instance type. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
