---
title: "Manually deleting instances"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Deleting-instances-manually"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

You can delete instances in scaling groups by using the Auto Scaling (AS) console or Elastic Compute Service (ECS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites

Before you delete an instance, confirm the items described in the following table.


|Project |Prerequisites |
|---|---|
|Instance |The instance must be in the **In service** or **Disabled** status. |
|Scaling group |The scaling group must be in the **Running** or **Cooling** status. |


<span id=".5pON5L2c6K-05piO"></span>
### Usage notes


* To delete multiple instances at one time, instance protection must be disabled for the instances. You can delete up to 20 instances at one time.

* Instances with instance protection enabled cannot be deleted.

* Manual deletion of instances is not subject to cooldown time restrictions. You can manually delete instances at any time. Deleted instances cannot be recovered. Proceed with caution.

* If the instance count or capacity of the scaling group is less than the minimum instance count or capacity of the scaling group after you delete instances, deletion is not allowed.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Instance Management" tab.

4. Select one or more instances to be deleted, and click the "Delete" button.

5. Select the instance reclaim mode.

   * Release mode: Instances are deleted, and no resources are retained.

   * Stop\-and\-Reclaim Mode: Instances are stopped and switched to Economical Mode. Computing resources (vCPU, GPU, and memory) are reclaimed, but to avoid data loss, the volume, image, EIP, and bandwidth (in fixed bandwidth mode) are retained. For detailed introduction to Economical Mode, refer to [Instance Stop Mode](https://docs.byteplus.com/en/docs/ecs/Stopping-instances#.5YGc5q2i5qih5byP).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In addition to deleting instances, you can also configure the instance reclaim mode for the scaling group. The rule is that Release Mode takes precedence over Stop\-and\-Reclaim Mode. If either the instance or the scaling group is set to Release Mode, the instance is released.   </div>
   

   6. If the [expected instance count/capacity](https://docs.byteplus.com/en/docs/as/Desire-instance-number-capacity) feature is enabled for the scaling group, the "Modify Expected Number of Instances/Modify Expected Capacity" option is available.

   * If you select this option, the expected instance count will be automatically updated to the actual instance count in the scaling group after the instances are deleted. For example, if the original expected instance count is 5 and you delete 2 instances, the expected instance count will be changed to 3 after the instances are deleted.

   * If you do not select this option, the expected instance count remains unchanged. When the health check is performed again after the instances are deleted, the scaling group will automatically scale out until the expected instance count is reached.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Deleting instances in "Disabling" state does not change the expected number of instances.   </div>
   

   7. Click the "OK" button to complete the operation.


<span id=".5Yig6Zmk5ZCO6LWE5rqQ5Zue5pS2562W55Wl"></span>
### Resource reclamation policy after deletion

After instances are deleted from the scaling group, the Auto Scaling console will no longer display the instances. However, whether the resources of the deleted instances are retained depends on the [lifecycle management](https://docs.byteplus.com/en/docs/as/Instance-lifecycle#.5a6e5L6L55Sf5ZG95ZGo5pyf566h55CG) method in the scaling group. Specifically:


* Instances whose lifecycle is **managed** by the scaling group: After you delete the instances from the scaling group, the instance will be automatically deleted, along with associated resources, such as the EIPs, volumes, and network interfaces. The instances will be removed from the associated load balancer and RDS database instances.

   > Since EBS Volume involves the security of your business data, only the System Volume and Data Volumes specified to be released with the instance in the [scaling configuration source](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-configuration-sources) are released.   
   

* Instances whose lifecycle is **not managed** by the scaling group: The instances will be removed from the scaling group, and the instances, associated resources, and resource association status will be retained. You can still log in to the corresponding console to view the resources.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[RemoveInstances](https://docs.byteplus.com/en/docs/as/RemoveInstances)
