---
title: "Binding or unbinding an EIP"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CLB-instances-05"
---

<span id="eDwAsBGl"></span>
## Instructions


* Public CLB instances do not support binding and unbinding Elastic IPs (EIPs).

* Private CLB instances support binding/unbinding an EIP .


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".57uR5a6a5YWs572RSVA="></span>
### Associating EIP

Only one Elastic IP (EIP) can be associated with a CLB instance.


1. Log in to[ the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. In the top menu bar, select the target project and target region.

3. Click  **··· \> Access to Internet \> Associate an EIP** on the right side of the target CLB instance.

4.  select the target EIP from the list below.

5. Click **Confirm** to complete the binding.


<span id=".6Kej57uR5YWs572RSVA="></span>
### Disassociating EIP


1. Log in to[ the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. In the top menu bar, select the target region and target project.

3. Click  **··· \> Access to Internet \> Disassociate an EIP** on the right side of the target CLB instance.

4. Click **OK** to complete the unbinding.


<span id=".55u45YWz5paH5qGj"></span>
## Related document


* [AssociateEipAddress](https://docs.byteplus.com/en/docs/eip/AssociateEipAddress)

* [DisassociateEipAddress](https://docs.byteplus.com/en/docs/eip/DisassociateEipAddress)
