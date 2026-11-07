---
title: "Adding or deleting a NAT IP"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Adding-or-deleting-a-NAT-IP"
---

After creating a VPC NAT Gateway, the system assigns an inactive private IP address from the subnet as the NAT Gateway's default NAT IP address. This IP cannot be deleted and shares the same lifecycle as the VPC NAT Gateway.

If the default NAT IP address does not meet your needs, you can flexibly add or delete the NAT IP by following procedures.

<span id=".5re75Yqg5Lit6L2sSVA="></span>
## Add a NAT IP

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* The subnet where the VPC NAT gateway is located has available private IP addresses.

* The number of NAT IP addresses added to the VPC NAT Gateway has not reached the quota. Please refer to [Limits](https://docs.byteplus.com/en/docs/natgateway/Limits).

* The current account is not overdue on payment, or the overdue time is within 2 hours. For more operations, refer to [Recharge procedure](https://docs.byteplus.com/en/docs/6269/100434).

* A single VPC NAT Gateway supports up to 50 NAT IP addresses.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [VPC NAT Gateway console](https://console.byteplus.com/nat/vpcNat).

2. In the top menu bar, select a target region and project.

3. In the VPC NAT gateway list, click **Configure NAT IP** to the right of the target VPC NAT gateway.

4. In the NAT IP tab, click **Add NAT IP**.

5. Enter the name of the NAT IP, then select the allocation method:

   * Automatic assignment: Automatically allocate an inactive IP address from the subnet to which the VPC NAT Gateway belongs.

   * Manual assignment: Manually allocate an inactive IP address from the subnet to which the VPC NAT Gateway belongs.

6. Click  **+Add** to sequentially add multiple NAT IPs.

7. Click **Add** to complete the action.


<span id=".5Yig6Zmk5Lit6L2sSVA="></span>
## Delete a NAT IP

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* The NAT IP is not attached to SNAT entries or DNAT entries. If attached, see [Delete a SNAT entry](https://docs.byteplus.com/en/docs/natgateway/Managing-SNAT-rules#.5Yig6ZmkU05BVOinhOWImQ==) or [Delete a DNAT entry](https://docs.byteplus.com/en/docs/natgateway/Managing-DNAT-rules#.5Yig6ZmkRE5BVOinhOWImQ==).

* Default NAT IPs cannot be deleted.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [VPC NAT Gateway console](https://console.byteplus.com/nat/vpcNat).

2. In the top menu bar, select a target region and project.

3. In the VPC NAT gateway list, click **Configure NAT IP** to the right of the target VPC NAT gateway.

4. On the NAT IP tab, click **Delete** to the right of the target NAT IP.

5. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [CreateNatIp](https://docs.byteplus.com/en/docs/natgateway/CreateNatIp): Add a NAT IP address.

* [DeleteNatIp](https://docs.byteplus.com/en/docs/natgateway/DeleteNatIp): Delete a NAT IP address.
