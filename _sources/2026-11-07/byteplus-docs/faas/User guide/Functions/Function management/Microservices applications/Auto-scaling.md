---
title: "Auto-scaling"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Elastic_scaling"
---

Microservices applications support custom auto\-scaling policies. You can select the appropriate policies and metrics, set auto\-scaling target values, and based on your business scenario achieve a balance between resource costs and stability. This topic introduces how to configure custom auto\-scaling policies for microservices applications.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For <strong>Event function</strong>, <strong>Web applications</strong>, and <strong>Task</strong> that only allocate CPU on request, FaaS automatically scales based on metrics such as request QPS and resource utilization during request processing, and does not support custom scaling policies.</div>


<span id="background-information"></span>
## Background information

Microservices applications automatically scale based on the trigger conditions configured in the monitoring metric policy, keeping resource utilization near the target value.


* **Calculation rules**

   * Target application instance count = ceil [current instance count × (current metric value / target metric value)]. Ceil represents rounding up.

   * To ensure scaling stability and prevent fluctuations, if the calculated scaling ratio is between [0.9, 1.1], no actual scaling is performed.

* **Example**

   For example, with CPU utilization, assume the target value is set at 50%, and the current instance count is 10.

   * The current utilization is 70%, and the calculated target number of instances = ceil[10\*(70%/50%)] = 14; scale up by 4 instances.

   * The current utilization is 30%, and the calculated target number of instances = ceil[10\*(30%/50%)] = 6; scale down by 4 instances.

   * The current utilization is 55%, and the calculated target number of instances = ceil[10\*(55%/50%)] = 11; the scale ratio is 11/10 = 1.1, to prevent oscillation, no scaling up is performed.

   * The current utilization is 45%, and the calculated target number of instances = ceil(10\*(45%/50%)) = 9; the scale ratio is 9/10 = 0.9, to prevent oscillation, no scaling down is performed.


<span id="prerequisites"></span>
## Prerequisites

Released microservices applications. For specific actions details , refer to [Release function](https://docs.byteplus.com/en/docs/faas/Release_function).

<span id="procedure-steps"></span>
## Procedure steps


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. In the top navigation bar select the region where your business is located.

3. On the **Function** page, find the target function and click the function name.

4. Switch to the **Resource Management** tab. The auto\-scaling policy list comes with a default configured monitoring metrics strategy, which can be modified as needed.

5. Click **Edit** to update the auto\-scaling policy.



|Parameter |Description |
|---|---|
|Policy type |Monitoring metrics strategy. |
|Trigger condition |Configure the trigger conditions for the monitoring metrics strategy. The following indicators and strategies are currently supported; please configure at least one monitoring indicator. The relationship between each indicator is "OR", where satisfying any condition triggers scaling.<br><br><br>* **CPU usage**: The average CPU usage of all instances within 15 seconds is used as the monitoring indicator.<br><br>* **MEM usage**: The average memory usage of all instances within 15 seconds is used as the monitoring indicator.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only one monitoring indicator strategy can be configured. Each indicator can only have one trigger condition configured.</div><br> |
|Configuration preview |* **Auto\-scaling threshold**: Displays the scale\-down and scale\-up thresholds according to your set targets.<br><br>* **Instance number range**: Displays the current upper and lower instance limits configured for microservices applications. The auto\-scaling will not exceed the upper and lower instance limits of the application. For adjusting the range of instance numbers, go to **Resource management \> Maximum resource \> Instance number range**. |



6. After the update, click **Save**.

   You can go to **Monitoring \> Function Instances(Count)**  to observe if the scaling meets expectations.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The modification of the auto\-scaling policy configuration is not constrained by the current state of the application, but the adjusted policy will only take effect when the application is in the <strong>Enabling</strong> state.   </div>
