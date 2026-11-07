---
title: "Implementing secure mutual access between different VPCs"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Secure-intercommunication-between-different-VPCs"
---

This topic describes how to forward access requests to a secure network deployed with a BytePlus Cloud Firewall or third\-party firewall via Transit Router (TR). This setup enables secure intercommunication between two Virtual Private Clouds (VPCs).

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

A company deployed private services within three VPCs in BytePlus China (Guangzhou). Among them, Business A and Business B are respectively deployed in vpc01 and vpc02, and the firewall software is deployed in vpc03. For business security considerations, the traffic between Business A and Business B must pass through the firewall software for traffic scrubbing. The specific scenario is shown in the following diagram.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If your firewall is Cloud Firewall, see <a href="https://docs.byteplus.com/en/docs/cloud_firewall/What-is-BytePlus-Cloud-Firewall">Cloud Firewall</a> for more information.</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d7d67cf7eee54b1c5e22853a4e65ce45.png) </span>

<span id=".5pWw5o2u6KeE5YiS"></span>
## Data planning

The data planning for secure intercommunication of traffic between different VPCs in the same region is shown below. Specific parameters for each cloud service in the networking scenario are shown in Table 1 and Table 2.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2fdadd7acce3de901b85d2909f0b8aa7.png) </span>

The description of traffic paths in the above figure is as follows (taking access from vpc01 to vpc02 as an example, the principle of vpc02 accessing vpc01 is similar):


1. After Elastic Compute Service (ECS) ecs01 initiates an access request to ecs02. According to the route table of the VPC linked to ecs01's subnet, the system matches the route entry with next hop tr01 and forwards the access request to tr01.

2. The TR forwards the access request to attach\-vpc03 after matching the destination CIDR block based on the TR system route table associated with attach\-vpc01.

3. In vpc03, the system references the VPC route table associated with the subnet that the TR network interface belongs to. It matches the route entry with a next hop of ecs\-fw and forwards the request to the ecs\-fw.

4. After the traffic of the access request is scrubbed through the firewall in the ECS ecs\-fw, based on the VPC route table associated with the subnet to which the ECS belongs, the system matches the route entry with the next hop of tr01 and forwards the request to the tr01.

5. The TR uses the TR custom route table for attach\-vpc03's associated forwarding to match the Destination CIDR Block and finally delivers the request to vpc02, achieving vpc01's secure access to vpc02.


**Table 1 VPC**


|VPC |VPC CIDR block |Subnet information |ECS information |
|---|---|---|---|
|vpc01 |192.168.0.0/16 |* Name: subnet01<br><br>* CIDR block: 192.168.1.0/24 |* Name: ecs01<br><br>* Private IP: 192.168.1.10 |
|vpc02 |172.16.0.0/16 |* Name: subnet02<br><br>* CIDR block: 172.16.1.0/24 |* Name: ecs02<br><br>* Private IP: 172.16.1.10 |
|vpc03 |10.1.0.0/16 |* Name: subnet03<br><br>* CIDR block: 10.1.0.0/24 |* Name: ecs\-fw<br><br>* Private IP address: 10.1.0.10 |


**Table 2 TR**


|Instance name |TR route table |Association forwarding |Destination CIDR |Next Hop |Route type |
|---|---|---|---|---|---|
|tr01 |tr01\-rtb\-sys |attach\-vpc01<br><br>attach\-vpc02 |192.168.1.0/24 |attach\-vpc03 |Static routes |
||||172.16.1.0/24 |attach\-vpc03 |Static routes |
||tr01\-rtb\-set |attach\-vpc03 |192.168.1.0/24 |attach\-vpc01 |Route learning |
||||172.16.1.0/24 |attach\-vpc02 |Route learning |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created necessary VPCs and their subnets. For procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* You have created a custom route table for vpc03 and associated the custom route table with the subnet to which the ecs\-fw belongs. For procedure, see [Creating a route table](https://docs.byteplus.com/en/docs/vpc/Creating-a-custom-route-table) and [Associate a subnet](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-a-subnet#.5YWz6IGU5a2Q572R).

* You have created Elastic Compute Service (ECS) instances in all VPCs. For procedure, see [Purchasing an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* You have deployed a firewall in ecs\-fw, and allowed the CIDR blocks of vpc01 and vpc02 in the firewall.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you use Cloud Firewall, see <a href="https://docs.byteplus.com/en/docs/cloud_firewall/VPC_boundary_firewall_policy">VPC Border Firewall Policies</a> for detailed configuration.   </div>
   

* You have created required TR instances and their custom route tables. For procedure, see [Creating a Transit Router instance](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01) and [Creating a route table](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-03).


<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedures

<span id=".5q2l6aqk5LiA77ya5Yib5bu6VFLlrp7kvovkuI5WUEPkuYvpl7TnmoTnvZHnu5zlrp7kvovov57mjqU="></span>
### Step 1: Create an attachment between the TR instance and the VPC

Follow the procedure of [Creating a VPC attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpc) to create 3 VPC attachments, separately connecting vpc01, vpc02 and vpc03. The parameter values for this example are shown in the table below.


* **Basic configuration**

   
   |Parameter |Description |Value<br><br>(Attach vpc01) |Value<br><br>(Attach vpc02) |Value<br><br>(connecting to vpc03) |
   |---|---|---|---|---|
   |**Basic information** |||||
   |TR |Defaults to the selected TR instance, requiring no manual configuration. |tr01 |tr01 |tr01 |
   |Region |Default to the same region as the TR instance. No manual configuration required. |China (Guangzhou) |China (Guangzhou) |China (Guangzhou) |
   |Name |The name for the network instance attachment to be created. |attach\-vpc01 |attach\-vpc02 |attach\-vpc03 |
   |**Network instances** |||| |
   |Attachment type |Select the type for the network instance attachment to be created. |VPC |VPC |VPC |
   |VPC |Select the VPC instance to be connected. |vpc01 |vpc02 |vpc03 |
   |**Attachment point configuration** ||| | |
   |Availability Zone and Subnet |Select the entry point where TR connects to the VPC. Select the availability zone and then the subnet, and set the selected availability zone as the default availability zone.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This example uses a single availability zone, so only one subnet is selected. We recommend using multiple availability zones for greater reliability in actual scenarios.</div><br> |Availability Zone A, subnet01 |Availability Zone A, subnet02 |Availability Zone A, subnet03a |
   

* **Route configuration**

   
   |Parameter |Description |Example value (connecting to vpc01) |Example value (connecting to vpc02) |Example value (connecting to vpc03) |
   |---|---|---|---|---|
   |**Route configuration** ||| | |
   |Association forwarding |Enabling association forwarding means traffic from the network instance will be forwarded according to the route in this TR route table.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Take attach\-vpc01 as an example. After enabling association forwarding, the TR forwards traffic from vpc01 based on tr01\-rtb\-sys.</div><br> |Enabled, tr01\-rtb\-sys |Enabled, tr01\-rtb\-sys |Enabled, tr01\-rtb\-set |
   |Route propagation |After enabling route learning, the TR route table will automatically learn routes of the network instance, and generate entries with the next hop as this attachment.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Take attach\-vpc01 as an example. After you enable route learning, tr01\-rtb\-set automatically generates a route with the destination CIDR block as vpc01's subnet CIDR block and the next hop as attach\-vpc01</div><br> |Enabled, tr01\-rtb\-set |Enabled, tr01\-rtb\-set |Disable |
   |Auto Publish Route |Enabling auto publishing will automatically synchronize routes from the associated TR route table to all route tables within this VPC. These synchronized routes are marked as system routes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Take attach\-vpc01 as an example. After enabling route synchronization, TR automatically synchronizes the routes from tr01\-rtb\-sys to all the route tables in vpc01.</div><br> |Check |Check |Disable |
   


<span id=".5q2l6aqk5LqM77ya6YWN572uVFLot6_nlLHooag="></span>
### Step 2: Configure a TR route table


1. Configure routes in the TR system route table to forward access requests from vpc01 and vpc02 to vpc03.

   For procedure, see [Create a static route](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05#.5Yib5bu66Z2Z5oCB6Lev55Sx). The routes configured for this example are listed in the table below.

   
   |No. |Destination CIDR |Next Hop |
   |---|---|---|
   |1 |192.168.1.0/24 |attach\-vpc03 |
   |2 |172.16.1.0/24 |attach\-vpc03 |
   

2. Confirm whether the subnet routes of vpc01 and vpc02 exist in the TR custom route table.

   * Yes. Proceed to [Step 3: Configure a VPC route table](https://docs.byteplus.com/en/docs/transitrouter/Secure-intercommunication-between-different-VPCs#.5q2l6aqk5LiJ77ya6YWN572uVlBD6Lev55Sx6KGo).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">In this example, skip this step since route learning for the attachments connecting vpc01 and vpc02 is enabled in Step 1.      </div>
      

   * No. Follow the procedure of [Create a route learning rule](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-06#.5Yib5bu66Lev55Sx5a2m5Lmg) to create separate rules on the TR custom route table for attach\-vpc01 and attach\-vpc02. After configuration, the routes in the TR custom route table are as shown in the following table.

      
      |No. |Destination CIDR |Next Hop |
      |---|---|---|
      |1 |192.168.1.0/24 |attach\-vpc01 |
      |2 |172.16.1.0/24 |attach\-vpc02 |
      


<span id=".5q2l6aqk5LiJ77ya6YWN572uVlBD6Lev55Sx6KGo"></span>
### Step 3: Configure a VPC route table


1. Confirm whether the route tables of vpc01 and vpc02 contain a route with Next Hop as tr01.

   * Yes. Skip this step and proceed to Step 2.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Since Auto Publish Route is enabled for the attachment connecting vpc01 in Step 1, proceed to Step 2.      </div>
      

   * No. Follow the procedure of [Enable auto publishing](https://docs.byteplus.com/en/docs/transitrouter/Attachments-04) to enable Auto Publish Route for respective attachments (attach\-vpc01 and attach\-vpc02). After configuration, the auto\-published routes in the system route tables of vpc01 and vpc02 are as shown in the following table.

      
      |VPC name |Route entry type |Destination CIDR |Next Hop |
      |---|---|---|---|
      |vpc01 |System route |172.16.1.0/24 |tr01 |
      |vpc02 |System route |192.168.1.0/24 |tr01 |
      

2. Configure the vpc03 system route table to forward requests accessing vpc01 and vpc02 to ecs\-fw.

   Add the following routes to the vpc03 system route table. For procedure, see [Add a route](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry#70HRpqsH).

   
   |No. |Route entry type |Destination CIDR |Next Hop |
   |---|---|---|---|
   |1 |Custom route |192.168.1.0/24 |ecs\-fw |
   |2 |Custom route |172.16.1.0/24 |ecs\-fw |
   

3. Configure the vpc03 custom route table to forward requests accessing vpc01 and vpc02 to tr01.

   Enable Auto Publish Route for attach\-vpc03 by seeing [Enable auto publishing](https://docs.byteplus.com/en/docs/transitrouter/Attachments-04).

   After configuration, the following routes are automatically added to the vpc03 custom route table.

   
   |No. |Route entry type |Destination CIDR |Next Hop |
   |---|---|---|---|
   |1 |System route |192.168.1.0/24 |tr01 |
   |2 |System route |172.16.1.0/24 |tr01 |
   


<span id=".5q2l6aqk5Zub77ya6YWN572u5LqR5pyN5Yqh5ZmoZWNzLWZ35byA5ZCvSVDovazlj5Hlip_og73vvIjlj6_pgInvvIk="></span>
### Step 4: Configure ecs\-fw to enable IP forwarding (optional)


1. Log in to ecs\-fw. For procedure, see [Logging on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging on to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Execute the following command to review whether the ECS has IP forwarding enabled.

   ```Plain Text
   cat /proc/sys/net/ipv4/ip_forward
   ```
   

   * The response is **1**, indicating IP forwarding is enabled. No further steps are needed.

   * The response is **0**, indicating IP forwarding is not enabled. Continue with the following steps.

3. Execute the following command to open the `sysctl.conf` file.

   ```Plain Text
   vi /etc/sysctl.conf
   ```
   

4. Press `i` to enter edit mode, change the value of `net.ipv4.ip_forward` to 1 to enable IP forwarding.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the <code>sysctl.conf</code> file does not contain a <code>net.ipv4.ip_forward</code> field, manually add <code>net.ipv4.ip_forward = 1</code> at the end of the file.   </div>
   

5. Press `esc` to exit the edit mode, enter `:wq` to save and exit the file.

6. Execute the following command to restart the system for the configuration to take effect.

   ```Plain Text
   sysctl -p /etc/sysctl.conf
   ```
   


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation


1. Log in to the ECS instance (ecs01) in vpc01. For procedure, see [Logging on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging on to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Execute the `ping` command to connect the ECS within vpc02, verifying that vpc01 can access vpc02 properly.

   If the response is the same as the diagram below, access is normal.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a8eb908921c8e4f94d890ff685674b50.png) </span>

3. Similarly, log in to the ECS instance (ecs02) in vpc02 and execute the `ping` command to verify that vpc02 can access vpc01 properly.

4. Review the monitoring data of attach\-vpc03. If the inbound and outbound bandwidth is not 0, the mutual traffic between vpc01 and vpc02 is forwarded through vpc03.

   For procedure, see [Viewing monitoring data](https://docs.byteplus.com/en/docs/transitrouter/Monitoring-01).

5. Check the firewall to confirm that mutual traffic between vpc01 and vpc02 is scrubbed by the firewall.
