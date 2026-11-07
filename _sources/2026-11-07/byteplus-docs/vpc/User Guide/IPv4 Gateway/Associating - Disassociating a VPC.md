---
title: "Associating/Disassociating a VPC"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Associating-Disassociating-a-VPC"
---

## Associate and activate VPC

### Prerequisites

* Ensure that the target route table does not contain a route entry with a destination CIDR of 0.0.0.0/0. If it exists, please [delete](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry#.5Yig6Zmk6Lev55Sx5p2h55uu) this route entry first.

* The target VPC is unrelated to an IPv4 gateway. A VPC can only be associated with one IPv4 gateway.

* No NAT gateway has been created in the target VPC. If it exists, please [delete](https://docs.byteplus.com/en/docs/natgateway/Deleting-a-NAT-gateway) this NAT gateway first.

* No resources in the target VPC are bound to a directly attached EIP. If attached, detach this EIP first.

* The target VPC has not been configured with any custom CIDR blocks. If present, delete this custom CIDR block first.

### Action description

* After associating a VPC, a route entry with the destination CIDR block 0.0.0.0/0 and the next hop pointing to the IPv4 gateway is automatically added to the specified subnet route table.

* All subnet route tables in the VPC must add a route entry with the next hop pointing to the IPv4 gateway. Otherwise, resources in the associated subnets cannot communicate with the Internet. For procedure, see [Adding a route entry](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry).

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation tree, select **IPv4 Gateway**.

3. In the top menu bar, select your target Region.

4. Click **Associate and activate VPC** to the right of the target IPv4 Gateway.

5. Select the VPC and subnet route table from dropdown.

6. Click **Activate** to complete the action.

## Disassociate VPC

### Prerequisites

* All subnet route tables in the VPC do not contain route entries with a next hop pointing to the IPv4 gateway. If one exists, see [Deleting a route entry](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry#.5Yig6Zmk6Lev55Sx5p2h55uu).

* The IPv4 Gateway is not associated with any gateway route table. If already associated, please [unlink](https://docs.byteplus.com/en/docs/vpc/Associating-disassociating-an-IPv4-Gateway) the gateway route table.

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation tree, select **IPv4 Gateway**.

3. In the top menu bar, select your target Region.

4. In the IPv4 Gateway list, click **Disable** to the right of the target IPv4 Gateway.

5. Click **Disassociate VPC** to the right of the target IPv4 Gateway.

   * **Public Mode**: After disassociation, resources in the VPC are no longer restricted by the IPv4 gateway. ECS instances can access the Internet by binding an EIP.

   * **Private Mode**: After disassociation, resources in the VPC cannot communicate with the Internet. If Internet communication is required, you must reassociate the IPv4 gateway and configure routes for the specified IPv4 gateway.

6. Click **Disable** to complete the action.

## Related documents

* [AttachIpv4Gateway](https://docs.byteplus.com/en/docs/vpc/AttachIpv4Gateway)

* [EnableIpv4Gateway](https://docs.byteplus.com/en/docs/vpc/EnableIpv4Gateway)

* [DetachIpv4Gateway](https://docs.byteplus.com/en/docs/vpc/DetachIpv4Gateway)
