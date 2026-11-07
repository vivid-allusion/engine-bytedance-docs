---
title: "Modifying an internet bandwidth limit"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CLB-instances-06"
---

If your public network traffic changes, you can adjust the internet bandwidth limit as needed.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Increasing internet bandwidth will not affect business operation but will increase costs.

* Reducing internet bandwidth may impact running services. Proceed with caution.

* When an EIP associated with a CLB instance has joined a bandwidth package, the modified internet bandwidth limit takes effect only after the EIP is removed from the bandwidth package.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click right side of the target CLB Instances list··· \> Public \> Edit EIP configuration.

4. Set the new maximum Internet bandwidth as needed. Consult and confirm the relevant legal documents according to the console instructions.

5. Click Buy now to complete the modification of the maximum Internet bandwidth.

6. Click Go to console to navigate to the EIP list page and view the bandwidth limit of the target EIP.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [ModifyEipAddressAttributes](https://docs.byteplus.com/en/docs/eip/ModifyEipAddressAttributes)
