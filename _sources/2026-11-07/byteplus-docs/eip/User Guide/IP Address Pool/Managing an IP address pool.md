---
title: "Managing an IP address pool"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Manage_IP_address_pools"
---

<span id=".5re75Yqg572R5q61"></span>
## Add a CIDR block

<span id=".5pON5L2c6K-05piO"></span>
### Instructions

You can add a new CIDR block to the IP address pool for scaling up.


* Adding **allocated** or **unavailable** IP CIDR block is not supported.

* IP address pools suspended due to overdue payments do not support adding CIDR blocks.

* Billing will start based on the number of IPs in the newly added CIDR block. For more billing rules, see [Billing notes](https://docs.byteplus.com/en/docs/eip/IP_address_pool_overview#.6K6h6LS56K-05piO).


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in [to the EIP console](https://console.byteplus.com/eip/eips).

2. In the top menu bar, select the target region and project.

3. In the left navigation pane, select **Access to Internet \> IP Address Pool**.

4. Click **Add CIDR block** on the right side of the target IP address pool.

5. Select the CIDR block allocation method:

   * Mask: select the IP address mask; the system assigns the IP address CIDR block automatically. The range is 24 to 28.

   * CIDR block: enter the IP address CIDR block. Currently, only adding IPv4 CIDR blocks is supported. The mask range is 23 to 30, and the IP address cannot start with 0.

   > When selecting the **CIDR block** method, we recommend that you first communicate with your account manager regarding the needed IP address CIDR block. Otherwise, allocation may fail.   
   

6. Click **OK** to complete the action.


<span id=".5Yig6Zmk572R5q61"></span>
## Delete a CIDR block

<span id=".5pON5L2c6K-05piO"></span>
### Instructions

Only supports deleting IP CIDR blocks without assigned EIPs. To delete a CIDR block with allocated EIPs, [release the EIP](https://docs.byteplus.com/en/docs/eip/Releasing-an-EIP) first.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in [to the EIP console](https://console.byteplus.com/eip/eips).

2. In the top menu bar, select the target region and project.

3. In the left navigation pane, select **Access to Internet \> IP Address Pool**.

4. Click the name of the target IP address pool, then click the **CIDR block list** tab.

5. Click **Delete** to the right of the target CIDR block.

6. In the pop\-up dialog box, click **Delete** to complete the action.


<span id=".5Yig6ZmkSVDlnLDlnYDmsaA="></span>
## Delete an IP address pool

<span id=".5pON5L2c6K-05piO"></span>
### Action notes

Only supports deleting IP address pools without allocated EIPs. To delete an IP address pool with allocated EIPs, first [release the EIP](https://docs.byteplus.com/en/docs/eip/Releasing-an-EIP).

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [EIP console](https://console.byteplus.com/eip/eips). 

2. In the top menu bar, select the target region and project.

3. Select **Access to Internet \> IP Address Pool** in the left navigation tree.

4. Click **Delete** to the right of the target IP Address Pool.

5. In the pop\-up dialog box, click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [ModifyIpAddressPoolAttributes](https://docs.byteplus.com/en/docs/eip/ModifyIpAddressPoolAttributes): Modify the name and description of an IP Address Pool.

* [AddIpAddressPoolCidrBlock](https://docs.byteplus.com/en/docs/eip/AddIpAddressPoolCidrBlock): Add a CIDR block to a specified IP Address Pool.

* [DeleteIpAddressPoolCidrBlock](https://docs.byteplus.com/en/docs/eip/DeleteIpAddressPoolCidrBlock): Delete a specified CIDR block from an IP Address Pool.

* [DeleteIpAddressPool](https://docs.byteplus.com/en/docs/eip/DeleteIpAddressPool): Delete an IP Address Pool.
