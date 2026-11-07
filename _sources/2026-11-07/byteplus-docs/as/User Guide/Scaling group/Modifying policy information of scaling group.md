---
title: "Modifying policy information of scaling group"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Modifying-the-multiAZ-policy-of-a-scaling-group"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

After a scaling group is created, you can modify its scaling policy and instance removal policy, but you cannot modify the mode for reclaiming instances.

<span id=".5pON5L2c6K-05piO"></span>
## Usage notes


* Modifying the scaling policy of a scaling group does not affect existing instances. It only affects instances created or removed in subsequent adjustments. For more information, see [Automatically scaling out instances](https://docs.byteplus.com/en/docs/as/Adding-instances-automatically#.5omp57yp5a65562W55Wl6K-05piO) and [Automatically scaling in instances](https://docs.byteplus.com/en/docs/as/Removing-instances-manually#.5omp57yp5a65562W55Wl6K-05piO).

* Modifying the instance removal policy of a scaling group takes effect immediately. The scaling group will follow the new policy the next time instances are removed.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Overview" tab.

4. Click the "Configuration policy" button in the "Policy information" section to select a new policy.

5. Click Confirm to complete the operation.


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[ModifyScalingGroup](https://docs.byteplus.com/en/docs/as/ModifyScalingGroup)
