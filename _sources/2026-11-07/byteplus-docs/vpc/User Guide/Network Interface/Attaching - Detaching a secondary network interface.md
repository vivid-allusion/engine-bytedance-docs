---
title: "Attaching/Detaching a secondary network interface"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Loading-or-unloading-a-secondary-network-interface"
---

## Scenarios

This topic introduces how to mount/unmount a secondary network interface for an Elastic Compute Service (ECS) instance.

> In addition to performing this operation in the Network Interface Console, you can also manage this in the ECS Console. For details, see [Attaching a Secondary Network Interface](https://docs.byteplus.com/en/docs/ecs/Attaching-and-detaching-secondary-network-interfaces#.5oyC6L296L6F5Yqp572R5Y2h) and [Detaching a Secondary Network Interface](https://docs.byteplus.com/en/docs/ecs/Attaching-and-detaching-secondary-network-interfaces#.5Y246L296L6F5Yqp572R5Y2h).

## Attach secondary network interface

You can attach secondary network interfaces to your ECS instances to enable flexible and highly available network architecture.

### Prerequisites

* The ECS instance and the secondary network interface must reside in the same VPC and the same Availability Zone.

* The ECS instance status is **Running** or **Stopped**.

* The number of assigned private IPv4 addresses and private IPv6 addresses on the secondary network interface must be within the per\-network interface IP quota supported by the instance type.

### Action description

* After a network interface is successfully attached, the number of private IPv4 addresses and private IPv6 addresses is limited by the ECS instance type. For details, see the [instance type introduction](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).

* After a network interface is successfully attached, you can [enable deletion with ECS instance](https://docs.byteplus.com/en/docs/vpc/Enabling-or-disabling-deletion-with-the-ECS-instance) as needed.

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Network Interface**.

3. In the top menu bar, select the target project and region.

4. Click **Attach** on the right side of the target Network Interface.

5. On the **Select Instance** page that pops up on the right, select the ECS instance that requires a secondary network interface to be mounted.

   > **tip**

   > On the **Select Instance** page, you can view the number of private IP addresses bound to the current network interface and the quota of private IP addresses for a single network interface in the specification of the target instance.

6. Click **Migrate** to complete the action.

### What to do next

After attaching a secondary network interface to an ECS instance, some images cannot automatically recognize the secondary network interface’s private IP address or add the corresponding route. You need to configure it manually. For details, refer to [Configuring a secondary network interface in ECS](https://docs.byteplus.com/en/docs/vpc/Configuring-a-network-interface-and-a-private-address).

## Detach secondary network interface

For secondary network interfaces that are no longer in use, you may detach them after fully evaluating the potential impact on your current services.

> **warning**

> The primary network interface cannot be detached. Its lifecycle is bound to the ECS instance.

### Prerequisites

The ECS instance status is **Running** or **Stopped**.

### Action description

[Secondary network interfaces with Deleted with ECS instance disabled](https://docs.byteplus.com/en/docs/vpc/Enabling-or-disabling-deletion-with-the-ECS-instance) are automatically detached when the ECS instance is released.

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Network Interface**.

3. In the top menu bar, select the target project and region.

4. Click **Detach** on the right side of the target Network Interface.

5. Click **Detach** to complete the actions.

### What to do next

If this Network Interface is no longer required, you can [Delete Network Interface](https://docs.byteplus.com/en/docs/vpc/Deleting-a-network-interface).

## Related documents

* [AttachNetworkInterface](https://docs.byteplus.com/en/docs/vpc/AttachNetworkInterface)

* [DetachNetworkInterface](https://docs.byteplus.com/en/docs/vpc/DetachNetworkInterface)
