---
title: "Mounting/Unmounting secondary network interfaces"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Attaching-and-detaching-secondary-network-interfaces"
---

This topic describes how to mount or unmount a secondary network interface in the ECS console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also <a href="https://docs.byteplus.com/en/docs/vpc/Loading-or-unloading-a-secondary-network-interface#.5oyC6L296L6F5Yqp572R5Y2h">mount</a> or <a href="https://docs.byteplus.com/en/docs/vpc/Loading-or-unloading-a-secondary-network-interface#.5Y246L296L6F5Yqp572R5Y2h">unmount</a> a secondary network interface in the VPC console.</div>


<span id=".5oyC6L296L6F5Yqp572R5Y2h"></span>
## Mount a secondary network interface

You can mount a secondary network interface to an ECS instance to support flexible configuration of high\-availability network solutions.

<span id=".5rOo5oSP5LqL6aG5"></span>
### Usage notes


* The target instance and the secondary network interface to be mounted must reside in the same VPC and availability zone.​

* The instance must be in the **Running** or **Stopped** status.

* The number of network interfaces that can be mounted to an ECS instance, as well as the number of private IPv4/IPv6 addresses that can be assigned to each network interface, is limited by the instance type. For more information, refer to the "elastic network interface" and "private IP address quota per network interface" metrics in the [Instance types](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types) topic.

* After the network interface is mounted, you can [specify that the network interface is deleted when the ECS instance is released](https://docs.byteplus.com/en/docs/vpc/Enabling-or-disabling-deletion-with-the-ECS-instance) based on your business requirements.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top menu bar, select the region and project where the target instance resides.

3. In the left\-side navigation pane, click "Instances & Images \> Instances" to go to the Instances page.

4. Click the name of the target instance to go to the instance details page.

5. Click the "Network Interface" tab to go to the network interface list page.

6. Click the "Attach Network Interface" button, and then select one or more secondary network interfaces that you want to mount.

7. Click the "Attach" button to mount secondary network interfaces to the instance.


<span id=".5ZCO57ut5pON5L2c"></span>
### Subsequent operation

After secondary network interfaces are mounted to the instance, some images cannot automatically recognize the private IP addresses of the secondary network interfaces and add the corresponding routes. Check whether you need to configure the secondary network interfaces. If you need to configure the secondary network interfaces, complete the configuration before you use the secondary network interfaces. For more information, see [Configuring secondary network interfaces for ECS instances](https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances).

<span id=".5Y246L296L6F5Yqp572R5Y2h"></span>
## Unmount secondary network interfaces

If you no longer need a secondary network interface, you can unmount it after you confirm that unmounting it does not affect your running services or workloads.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites

The target instance is in the **Running** or **Stopped** status.

<span id=".5pON5L2c6K-05piO"></span>
### Usage notes


* You cannot unmount a primary network interface. The lifecycle of a primary network interface is the same as the lifecycle of the instance.

* If you [do not specify that a secondary network interface is deleted when the ECS instance is released](https://docs.byteplus.com/en/docs/vpc/Enabling-or-disabling-deletion-with-the-ECS-instance), when the ECS instance is released, the secondary network interface is automatically unmounted from the ECS instance.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Images".

3. In the top menu bar, select the region and project of the target instance.

4. Click the name of the target instance to go to the instance details page.

5. Click the "Network Interface" tab to go to the network interface list page.

6. Click the "Detach" button in the "Actions" column on the right side of the target network interface.

7. After you confirm the information, click the "Detach" button.


A network interface that is unmounted from an ECS instance is removed from the network interface list of the instance.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [AttachNetworkInterface](https://docs.byteplus.com/en/docs/vpc/AttachNetworkInterface): Mounts secondary network interfaces to ECS instances

* [DetachNetworkInterface](https://docs.byteplus.com/en/docs/vpc/DetachNetworkInterface): Unmounts secondary network interfaces from ECS instances
