---
title: "CreateScalingPolicy"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/CreateScalingPolicy1"
---

Call CreateScalingPolicy to create a target tracking scaling rule.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic only describes the request parameters required when you create a target tracking scaling rule. All other call configurations remain consistent with standard settings. For more information, see <a href="https://docs.byteplus.com/en/docs/as/CreateScalingPolicy">CreateScalingPolicy</a>.</div>


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Required |Example value |The description. |
|---|---|---|---|---|
|TargetTrackingPolicy.RuleType |String |No |Static |The monitoring metric type of the target tracking scaling rule. Valid value: Static (default), which specifies static monitoring metrics collected by the agent.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is valid and required only when <code>ScalingPolicyType</code> is set to TargetTracking.</div><br> |
|TargetTrackingPolicy.DisableScaleIn |Boolean |No |false |Whether the target tracking scaling rule disables scale\-in. Value:<br><br><br>* false (default): Does not disable scale\-in.<br><br>* true: Disables scale\-in.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>ScalingPolicyType</code> is set to TargetTracking.</div><br> |
|TargetTrackingPolicy.MetricName |String |No |CpuTotal_Avg |The monitoring metric of the target tracking scaling rule. Value:<br><br><br>* Instance_CpuBusy_Avg: The average out\-of\-band CPU utilization.<br><br>* CpuTotal_Avg: The average in\-band CPU usage.<br><br>* Instance_NetTxBits_Avg: The average out\-of\-band network outbound rate.<br><br>* Instance_NetRxBits_Avg: The average out\-of\-band network inbound rate.<br><br>* Instance_NetTxPackets_Avg: The average out\-of\-band network packet sending rate.<br><br>* Instance_NetRxPackets_Avg: The average out\-of\-band network packet receiving rate.<br><br>* MemoryUsedUtilization_Avg: The average in\-band memory usage.<br><br>* GpuUsedUtilization_Avg: The average in\-band GPU usage. |
|TargetTrackingPolicy.MetricUnit |String |No |Percent |The unit of the monitoring metric target value for the target tracking scaling rule. Valid values:<br><br><br>* When the TargetTrackingPolicy.MetricName parameter is set to the average CPU, GPU, or memory usage: Percent.<br><br>* When the AlarmPolicy.Condition.MetricName parameter is set to network inbound/outbound rate: Bits/Second (IEC).<br><br>* When the AlarmPolicy.Condition.MetricName parameter is set to network packet sending/receiving rate: Packet/Second.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>ScalingPolicyType</code> is set to TargetTracking.</div><br> |
|TargetTrackingPolicy.TargetValue |String |No |20 |The target value for the monitoring metric of the target tracking scaling rule. Value:<br><br><br>* When TargetTrackingPolicy.MetricUnit is set to Percent: 1 to 100.<br><br>* When TargetTrackingPolicy.MetricUnit is set to Bits/Second (IEC): an integer greater than 0.<br><br>* When TargetTrackingPolicy.MetricUnit is set to Packet/Second: an integer greater than 0.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>ScalingPolicyType</code> is set to TargetTracking.</div><br> |
|TargetTrackingPolicy.ScaleInEvaluationCount |Integer |No |15 |The number of consecutive threshold breaches required to trigger a scale\-in alert for the target tracking scaling policy. Default value: 15.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>ScalingPolicyType</code> is set to TargetTracking.</div><br> |
|TargetTrackingPolicy.ScaleOutEvaluationCount |Integer |No |3 |The number of consecutive threshold breaches required to trigger a scale\-out alert for the target tracking scaling policy. Default value: 3.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>ScalingPolicyType</code> is set to TargetTracking.</div><br> |
