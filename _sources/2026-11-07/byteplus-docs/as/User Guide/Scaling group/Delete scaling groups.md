---
title: "Delete scaling groups"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Deleting-a-scaling-group"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

You can perform this operation to delete a scaling group. Deletion is irreversible. If you need to use the scaling group later, we recommend that you [disable the scaling group](https://docs.byteplus.com/en/docs/as/Disabling-a-scaling-group).

<span id=".5pON5L2c6K-05piO"></span>
## Usage notes


* For instances **with instance protection disabled** and whose lifecycle is **managed** by the scaling group: When you delete the scaling group, the instances and their associated resources, such as EIPs, volumes, and network interfaces, will be deleted at the same time. The instances will also be removed from the load balancer and RDS database instances.

* For instances with **instance protection enabled** or **standby status enabled**, or instances whose lifecycle is **not managed** by the scaling group: When the scaling group is deleted, the instances will only be removed from the group, while the instances themselves, their associated resources, and resource association status will be retained. For more information, see [Instance lifecycle](https://docs.byteplus.com/en/docs/as/Instance-lifecycle).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the "Delete" button on the right side of the scaling group you want to delete.

4. Click "Delete" to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[DeleteScalingGroup](https://docs.byteplus.com/en/docs/as/DeleteScalingGroup)
