---
title: "Expected instance count"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Desire-instance-number-capacity"
---

You can specify an expected instance count or capacity to maintain a fixed number of instances or a fixed amount of capacity in a scaling group. This ensures the instance count or capacity stays consistently fixed throughout the operation. Applicable scenarios:


* When the business remains stable for an extended period, failed instances can be automatically replaced without manual intervention.

* If an adjustment fails, the system automatically retries until the expected instance count or capacity is reached, so no manual retry is required.


<span id=".5pyf5pyb5a6e5L6L5pWwL-WuuemHj-eahOaVsOWAvOiMg-WbtA=="></span>
## Value range of expected instance count or capacity


* The expected instance count or capacity must be greater than or equal to the minimum instance count or capacity and less than or equal to the maximum instance count or capacity.

* The calculation of expected instance count or capacity does not include instances in the scaling group that are in "Disabled" status.


<span id=".5aaC5L2V6K6-572u5pyf5pyb5a6e5L6L5pWwL-WuuemHjw=="></span>
## Specify an expected instance count or capacity

<span id=".5ZCv55So5pyf5pyb5a6e5L6L5pWwL-WuuemHj-WKn-iDvQ=="></span>
### Enable the expected instance count or capacity feature

You can enable this feature by specifying an expected instance count or capacity only when you [create a scaling group](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group). After the scaling group is created, you cannot enable or disable this feature. However, you can modify the expected instance count or capacity.

If you specify an expected instance count or capacity when you create a scaling group, the scaling group will immediately scale out until the expected instance count is reached.

<span id=".5L-u5pS55pyf5pyb5a6e5L6L5pWwL-WuuemHjw=="></span>
### Modify the expected instance count or capacity

You can modify the expected instance count or capacity manually or through an adjustment


|Modification type |Method |Changes to the expected instance count |Sample value |
|---|---|---|---|
|Manual modification |[Modifying expected instance count or capacity of scaling group](https://docs.byteplus.com/en/docs/as/Modifying-the-instance-number-capacity-of-a-scaling-group) |When the scaling group performs a health check again, if the current instance count or capacity in the group does not match the expected value, an adjustment will be executed to ensure the instance count or capacity in the group matches the expected value.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After an adjustment is executed, the actual capacity of the scaling group may be slightly greater than the expected capacity. Reason:</div><br><br><br><div data-tips="true" data-tips-type="tip">If the expected capacity is not perfectly divisible by the weight of the highest\-priority instance type, the value will be rounded up to meet the computing power requirement. For example, if the expected capacity is set to 100 and the weight of the highest\-priority instance type is 30, 4 instances will ultimately be provisioned, resulting in an actual scaling group capacity of 120.</div><br> |* Current instance count/Current expected instance count: 2.<br><br>* Modify the expected instance count to: 3.<br><br>* Result: After the expected instance count is changed to 3, the health check detects an instance count mismatch and scales out by 1 instance. |
|Automatic modification |[Adding instance manually](https://docs.byteplus.com/en/docs/as/Adding-instances-manually) |The expected instance count or capacity is automatically updated to the actual instance count or capacity in the scaling group after manual instance scale\-out is completed. |* Current instance count/Current expected instance count: 2.<br><br>* Manually added instance count: 2.<br><br>* Result: If 2 instances are added, the expected instance count becomes 4. If only 1 instance is added, the expected instance count becomes 3. |
||Specify whether to synchronously modify the expected instance count when instances are manually [removed](https://docs.byteplus.com/en/docs/as/Removing-instances-automatically) or [deleted](https://docs.byteplus.com/en/docs/as/Deleting-instances-manually) |If you specify that the expected instance count is synchronously modified when instances are removed or deleted, the expected instance count or capacity is automatically modified to the actual instance count or capacity in the scaling group when instance scale\-in is completed. |* Current instance count/Current expected instance count: 2.<br><br>* Manually removed instance count: 1.<br><br>* Result: If 1 instance is removed, the expected instance count becomes 1. If no instance is removed, the expected instance count is still 2. |
|||If you specify that the expected instance count is not synchronously modified when instances are removed or deleted, the expected instance count or capacity remains unchanged. When the health check is performed again after instance scale\-in is completed, the scaling group will automatically scale out until the expected instance count or capacity is reached. |* Current instance count/Current expected instance count: 2.<br><br>* Manually removed instance count: 1.<br><br>* Result: If 1 instance is removed, the expected instance count is still 2. In this case, the health check will detect a mismatch between the current instance count and the expected instance count and automatically scale out by 1 instance. |
||Modification triggered by [scaling rules](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-policys) |The expected instance count or capacity will be automatically updated to the anticipated instance count or capacity in the scaling group when adjustments are executed.<br><br>If not all adjustments succeed, the health check will detect a mismatch between the actual instance count or capacity in the group and the expected value. In this case, the scaling group will execute adjustments again to ensure that the actual instance count or capacity matches the expected value. |* Current instance count/Current expected instance count: 2.<br><br>* Planned scale\-out instance count via scaling rules: 1.<br><br>* Result: After the expected instance count becomes 3, 1 instance is scaled out. If the scale\-out fails, the health check will detect a mismatch between the current instance count and the expected instance count and automatically scale out by 1 instance. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Manual modification and manual addition, removal, or deletion of instances are not subject to the <a href="https://docs.byteplus.com/en/docs/as/Cooldown-period">cooldown period</a>.</div>
