---
title: "Creating or Deleting a network interface"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Creating-or-Deleting-a-network-interface"
---

This article introduces to you how to create or delete Network Interface.

<span id="creating-a-network-interface"></span>
## Creating a Network Interface

<span id="instruction"></span>
### Instruction


* The primary network interface is created by default with the instance of the Elastic Compute Service (ECS) and cannot be created separately.

* The BytePlus Network Interface is created by default with the service it belongs to and cannot be created separately.


<span id="procedure"></span>
### Procedure


1. Log on to the [Network Interface console](https://console.byteplus.com/vpc/port).

2. In the top menu bar, select the target Region and target project.

3. Click **Create Network Interface** .

4. Configure the following parameters.

   
   |**Parameter** |**Description** |**Example Value** |
   |---|---|---|
   |Name |Set the name of the secondary network interface. |eni\-01 |
   |VPC |Select the virtual private cloud (VPC) where the secondary Network Interface is located. After the VPC is selected, the Network Interface can only be associated with or attached with cloud resources in the same VPC as it, such as security groups and ECS instances.<br><br>You can click **Create VPC** to create a VPC, and after the VPC is created, go to this page to select the new VPC. |vpc\-01 |
   |Subnet |Select the subnet where the secondary Network Interface is located. The subnet assigns private IPv4 addresses to the secondary Network Interface. Make ensure that the subnet includes sufficient available IPv4 addresses. |subnet\-01 |
   |Primary Private IPv4 Address |Set the primary private IPv4 address of the secondary Network Interface. This address can be automatically or manually assigned.<br><br><br>* Auto\-assign: The system automatically assigns an unoccupied IPv4 address from the selected subnet.<br><br>* Custom\-assign : You can manually enter an unoccupied IPv4 address from the selected subnet. |192.XX.XX.5 |
   |Secondary Private IPv4 Address |Set a secondary private IPv4 address for the secondary Network Interface as required. Up to nine secondary private IPv4 addresses can be assigned.<br><br><br>* Do not assign: Skip assigning secondary private IPv4 addresses now.<br><br>* Auto\-assign: Specify the number of secondary private IPv4 addresses to be automatically assigned. Then, the system automatically assigns the specified number of unoccupied IPv4 addresses from the selected subnet.<br><br>* Custom\-assign: You can manually enter an unoccupied IPv4 address from the selected subnet. |192.XX.XX.6 |
   |Private IPv6 Address |If IPv6 is enabled for the subnet, you can set up to 10 private IPv6 addresses for the secondary Network Interface.<br><br><br>* Do not assign: Skip assigning private IPv6 addresses now.<br><br>* Auto\-assign: Specify the number of secondary private IPv6 addresses to be automatically assigned. Then, the system automatically assigns the specified number of unoccupied IPv6 addresses from the selected subnet.<br><br>   \*Custom\-assign: You can manually enter an unoccupied IPv6 address from the selected subnet. |Do not assign |
   |Security Group |Select the security group associated with the secondary Network Interface to protect the secondary Network Interface. Up to five security groups can be associated with a single Network Interface.<br><br>To modify a security group rule after the secondary Network Interface is created, refer to [Changing a security group rule of a secondary Network Interface](https://docs.byteplus.com/en/docs/vpc/Updating-the-security-group-of-a-network-interface). |Default |
   |Project |Select the project to which the Network Interface belongs. For more information, refer to [Managing projects](https://docs.byteplus.com/en/docs/vpc/Managing-projects).<br><br><br>* If you select **All Resources** from the top menu bar before opening the creation page, you can select an existing project from the drop\-down list.<br><br>* If you select the target project from the top menu bar before opening the creation page, you can select only the target project. |default |
   |Tags |Add one or more user tags to the secondary Network Interface. A tag consists of a key\-value pair. You can use tags to classify and search for resources.<br><br>Click the add icon, then select or enter a tag key and a tag value, to add a tag to the Network Interface. |* key:eni\-key<br><br>* value:eni\-v1 |
   

5. Click **OK**.


After the secondary Network Interface is created, you must [attach it to an ECS instance](https://docs.byteplus.com/en/docs/ecs/Attaching-and-detaching-secondary-network-interfaces#attaching-secondary-network-interfaces) and check whether further configuration of the secondary Network Interface is required. For more information, refer to [Configuring a secondary Network Interface](https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances). If required, further configure the secondary Network Interface before use.

<span id="delete-network-interface"></span>
## Delete Network Interface

You can refer to the following operations to delete the Network Interface that is no longer in use.


<Tabs>
<Tab zoneid="X0AG2fchqR" title="Delete Secondary Network Interface">
<TabTitle>Delete Secondary Network Interface</TabTitle>

<span id="limits"></span>
#### limits


* The secondary Network Interface that has been attached to the ECS instance cannot be deleted.

* Only the Network Interface in the **Detaching** state supports the delete action, and the network interface in other statuses cannot be deleted.

* The secondary Network Interface that has enabled the function of deleting with the ECS instance will be deleted along with the ECS instance when it is deleted.


<span id="procedure"></span>
#### Procedure


1. Log on to the [Network Interface console](https://console.byteplus.com/vpc/port).

2. In the top navigation bar, select the project and Region.

3. Click  **···\> Delete** on the right side of the target secondary Network Interface.

4. Click **Delete**.


</Tab>
<Tab zoneid="CQXCfRe2Bx" title="Delete BytePlus Network Interface">
<TabTitle>Delete BytePlus Network Interface</TabTitle>

Delete the service to which the BytePlus Network Interface belongs, and the Network Interface can be deleted.


</Tab>
<Tab zoneid="PHurkXZXUD" title="Delete Primary Network Interface">
<TabTitle>Delete Primary Network Interface</TabTitle>

After deleting the ECS instance, the primary Network Interface will be deleted along with it.


</Tab>
</Tabs>


<span id="related-documents"></span>
## Related documents


* [CreateNetworkInterface](https://docs.byteplus.com/en/docs/vpc/CreateNetworkInterface) : Creates a secondary network interface.

* [DeleteNetworkInterface](https://docs.byteplus.com/en/docs/vpc/DeleteNetworkInterface) : Deletes a specified secondary network interface.
