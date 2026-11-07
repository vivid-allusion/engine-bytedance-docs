---
title: "Deleting NLB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Deleting-NLB-instance"
---

<span id="操作场景"></span>
## Operation scenario

If you no longer use the NLB instance, you can release resources by deleting to save costs.

<span id="操作说明"></span>
## Instructions


* When deleting an NLB instance, the system will automatically disassociate resources (for example, server group, security group) and remove all listeners of the NLB instance.

* Resources cannot be recovered after deleting the NLB instance, proceed with caution.

* When deleting an NLB instance, the specific changes to its associated network resources are summarized in the table below.

   
   |Network resources associated with the instance |Public instance |Private instance |
   |---|---|---|
   |Network interface |All private IPv4 and IPv6 addresses of the NLB instance have been deallocated, and its network interfaces have been deleted. ||
   |EIP  |* The Elastic IP (EIP) added to the Shared Bandwidth Package has been removed from the Shared Bandwidth Package.<br><br>* The new Elastic IP (EIP) along with the NLB instance will be automatically disassociated and deleted when the instance is removed.<br><br>* The existing Elastic IP (EIP) associated with the NLB instance is automatically disassociated but will not be deleted. Description of the Elastic IP (EIP) has been modified to empty, and its name has been changed to the instance ID of the Elastic IP (EIP). |\-\- |
   |IPv6 Internet Bandwidth |* The IPv6 Internet bandwidth that was part of the Shared Bandwidth Package is removed from the Shared Bandwidth Package.<br><br>* IPv6 Internet Bandwidth is deleted. |\-\- |
   


<span id="操作步骤"></span>
## Procedure


1. Log in to the [NLB Console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target region and target project.

3. Click the  **··· \> Delete** button on the right side of the target NLB instance, confirm the resource information, and input **Confirm delete**.

4. Click the **Confirm delete** button to complete the action.


<span id="相关文档"></span>
## Related documents

[DeleteNetworkLoadBalancer](https://docs.byteplus.com/en/docs/clb/DeleteNetworkLoadBalancer)
