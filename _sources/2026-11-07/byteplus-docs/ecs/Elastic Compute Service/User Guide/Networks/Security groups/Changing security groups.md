---
title: "Changing security groups"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Changing-security-groups"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

This topic introduces how to add, change, or remove security groups for the network interface of ECS instances in the ECS console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A  network interface can be associated with at least one security group and at most five security groups.

* A network interface can only associate with the security group within the same VPC.


<span id=".5pON5L2c5q2l6aqk"></span>
## Manage security groups in a batch

If you need unified security group management for multiple ECS instances, you can add, change, or remove security groups for instances in a batch.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This feature is supported by the orchestration service, which by default uses the CustomerRoleForOOS role to submit operations. If you are a first time user, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Preparation">Orchestration permission management</a> to create this role.</div>


* <div data-tips="true" data-tips-type="default">To manage security groups in bulk, make sure that the selected instances reside in the same VPC.</div>




<Tabs>
<Tab zoneid="lut93FOf92" title="Add to security group">
<TabTitle>Add to security group</TabTitle>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When you add network interfaces to a security group in a batch, the security groups originally associated with selected network interfaces are not affected.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the region and project where the target instance resides.

4. On the Instances page, select one or more instances, and then select the "··· \> Add to security group" at the bottom of the list.

5. In the "In bulk Add to security group" window that the system pops up, click "Continue".

6. For detailed steps, you can refer to the table below.

   
   |Configuration item |Description |
   |---|---|
   |Select the network interface of the instance |For selected instances, you can select the network interface that you need to associate with the security group. The options include:<br><br><br>* Select all network interfaces (default): The system defaults to this option. This means you add all network interfaces associated with the ECS instance to the selected security groups.<br><br>* Select all primary network interfaces: After choosing this option, you add the primary network interface associated with the ECS instance to the selected security groups.<br><br>* Select custom network interface: In the "Network Interface" column, you can select the network interfaces that you need to add to the security group. |
   |Select the security group |When creating an instance, you must associate at least one security group with the instance. Therefore, you can add up to 4 security groups here. The page by default displays all security groups under the current VPC. If no security group is available, please [create a security group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group) first. |
   

7. Click "Save" to complete the operation.

8. After completing the operation, you can click the "Go to instance maintenance attribute" to [view task details](https://docs.byteplus.com/en/docs/ecs/Manage_orchestration_tasks#.5p-l55yL5Lu75Yqh6K-m5oOF) on the CloudOps Orchestration page.


</Tab>
<Tab zoneid="MHAjDZLv3Y" title="Replace security group">
<TabTitle>Replace security group</TabTitle>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After you replace the security group for network interfaces, the original security group is no longer retained and replaced directly by the newly selected security group.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the region and project where the target instance resides.

4. On the Instances page, select one or more instances, then select "··· \> Replace security group" at the bottom of the list.

5. In the "In bulk Replace security group" window that the system pops up, click "Continue".

6. For detailed steps, you can refer to the table below.

   
   |Configuration item |Description |
   |---|---|
   |Select the network interface of the instance |For selected instances, you can select the network interface you need to replace the security group for. The selecting options of the network interface include:<br><br><br>* Select all network interfaces (default): The system defaults to this option. This means you replace security groups for all network interfaces associated with the ECS instance.<br><br>* Select all primary network interfaces: After choosing this option, you replace the security group for the primary network interface associated with the ECS instance with the selected security groups.<br><br>* Select custom network interfaces: In the "Network Interface" column, select the network interfaces you want to manage. |
   |Select the security group |This page by default displays all security groups under the current VPC. If no security group is available, please [create a security group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group) first. |
   

7. Click "Save" to complete the operation.

8. After completing the operation, you can click the "Go to instance maintenance attribute" to [view task details](https://docs.byteplus.com/en/docs/ecs/Manage_orchestration_tasks#.5p-l55yL5Lu75Yqh6K-m5oOF) on the CloudOps Orchestration page.


</Tab>
<Tab zoneid="KkGU3I2sSU" title="Remove from security group">
<TabTitle>Remove from security group</TabTitle>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Remove from the selected security group only. This does not affect other security groups associated with the network interface.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the region and project where the target instance resides.

4. On the Instances page, select one or more instances, then select "··· \> Remove from security group" at the bottom of the list.

5. In the "In bulk Remove from security group" window that the system pops up, click "Continue".

6. For detailed steps, you can refer to the table below.

   
   |Configuration item |Description |
   |---|---|
   |Select the network interface of the instance |For selected instances, you can select the network interface that you need to disassociate with the security group.<br><br><br>* Select all network interfaces (default): The system defaults to this option. This means you remove all network interfaces associated with the ECS instance from the selected security groups.<br><br>* Select all primary network interfaces: After choosing this option, you remove the primary network interface associated with the ECS instance from the selected security groups.<br><br>* Select custom network interface: In the "Network Interface" column, you can select the network interfaces that you need to remove from the security group. |
   |Select the security group |Select the security group you need to remove network interfaces from. Unselectable options mean no network interface is associated with the security group. |
   

7. Click "Save" to complete the operation.

8. After completing the operation, you can click the "Go to instance maintenance attribute" to [view task details](https://docs.byteplus.com/en/docs/ecs/Manage_orchestration_tasks#.5p-l55yL5Lu75Yqh6K-m5oOF) on the CloudOps Orchestration page.


</Tab>
</Tabs>


<span id="W48IyXAZ"></span>
##  of changing the security group for an ECS instance


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top menu bar, select a target region.

3. In the left\-side navigation pane, click "Instances".

4. On the right side of the target instance, select "··· \> Network and security group\> Change Security Group".

5. From the drop\-down menu, click the network interface to be added, and then select the target security group.

6. Click "Save" to complete the operation.


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[ModifyNetworkInterfaceAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaceAttributes): Modifies network interface information such as the name, description, security group, source/destination check, and "Removal with ECS Instances" setting.
