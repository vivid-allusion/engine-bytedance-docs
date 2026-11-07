---
title: "Enabling scaling group"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Enabling-a-scaling-group"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

You can perform this operation to enable a scaling group.

<span id=".5pON5L2c6K-05piO"></span>
## Usage notes


* After being enabled, the scaling group may immediately trigger scaling operations. You are charged for the new instances.

* You have [associated a scaling configuration source with the scaling group](https://docs.byteplus.com/en/docs/as/Associating-a-scaling-configuration-source-with-a-scaling-group), and the scaling group's scaling policy, subnet, and scaling configuration source meet the following requirements. Otherwise, the scaling group cannot be enabled as expected:

   
   |Scaling policy |Requirements for the subnet and scaling configuration source |
   |---|---|
   |Priority policy |The instance type and image of the scaling configuration source currently associated with the scaling group must be available in the availability zone corresponding to the scaling group’s highest\-priority subnet (that is, the first selected subnet). |
   |Balanced policy |The instance type and image of the scaling configuration source currently associated with the scaling group must be available in the availability zones corresponding to all selected subnets of the scaling group. |
   


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the "Enable" button on the right side of the scaling group that you want to enable.

4. Click the "Confirm" button to complete the operation.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[EnableScalingGroup](https://docs.byteplus.com/en/docs/as/EnableScalingGroup)
