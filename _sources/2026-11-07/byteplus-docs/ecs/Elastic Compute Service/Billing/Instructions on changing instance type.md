---
title: "Instructions on changing instance type"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Instance-type-change"
---

When the instance type of your Elastic Compute Service (ECS) instance does not meet business requirements, you can upgrade or downgrade the instance configuration.

Real\-time upgrade and downgrade are available for pay\-as\-you\-go and subscription instances. After the change, the new instance configuration will remain in effect until the next modification or resource release.


* Upgrade: The listed price of the new configuration (hourly listed price) ≥ the listed price of the original configuration (hourly listed price).

* Downgrade: The listed price of the new configuration (hourly rate) < the listed price of the original configuration (hourly listed price).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Upon successful change, the platform generates a "Change config" order to indicate the successful configuration change. Then, the instance starts running with the new configuration.</div>



|Item |Pay\-as\-you\-go |Subscription |
|---|---|---|
|Billing rules |The cost for the configuration change is based on the price of the target configuration. The price may vary slightly in different periods, depending on the actual configuration change. (Deduction with coupons is allowed.)<br><br>For configuration changes, the order amount is calculated on an hourly basis, and is accurate to four decimal places. |For more information, refer to [Changing specifications of subscription-based resources](https://docs.byteplus.com/en/docs/byteplus-platform/Billing_Rules_for_Resource_Subscription_Change). |
|Actions guide |Refer to [Changing instance type](https://docs.byteplus.com/en/docs/ecs/Modify-instance-type). ||
|Fee description |The fees displayed in the console shall prevail. ||
|Effective time |After the action succeeds, the system immediately restarts, and the new configuration takes effect in real time. ||
