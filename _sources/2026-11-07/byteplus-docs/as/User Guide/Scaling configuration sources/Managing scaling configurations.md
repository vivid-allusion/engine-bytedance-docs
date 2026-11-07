---
title: "Managing scaling configurations"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Managing_a_scaling_configuration"
---

Scaling configurations define the compute, storage, network, and security capabilities of cloud resources such as ECS instances. These configurations are used to create cloud resource instances during elastic scaling. This topic describes how to create a scaling configuration.

## Create a scaling configuration

1. Log in to the[ Auto Scaling console](https://console.byteplus.com/as/group).

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select "Scaling Configuration Sources \> Scaling configurations".

4. Click the "Create Scaling Configuration" button. The parameters required to create a scaling configuration are generally the same as those required to purchase an ECS instance. The following table lists the parameters that are different. For more information, see [Purchasing ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   |Differential parameter |Description |
   |---|---|
   |**Billing method** ||
   |Billing method |Currently, only "Pay\-as\-you\-go" and "Spot" instances can be created by using a scaling group. |
   |Region |The region selected for the scaling group is inherited. You cannot modify this parameter. |
   |**Instance configuration** ||
   |Availability zone |The availability zone corresponding to the subnet of the scaling group is inherited. This parameter is not displayed. |
   |Instance type |The preferred instance type for scale\-out, that is, the instance type with the highest priority.<br><br>> **tip**<br><br><br><br>* > The instance types supported in the corresponding availability zone are subject to the actual display in the console.<br><br><br>* > We recommend that you select an instance type with "Normal stock" to improve the success rate of scaling out.<br> |
   |System volume |The system volume type and capacity used by instances during scaling up. Supported:<br><br><br>* [TSSD TL0](https://docs.byteplus.com/en/docs/ecs/Volume-specification-tssd-tl0-Volume)<br><br>* [ESSD FlexPL](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume)<br><br>* [ESSD PL0](https://docs.byteplus.com/en/docs/ecs/esd_pl0_volume)<br><br><br>> **tip**<br><br><br>> A system volume is used to store the operating system and is created with the ECS instance. The system volume and the ECS instance have the same lifecycle.<br> |
   |Data Volume |The system volume type and capacity used by instances during scaling up. Supported:<br><br><br>* [T](https://docs.byteplus.com/en/docs/ecs/Volume-specification-tssd-tl0-Volume)[SSD TL0](https://docs.byteplus.com/en/docs/ecs/Volume-specification-tssd-tl0-Volume)<br><br>* [ESSD FlexPL](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume)<br><br>* [ESSD PL0](https://docs.byteplus.com/en/docs/ecs/esd_pl0_volume)<br><br><br>> **tip**<br><br><br>> Data volumes can be used to store application data. The number of data volumes supported by one ECS instance is determined by the instance type. For more information, refer to [Instance type and specification](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).<br> |
   |Multi\-type |After you select the preferred instance type and the matched image and volumes, you can still select multiple instance types and drag to sort them. The preferred instance type has the highest priority and cannot be adjusted. To modify the preferred instance type, clear "Enable multi\-type selection" before you proceed.<br><br>> **tip**<br><br><br><br>* > When the scaling group scales out, upon meeting the scaling policy requirements, if the higher\-priority instance type in the specified availability zone is out of stock or fails to be provisioned as expected, a lower\-priority instance type will automatically be used to create instances. For more information, see [Automatically scaling out instances](https://docs.byteplus.com/en/docs/as/Adding-instances-automatically).<br><br><br>* > When the scaling group scales in, upon meeting both the scaling policy and instance removal policy requirements, lower\-priority instances in the specified availability zone are removed first. For more information, see [Automatically removing instances](https://docs.byteplus.com/en/docs/as/Removing-instances-automatically).<br> |
   |Virtual Private Cloud |The VPC to which the scaling group belongs is inherited. You cannot modify this parameter. |
   |Subnet |The subnet of the scaling group is inherited. This parameter is not displayed. |
   |Secondary network interface |Secondary network interfaces cannot be simultaneously created when the scaling group creates instances. After the instances are created, you can mount secondary network interfaces to the instances in the ECS console. For more information, see [Mounting network interfaces to instances](https://docs.byteplus.com/en/docs/ecs/Attaching-and-detaching-secondary-network-interfaces). |
   |Quantity |The number of instances in the scaling group is controlled by the scaling group and scaling rules. Therefore, this parameter is not involved in the scaling configuration. |
   |Instance name/Hostname |You can configure ordered and unique names or hostnames for scale\-out instances. The configuration rules differ slightly from those for ECS instances. Refer to [Setting sequential and unique names or hostnames for instances](https://docs.byteplus.com/en/docs/as/Setting-sequential-and-unique-names-or-hostnames-for-instances). |
   |Scaling configuration name |The name of the scaling configuration. |
   |Status After Creation |Specify whether to immediately associate the scaling configuration with the scaling group upon creation.<br><br><br>* **Take note that** a scaling group can only be associated with one scaling configuration at a time. If you select "Associate scaling group" when the scaling group is already associated with an existing scaling configuration, the new scaling configuration will be used to create instances in subsequent scale\-out operations upon the completion of this creation. Existing instances in the scaling group are not affected.<br><br>* If you do not select "Associate scaling group", you can associate the scaling configuration with the scaling group later by referring to [Associating scaling group](https://docs.byteplus.com/en/docs/as/Associating-a-scaling-configuration-source-with-a-scaling-group). |

6. Confirm the configuration information and click the "Create Now" button to complete the operation.

## Modify a scaling configuration

You can modify a scaling configuration at any time. After modification, the new configuration will be applied when instances are created using this scaling configuration in subsequent operations. Existing instances in the scaling group will not be affected.

1. Log in to the[ Auto Scaling console](https://console.byteplus.com/as/group).

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select "Scaling Configuration Sources \> Scaling configurations".

4. Click the "Change scaling configuration" button on the right side of the scaling configuration you want to modify.

5. Modify the configuration by referring to [Create a scaling configuration](https://docs.byteplus.com/en/docs/as/Managing_a_scaling_configuration). The instance type must be supported in the availability zone selected for the scaling group. Otherwise, the scaling configuration cannot be modified as expected.

6. Click the "Modify now" button to complete the operation.

## Delete a scaling configuration

You cannot delete a scaling configuration associated with a scaling group. To delete it, you need to associate another scaling configuration with the scaling group.

1. Log in to the[ Auto Scaling console](https://console.byteplus.com/as/group).

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select "Scaling Configuration Sources \> Scaling configurations".

4. Click "... \> Delete" on the right side of the scaling configuration that you want to delete.

5. Click the "Confirm" button to complete the operation.

## Subsequent operations

You need to [create scaling rules](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-policys) for a scaling group to define the conditions and methods that trigger the scaling of instances within the group, including trigger time, adjustments, cooldown time, and other relevant parameters.

## Related documents

* [CreateScalingConfiguration](https://docs.byteplus.com/en/docs/as/CreateScalingConfiguration)

* [ModifyScalingConfiguration](https://docs.byteplus.com/en/docs/as/ModifyScalingConfiguration)

* [DeleteScalingConfiguration](https://docs.byteplus.com/en/docs/as/DeleteScalingConfiguration)
