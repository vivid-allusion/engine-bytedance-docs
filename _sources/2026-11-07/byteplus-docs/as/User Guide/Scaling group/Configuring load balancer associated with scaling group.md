---
title: "Configuring load balancer associated with scaling group"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Configuring-the-load-balancer-associated-with-a-scaling-group"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

After you create a scaling group, you can modify the associated load balancer and backend server group at any time.

<span id=".5pON5L2c6K-05piO"></span>
## Usage notes

Changes take effect immediately. Any new instance added to the scaling group will be automatically synchronized to the backend server group.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To modify instances that already exist in the scaling group, move them out of the scaling group and add them again so they can be automatically synchronized to the backend server group.</div>


* <div data-tips="true" data-tips-type="tip">If you need to modify the port or weight of a backend server group, you must first remove it from the scaling group and then re\-add it.</div>



<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Overview" tab.

4. Click the "Configuring Classic Load Balancer (CLB)" or "Configuring an ALB Server Group" button to reconfigure the Classic Load Balancer (CLB) or Application Load Balancer (ALB).

5. Click the "Confirm" button to confirm the modification.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [AttachServerGroups](https://docs.byteplus.com/en/docs/as/AttachServerGroups)

* [DetachServerGroups](https://docs.byteplus.com/en/docs/as/DetachServerGroups)
