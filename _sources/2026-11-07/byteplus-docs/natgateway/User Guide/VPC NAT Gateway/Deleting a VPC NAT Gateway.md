---
title: "Deleting a VPC NAT Gateway"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Deleting-a-VPC-NAT-Gateway"
---

You can follow this procedure to delete a VPC NAT Gateway when it is no longer needed.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The VPC NAT Gateway has no SNAT entries. If any exist, first [delete the SNAT entries](https://docs.byteplus.com/en/docs/natgateway/Managing-SNAT-rules-vpcnat#.5Yig6ZmkU05BVOinhOWImQ==).

* The VPC NAT Gateway has no DNAT entries. If any exist, first [delete the DNAT entries](https://docs.byteplus.com/en/docs/natgateway/Managing-DNAT-rules-vpcnat#.5Yig6ZmkRE5BVOinhOWImQ==).

* The VPC NAT Gateway has no NAT IP addresses other than the default NAT IP address. If any exist, first [delete the NAT IP addresses](https://docs.byteplus.com/en/docs/natgateway/Adding-or-deleting-a-NAT-IP#.5Yig6Zmk5Lit6L2sSVA=).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VPC NAT Gateway console](https://console.byteplus.com/nat/vpcNat).

2. In the top menu bar, select a target region and project.

3. In the VPC NAT Gateway list, click  **··· \> Delete** to the right of the target VPC NAT Gateway.

4. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[DeleteNatGateway](https://docs.byteplus.com/en/docs/natgateway/DeleteNatGateway): Delete a VPC NAT Gateway.
