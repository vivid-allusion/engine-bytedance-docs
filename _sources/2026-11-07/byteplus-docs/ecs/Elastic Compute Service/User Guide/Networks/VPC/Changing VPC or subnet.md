---
title: "Changing VPC or subnet"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Changing-the-VPC-or-subnet-of-an-ECS-instance"
---

This topic introduces how to change the VPC or subnet for an ECS instance.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Networks are isolated between different VPCs. Therefore, after you change the VPC for the instance, the instance can not communicate with the instances in the original VPC. Please proceed with caution. <a href="https://docs.byteplus.com/en/docs/vpc/Application-scenarios">How to connect networks between different VPCs?</a></div>


<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios


* As the business grows, the existing network architecture can no longer meet business needs, which requires new network plans. If multiple businesses share one VPC, management difficulties may occur. Therefore, you can plan new VPCs based on your needs and then migrate corresponding ECS instances to the VPCs.

* If address conflicts occur when you enable communication of ECS instances between different VPCs, you can change the VPC or subnet of the ECS instance.

* If you select an inappropriate VPC or subnet when creating an ECS instance, you can change the VPC or subnet for the instance.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


|Resource |Prerequisites |Description |
|---|---|---|
|ECS instance |Must be in the **Stopped** state |If the instance is not in the Stopped state, [stop the instance](https://docs.byteplus.com/en/docs/ecs/Stopping-instances) first. |
||When you replace instance VPCs or subnets in a batch, all selected instances must be under the same project and in the same availability zone. |\- |
||Not added to CLB backend server group |If the ECS instance was added to a CLB backend server, [remove the instance from the backend server group](https://docs.byteplus.com/en/docs/clb/Modifying-the-server-group) first. |
||Not used by other cloud services |\- |
||Not associated with High\-Availability Virtual IP Address |If an Anycast EIP has been associated, [disassociate](https://docs.byteplus.com/en/docs/vpc/Binding-or-unbinding-cloud-resources) the Anycast EIP. The High\-Availability Virtual IP Address is in Beta. If you need a trial, please contact the account manager. |
||The associated subnet is not attached to a custom route table |If the associated subnet was attached to a custom route table, [detach the subnet to the custom route table](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-a-subnet#.6Kej6Zmk5YWz6IGU5a2Q572R). |
||No secondary network interface is mounted |If a secondary network interface was mounted, [unmount the secondary network interface](https://docs.byteplus.com/en/docs/vpc/Loading-or-unloading-a-secondary-network-interface#.5Y246L296L6F5Yqp572R5Y2h) from the selected instance. |
||The associated primary network interface has not been allocated a secondary private IP address |If a secondary private IP address was allocated, [release the secondary private IP address](https://docs.byteplus.com/en/docs/vpc/Adding-or-releasing-a-private-IP-address). |
||Not associated with an IPv6 address |If an IPv6 address was allocated to the instance, [release the IPv6 address](https://docs.byteplus.com/en/docs/vpc/Adding-or-releasing-a-private-IP-address) first. The feature of allocating IPv6 addresses to ECS instances is currently in Beta. If you need a trial, please contact the account manager. |
||Not associated with Anycast EIP |If an Anycast EIP has been associated, [disassociate](https://docs.byteplus.com/en/docs/eip/Disassociating-Cloud-Resource-from-an-EIP) the Anycast EIP. Anycast EIP is currently in Beta. If you need a trial, please contact the account manager. |
|VPC or subnet |The target VPC and instance are in the same region |If the target VPC and selected instance are not in the same region, [create a VPC in the same region as the instance](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC). |
||The target subnet and current subnet are in the same availability zone |If the current subnet and target subnet are not in the same availability zone, [create a subnet in the same availability zone](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet) as the current subnet. |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id="ngyiKMjv"></span>
### Replace the VPC or subnet of one instance

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The target instance must be in the <strong>Stopped</strong> state.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the target project and region.

4. On the Instances page, select " **···**  \> Network and security group \> Modify VPC" in the "Actions" column on the right of the target instance.

5. Refer to the table below to configure the relevant parameters.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Target VPC |Select a VPC in the same region.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you only need the subnet replaced, select the current VPC of the ECS instance.</div><br> |des\-vpc |
   |Subnet |Select a subnet in the same availability zone as the subnet of the current instance, and then assign an IP address for the selected subnet. You can choose to have the system automatically assign an IP address or manually assign an IP address. |des\-subnet |
   |Target security group |Select a security group. |des\-sg |
   

6. Click "Save" to complete the operation.


<span id="a3sHAYML"></span>
### Replace instance VPCs or subnets in a batch

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When you replace instance VPCs or subnets in a batch, the selected instances must be under the same project and in the same availability zone.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the target project and region.

3. In the left\-side navigation pane, select "Instances & Images \> Instances".

4. Select one or more instances, and then select "··· \> Modify VPC" at the bottom of the list.

5. The system pops up a "In bulk Modify VPC" window. Here, you can view operable instances, inoperable instances, and the reasons.

   > Inoperable instances are instances that do not meet the conditions required for modifying VPCs. You can address the issue based on prompts and try again once the conditions are met.   
   

6. Click the "Continue" button to go to the Modify VPC page and configure relative parameters.

   
   |Parameters |Description |Sample value |
   |---|---|---|
   |Target VPC |Select a VPC in the same region.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you only need the subnet replaced, select the current VPC of the ECS instance.</div><br> |des\-vpc |
   |Subnet |Select a subnet in the same availability zone as the subnet of the current instance, and then assign an IP address for the selected subnet. You can choose to have the system automatically assign an IP address or manually assign an IP address. |des\-subnet |
   |Target security group |Select a security group. |des\-sg |
   

7. Click "Reboot" to complete the operation.


<span id=".5pON5L2c57uT5p6c"></span>
## Operation result


* After you replace instance VPCs or subnets in a batch, the instances are still in the **Stopped** state. You need to manually [start](https://docs.byteplus.com/en/docs/ecs/Starting-instances) the ECS instances.

* To view the changed VPC or subnet, go to the Overview page by clicking the instance name on the Instances page.


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[ModifyInstanceVpcAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceVpcAttribute)
