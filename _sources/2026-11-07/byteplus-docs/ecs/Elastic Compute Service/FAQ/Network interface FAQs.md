---
title: "Network interface FAQs"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Network-interface-FAQs"
---

<span id="how-can-i-view-the-eip-address-of-an-instance"></span>
## How can I view the EIP address of an instance?

You can view the EIP address bound to the instance on the instance or details page. For specific operations, please refer to [View instance information](https://docs.byteplus.com/en/docs/ecs/Instance-overview-1).

<span id="how-can-i-distinguish-between-the-primary-network-interface-and-the-secondary-network-interface"></span>
## How can I distinguish between the primary network interface and the secondary network interface?

Primary network interface: The network that is created by default when the Elastic Compute Service (ECS) instance is created. The primary network interface cannot be detached from the ECS instance.

Secondary network interface: The network interface that can be created, attached, and detached as needed.

<span id="can-i-detach-the-primary-network-interface"></span>
## Can I detach the primary network interface?

The lifecycle of the primary network interface is the same as that of the ECS instance. You are not allowed to detach it.

<span id="can-i-change-the-elastic-ip-address-eip-and-private-ip-address-of-each-network-interface"></span>
## Can I change the Elastic IP Address (EIP) and private IP address of each network interface?

Associate and dissociate an EIP to change the EIP of a network interface.

Release and add private IP addresses to change the secondary private IP addresses of the network interface (including the secondary private IPv4 address and private IPv6 address).

You are not allowed to change the primary private IPv4 address of the secondary network interface. However, you are allowed to replace the Virtual Private Cloud (VPC) to change the primary private IPv4 address of the primary network interface.

<span id="is-there-a-limit-to-the-number-of-network-interfaces-that-can-be-attached-to-an-ecs-instance"></span>
## Is there a limit to the number of network interfaces that can be attached to an ECS instance?

Yes. The limit depends on the ECS instance type. For more information, refer to [Instance types](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).

<span id="do-the-ecs-instance-and-secondary-network-interface-to-be-attached-have-to-belong-to-the-same-vpc"></span>
## Do the ECS instance and secondary network interface to be attached have to belong to the same VPC?

Yes. However, the secondary network interface of another subnet can be attached to the ECS instance for traffic segmentation.

<span id="what-can-i-do-after-i-fail-to-detach-a-network-interface"></span>
## What can I do after I fail to detach a network interface?

Log on to the [ECS Console](https://console.byteplus.com/ecs/instance) and click **Support** in the top menu bar for support.

<span id="why-does-the-secondary-network-interface-i-attach-not-work"></span>
## Why does the secondary network interface I attach not work?

After you attach a secondary network interface to an ECS instance, some images do not automatically identify the private IP address of the secondary network interface or add the corresponding route. Refer to [Configuring a network interface and a private address](https://docs.byteplus.com/en/docs/vpc/Configuring-a-network-interface-and-a-private-address) to confirm whether you want to configure the secondary network interface. You must confirm the network interface before you can use it.
