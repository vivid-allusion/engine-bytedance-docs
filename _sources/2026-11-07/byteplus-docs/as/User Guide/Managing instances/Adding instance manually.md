---
title: "Adding instance manually"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Adding-instances-manually"
---

## Scenarios

You can add existing instances to a scaling group, where they will share access traffic with other instances in the group and jointly provide external services.

## Prerequisites

Only the primary network interface of an instance can be added to a scaling group. Before you add an instance to a scaling group, you need to confirm the items described in the following table.

|Item |Prerequisites |
|---|---|
|Instance |* The instance must be in the same VPC as the scaling group.<br><br>* The instance must be in **Running** status in the ECS console.<br><br>* The instance must not already exist in other scaling groups.<br><br>* For a scaling group with the specified instance type and weight, only instances with the specified instance type can be added. After the instances are added to the scaling group, they automatically inherit the specified weight. |
|Scaling group |The scaling group must be in the **Running** or **Cooling** status. |

## Instructions

* You can add up to 20 instances to a scaling group at one time.

* Instances added manually are not subject to scaling configuration and cooldown time restrictions. You can manually add instances with any configuration at any time.

* The sum of the instance count or capacity that you want to add and the existing instance count or capacity in the scaling group must not exceed the maximum instance count or capacity of the scaling group.

* If [ or capacity](https://docs.byteplus.com/en/docs/as/Desire-instance-number-capacity)[ or capacity](https://docs.byteplus.com/en/docs/as/Desire-instance-number-capacity) is enabled for a scaling group, after you add instances to the scaling group, the expected instance count or capacity will be automatically modified to the actual instance count or capacity of the scaling group.

## Procedure

1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group).

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Instance Management" tab.

4. Click the "Add existing instance" button and select the instances that you want to add. The page only displays instances in the same availability zone and VPC as the scaling group.

   > **tip**

   > Make sure the target instance has not been added to a scaling group and that the scaling group has not reached the maximum number of instances.

5. Determine whether to select "Enable the scaling group to manage the instance lifecycle" based on your needs. If you select "Enable the scaling group to manage the instance lifecycle", the instances will be automatically deleted when the scaling group scales in, and associated resources such as EIPs, volumes, and network interfaces will also be deleted at the same time. For more information about lifecycle management, see [Instance lifecycle](https://docs.byteplus.com/en/docs/as/Instance-lifecycle).

   > **tip**

   * > The lifecycle of Subscription instances cannot be managed by the scaling group. Even if you select "Enable the scaling group to manage the instance lifecycle" for Subscription instances, the setting will not take effect.

   * > Once entrusted, the action cannot be revoked.

6. Click the "Confirm" button to complete the operation.

## Resource mounting policy after instances are added

Instances are automatically added to the load balancer and RDS database instances associated with the scaling group. EIPs are automatically purchased and assigned based on the network configuration of the scaling configuration. You can log in to the Load Balancer, EIP, and other consoles to view the new resources.

## Related documents

[AttachInstances](https://docs.byteplus.com/en/docs/as/AttachInstances)
