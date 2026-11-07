---
title: "DescribeScalingPolicies"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/DescribeScalingPolicies1"
---

Call DescribeScalingPolicies to query a target tracking scaling rule.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic only describes the new response parameters when you query a target tracking scaling rule. All other call configurations remain consistent with standard settings. For more information, see <a href="https://docs.byteplus.com/en/docs/as/DescribeScalingPolicies">DescribeScalingPolicies</a>.</div>


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

<span id="ScalingPolicies"></span>
#### ScalingPolicies


|Name |Type |Sample value |The description. |
|---|---|---|---|
|TargetTrackingPolicy |Struct |\- |The detailed information of the target tracking scaling rule. For more information, see the "**TargetTrackingPolicy structure**" table below. |


<span id="TargetTrackingPolicy"></span>
#### TargetTrackingPolicy


|RuleType |String |Static |The type of monitoring metric in the target tracking scaling rule. |
|---|---|---|---|
|DisableScaleIn |Boolean |false |Whether the target tracking scaling rule disables scale\-in. |
|MetricName |String |CpuTotal_Avg |The monitoring metric of the target tracking scaling rule. |
|MetricUnit |String |Percent |The unit of the monitoring metric target value for the target tracking scaling rule. |
|TargetValue |String |20 |The target value for the monitoring metric of the target tracking scaling rule. |
|ScaleInEvaluationCount |Integer |15 |The number of consecutive threshold breaches required to trigger a scale\-in alert for the target tracking scaling policy. |
|ScaleOutEvaluationCount |Integer |3 |The number of consecutive threshold breaches required to trigger a scale\-out alert for the target tracking scaling policy. |
