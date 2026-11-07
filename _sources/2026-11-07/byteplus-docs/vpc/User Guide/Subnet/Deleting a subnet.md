---
title: "Deleting a subnet"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Deleting-a-subnet"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

You may use this procedure to delete unused subnets.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


|Prerequisites |Explanation |
|---|---|
|No network interface in the subnet |First [delete the network interface](https://docs.byteplus.com/en/docs/vpc/Deleting-a-subnet) if any |
|No high availability virtual IP in the subnet |First [delete the High-Availability Virtual IP Address](https://docs.byteplus.com/en/docs/vpc/Deleting-a-HAVIP) if any. |
|Subnet is not associated with a Network ACL |First [disassociate](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-with-subnet-with-a-network-ACL) if already bound. |
|The subnet is not referenced by any SNAT rules |First [delete the SNAT entry](https://docs.byteplus.com/en/docs/natgateway/Managing-SNAT-rules) if already referenced. |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Subnet**.

3. In the top menu bar, select the target project and region.

4. In the subnet list, find the target subnet, then click **Delete** on the right side.

   * If you receive a "Temporarily unable to delete subnet" notification: This indicates unmet prerequisites for deletion. Follow the provided instructions to remove associated resources before retrying Subnet deletion.

   * Can be deleted: Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[DeleteSubnet](https://docs.byteplus.com/en/docs/vpc/DeleteSubnet)
