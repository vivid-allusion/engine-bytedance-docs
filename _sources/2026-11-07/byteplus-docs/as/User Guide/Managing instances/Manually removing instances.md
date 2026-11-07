---
title: "Manually removing instances"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Removing-instances-automatically"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

You can manually remove instances from a scaling group. After removal, the instances will no longer share access traffic, but the instances will be retained and you are charged for the instances.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before you remove instances, confirm the items described in the following table.


|Project |Prerequisites |
|---|---|
|Instance |The instance must be in the **In service** or **Disabled** status. |
|Scaling group |The scaling group must be in the **Running** or **Cooling** status. |


<span id=".5pON5L2c6K-05piO"></span>
## Usage notes


* You can remove up to 20 instances at one time.

* Manually removing instances is not subject to the cooldown time, and you can perform this operation at any time.

* If the number of instances in the scaling group is less than the minimum instance count after removal, an adjustment will be triggered during the next health check to add instances until the minimum instance count is reached.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Instance Management" tab.

4. Select one or more instances to be removed, and click the "Remove from Scaling Group" button.

5. Check or uncheck "Detach instances to Load Balancer (LB), RDS instances, and EIP automatically".

   * If you select the option, the instances will be automatically removed from the load balancer and RDS instance, and the EIP resources will be automatically deleted.

6. If the [expected instance count/capacity](https://docs.byteplus.com/en/docs/as/Desire-instance-number-capacity) feature is enabled for the scaling group, the "Modify Expected Number of Instances/Modify Expected Capacity" option is available.

   * If you select this option, the expected instance count will be automatically updated to the actual instance count in the scaling group after the instances are removed.

   * If you do not select this option, the expected instance count remains unchanged. When the health check is performed again after the instances are removed, the scaling group will automatically scale out until the expected instance count is reached.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Removing "Disabling" instances does not change the desired instance count.   </div>
   

7. Click the "OK" button to complete the operation.


<span id=".56e75Ye65ZCO6LWE5rqQ5Zue5pS2562W55Wl"></span>
## Resource reclaim policy after instance removal

After instances are removed from the scaling group, the Auto Scaling console will no longer display the instances. Whether resources associated with the removed instances are retained depends on whether you have checked "Detach instances to Load Balancer (LB), RDS instances, and EIP automatically".


* If you select the option, the instances will be automatically removed from the Load Balancer and RDS instance, and the EIP resources will be automatically deleted.

* If you do not select the option, the instances, EIPs, and resource association status will be retained, and you can still log in to the corresponding consoles to view the resources.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[DetachInstances](https://docs.byteplus.com/en/docs/as/DetachInstances)
