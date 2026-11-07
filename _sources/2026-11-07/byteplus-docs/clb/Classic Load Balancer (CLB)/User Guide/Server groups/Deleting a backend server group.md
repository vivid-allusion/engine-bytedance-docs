---
title: "Deleting a backend server group"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Deleting-the-server-group"
---

<span id="1tCUkV63"></span>
## Prerequisites


* The affiliated Classic Load Balancer (CLB) instance does not have Modification Protection enabled.

* The backend server group is not associated with a listener.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the target CLB instance name.

4. On the Server Group tab, click the delete icon on the right side of the target server group.

5. Click **Delete** to complete the action.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After deleting the backend server group, the ECS instances still exist. If you no longer require these ECS instances, please delete them on the ECS side. For detailed steps, please see <a href="https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances">Deleting an ECS instance</a>.   </div>
   

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[DeleteServerGroup](https://docs.byteplus.com/en/docs/clb/DeleteServerGroup)
