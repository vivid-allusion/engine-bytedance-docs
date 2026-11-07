---
title: "Scaling rule overview"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Overview-of-scaling-policys"
---

Scaling rules define the conditions and methods that trigger scaling actions, such as rule type, trigger time, scaling action, and cooldown time.

For the same scaling group, you can configure multiple scaling rules of different types. When the predefined conditions of any one rule are met, the scaling group initiates scaling adjustment. However, if different types of rules are triggered at the same time, the adjustment triggered manually will be executed first.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">All <a href="https://docs.byteplus.com/en/docs/as/Adjustment-types">adjustment types</a> other than those triggered manually are mutually competitive. Only the one triggered first will be executed.</div>


<span id=".5Ly457yp6KeE5YiZ57G75Z6L"></span>
## Scaling rule type


* Scheduled task: The system automatically scales in or out instances at a specified time, suitable for expected large\-scale events, such as major promotional events or the broadcast of trending news.

* Periodic task: Executed automatically at fixed times on a daily, weekly, or monthly basis. This feature is applicable to long\-term regular business scenarios, such as monthly end\-of\-month settlements or daily scheduled ticket sales.

* Alert task: Based on instance monitoring metrics, this feature is integrated with [Cloud Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/Release-notes) and detects whether the instance status meets expectations to achieve dynamic scaling. It is applicable to sudden or unpredictable business scenarios, such as breaking news.

* Target tracking: This feature is integrated with [Cloud Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/Release-notes), which allows you to select a monitoring metric based on your operational experience and specify a target value for it. The platform automatically calculates the number of instances to add or remove during scaling, thereby keeping the specified metric close to the target value.


<span id=".5Ly457yp6KGM5Li6"></span>
## Adjustment

When the trigger conditions are met, a scaling group supports scale\-out, scale\-in, and fixed\-capacity adjustment operations.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The specified number must be within the minimum and maximum instance count range or minimum and maximum capacity range, and is not allowed to exceed these limits. For example, if the scaling group is configured with a maximum instance count of 3 and a minimum instance count of 1, and the group currently has 2 running instances, when a scale\-out of 2 instances is needed at a fixed time, only 1 instance will be added in the end.</div>


* <div data-tips="true" data-tips-type="tip">If the scaling group has the feature of <a href="https://docs.byteplus.com/en/docs/as/Desire-instance-number-capacity">/capacity</a><a href="https://docs.byteplus.com/en/docs/as/Desire-instance-number-capacity">/capacity</a> enabled, the expected instance count will be automatically updated to the anticipated instance count/capacity in the scaling group when adjustments are executed.</div>



<span id=".5Ya35Y205pe26Ze0"></span>
## Cooldown time

Auto Scaling prioritizes the cooldown time of the scaling rule over that of the scaling group. For a detailed description, refer to [Cooldown time](https://docs.byteplus.com/en/docs/as/Cooldown-period).
