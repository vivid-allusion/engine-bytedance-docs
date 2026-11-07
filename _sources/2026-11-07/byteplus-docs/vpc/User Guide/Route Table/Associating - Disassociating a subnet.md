---
title: "Associating/Disassociating a subnet"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-a-subnet"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

All subnets are associated with the system route table by default. For fine\-grained route management, you can flexibly associate different subnets with corresponding custom subnet route tables based on your business requirements.

<span id="04KlsEFe"></span>
## Instructions


* The system route table does not support manually associating or disassociating subnets.

* A route table can be associated with one or more subnets within its Virtual Private Cloud (VPC), and a subnet can only be associated with one route table.

* The system route table serves as the fallback mechanism: When a subnet is associated with a custom route table, it is automatically disassociated from the system route table. When the subnet is disassociated from the custom route table, it is automatically re\-associated with the system route table.


<span id=".5YWz6IGU5a2Q572R"></span>
## <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7007c9181d12a8171bc8b0a2b5c34b79.png) </span>

<span id=".5YWz6IGU5a2Q572R"></span>
## Associate subnet

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Once a custom route table is associated with a subnet, its routing entries take effect immediately for that subnet. All cloud resources within the subnet will then use this routing policy.</div>



1. Log in to the  [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Route Table**.

3. In the top menu bar, select the target project and region.

4. Click **Associate Subnet** on the right side of the target custom subnet route table.

5. Select the associated subnet and click **Associate** to complete the association.


<span id=".6Kej6Zmk5YWz6IGU5a2Q572R"></span>
## Dissociate Subnet


1. Log in to the  [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Route Table**.

3. In the top menu bar, select the target project and target Region.

4. Click the name of the target route table.

5. On the **Associated Subnets** tab, click **Disassociate** on the right side of the target subnet.

6. Click **Disassociate** to complete the actions.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [AssociateRouteTable](https://docs.byteplus.com/en/docs/vpc/AssociateRouteTable)

* [DisassociateRouteTable](https://docs.byteplus.com/en/docs/vpc/DisassociateRouteTable)


&nbsp;
