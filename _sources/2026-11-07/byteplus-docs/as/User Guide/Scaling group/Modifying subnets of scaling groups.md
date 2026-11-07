---
title: "Modifying subnets of scaling groups"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Modifying-the-subnets-of-a-scaling-group"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

After you create a scaling group, you can modify the subnets to which the instances in the scaling group belong.

<span id=".5pON5L2c6K-05piO"></span>
## Usage notes


* At least one subnet must be selected for a single scaling group, and only one subnet can be selected in the same availability zone.

* Different scaling policies support slightly different subnets, as described in the following table. You need to select a subnet that meets the applicable restrictions. Otherwise, you will fail to modify the subnet or start the scaling group.

   
   |Scaling policy |Subnet restriction |
   |---|---|
   |Priority policy |The instance type and image of the scaling configuration currently associated with the scaling group must belong to the availability zone corresponding to the subnet with the highest priority (that is, the first selected subnet). |
   |Balanced policy |The instance type and image of the scaling configuration currently associated with the scaling group must belong to the availability zone corresponding to any selected subnet. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By default, "Priority policy" is assigned to scaling groups with a single subnet created before June 6, 2022.   </div>
   

* After you add a subnet, existing instances will not change their subnet. After you delete a subnet, when the scaling group automatically scales in, instances in the deleted subnet will be removed first.

* To modify the priorities of subnets, deselect and then reselect them. The first subnet selected has the highest priority.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Overview" tab.

4. Click the "Modify Subnet" button to reselect the subnet.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">We recommend that you select subnets with "Normal stock" to improve the success rate of scale\-out. The platform determines the stock based on the following logic:   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The instance type with the highest specification in the availability zone is used as the criterion. If the instance type with the highest specification has normal stock, it is displayed as normal stock. If the instance type with the highest specification has low stock, it is displayed as low stock. If the instance type with the highest specification is sold out, it is displayed as sold out.   </div>
   

   5. Click the "OK" button to complete the operation.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ModifyScalingGroup](https://docs.byteplus.com/en/docs/as/ModifyScalingGroup)
