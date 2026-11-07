---
title: "Creating scaling group"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

This topic describes how to create a scaling group, including how to define the instance count/vCPU capacity, cooldown time, and subnet of the scaling group.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

<span id=".5Yib5bu65ZCM5pe257uR5a6a6LSf6L295Z2H6KGh"></span>
### Create a scaling group and associate it with a load balancer

When you create a scaling group, if you want to associate a load balancer with it, confirm that you have a Load Balancer instance in the same VPC as the scaling group and that the instance is in **Normal** status. Refer to [CLB quick start](https://docs.byteplus.com/en/docs/clb/Getting-Started) or [ALB quick start](https://docs.byteplus.com/en/docs/clb/ALB-quick-start-Overview) to complete the initialization of the corresponding Load Balancer instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can associate a load balancer with multiple scaling groups. You can also associate a scaling group with multiple load balancers. After you associate a scaling group with a load balancer, instances in the scaling group will be automatically added to one or more specified backend server groups under the load balancer.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the "Create Scaling Group" button to configure the basic information of the scaling group.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7b141620def4c4334ee71a24e34e131d.png) </span>

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Region |Select the region to which the scaling group and instances belong. |In this example, the default value China (Guangzhou) is used. |
   |Scaling Group Name |Configure the name of the scaling group. |as01 |
   

4. Configure the scaling configuration source, which serves as the configuration source for automatically scaling out instances in the scaling group.

   * Select "Not Settings": After the scaling group is created, you will need to create and associate a scaling configuration or select an instance launch template, and enable the scaling group before the scaling group can work as expected.

   * Select "Launch Template": After the scaling group is created, you can directly enable the scaling group.

      > For more information and limits on instance launch templates, see [Overview of scaling configuration source](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-configuration-sources).      
      

      The following table describes the related parameters.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ea2be37a42543e92bfd0766ea3e99b4e.png) </span>

      
      |Parameter​ |Description |Sample value |
      |---|---|---|
      |Select Launch Template/Select template version |You can select any version of the template. |\- |
      |Extended Launch Template Configuration |If you select "Enable", you can select multiple instance types and adjust their priorities.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is currently in Beta. To apply for a trial, contact your account manager.</div><br><br><br><br>* Priority: You can click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_147446bd47e7749a62c332864f7a0a53.png) </span> to the left side of "Selected instance types" and drag to sort the instance types.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the scaling group scales out, upon meeting the scaling policy requirements, if the higher\-priority instance type in the specified availability zone is out of stock or fails to be provisioned as expected, a lower\-priority instance type will automatically be used to create instances. For more information, see <a href="https://docs.byteplus.com/en/docs/as/Adding-instances-automatically">Automatically scaling out instances</a>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the scaling group scales in, upon meeting both the scaling policy and instance removal policy requirements, lower\-priority instances in the specified availability zone are removed first. For more information, see <a href="https://docs.byteplus.com/en/docs/as/Removing-instances-automatically">Automatically removing instances</a>.   </div><br>   <br><br>* Custom Weight: A weight specifies the unit capacity occupied by each instance type in the scaling group. You can customize the weight of each instance type. We recommend that you define the weight based on the contribution of each instance type to actual application performance. The default weight is the number of vCPUs of the instance type.<br><br>   For example: If the weight of the g2a instance type is set to 20, three g2a instances will occupy 60 units of capacity in the scaling group. |Enable |
      

5. Configure the instance count information for the scaling group. You can configure the capacity only when you select "Enable" for "Extended Launch Template Configuration" in the previous step.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1aa616c2e3fd28f24e9113ec785864e9.png) </span>

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Minimum Number of Instances/Minimum Capacity |The minimum value for the instance count or capacity in the scaling group.<br><br><br>* When Auto Scaling executes an adjustment, Auto Scaling will automatically ensure that the instance count or capacity in the scaling group is not less than the value of this parameter.<br><br>* After the scaling group is created, you can manually [ or capacity](https://docs.byteplus.com/en/docs/as/Modifying-the-instance-number-capacity-of-a-scaling-group)[ or capacity](https://docs.byteplus.com/en/docs/as/Modifying-the-instance-number-capacity-of-a-scaling-group) based on your needs. |1 |
   |Maximum Number of Instances/Maximum Capacity |The maximum value for the instance count or capacity in the scaling group.<br><br><br>* When the scaling group executes an adjustment, Auto Scaling automatically ensures that the instance count in the scaling group does not exceed the value of this parameter. However, the instance capacity in the group may be slightly greater than the value of this parameter. This is because:<br><br>   If the maximum capacity is not perfectly divisible by the weight of the highest\-priority instance type, the value will be rounded up to meet the computing power requirement. For example, if the maximum capacity is set to 100 and the weight of the highest\-priority instance type is 30, 4 instances will ultimately be provisioned when scale\-out is triggered, resulting in an actual scaling group capacity of 120.<br><br>* After the scaling group is created, you can manually [modify the instance count](https://docs.byteplus.com/en/docs/as/Modifying-the-instance-number-capacity-of-a-scaling-group) based on your needs.<br><br>* The default upper limit for the maximum number of instances is 100. You can raise the upper limit in the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=Auto_Scaling), with a maximum allowable value of 1000. |1 |
   |Expected Number of Instances/Expected Capacity |Configure the expected instance count or capacity in the scaling group and enable the expected instance count feature. For more information, see [Expected instance count/capacity](https://docs.byteplus.com/en/docs/as/Desire-instance-number-capacity).<br><br><br>* The expected instance count or capacity must be greater than or equal to the minimum instance count or capacity and less than or equal to the maximum instance count or capacity.<br><br>   However, when the scaling group executes an adjustment, the actual capacity of the scaling group may be slightly greater than the value of this parameter. This is because:<br><br>   If the expected capacity is not perfectly divisible by the weight of the highest\-priority instance type, the value will be rounded up to meet the computing power requirement. For example, if the expected capacity is set to 100 and the weight of the highest\-priority instance type is 30, 4 instances will ultimately be provisioned, resulting in an actual scaling group capacity of 120.<br><br>* After the scaling group is created, you can [modify the expected instance count](https://docs.byteplus.com/en/docs/as/Modifying-the-instance-number-capacity-of-a-scaling-group). |1 |
   |Cooldown Time |The cooldown time after the scaling group executes an adjustment. For more information, see [Cooldown time](https://docs.byteplus.com/en/docs/as/Cooldown-period).<br><br>During the cooldown time, the scaling group will reject adjustments triggered by scheduled, periodic, or alert\-based scaling rules. Adjustments triggered by other conditions, such as manual scaling or instance count checks, can proceed as expected. |300s |
   

6. Configure the network configuration information for the scaling group.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d7379a9f9c824ffad24921c4a35b2a15.png) </span>

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Virtual Private Cloud |Select the VPC to which the instances belong. After the scaling group is created, you cannot change the VPC. |vpc01 |
   |Subnet |Select the subnet to which the instance belongs.<br><br><br>* To meet high availability and disaster recovery requirements, we recommend that you select multiple subnets in different availability zones.<br><br>* To meet low latency requirements, we recommend that you select a single subnet and deploy instances in the same availability zone.<br><br>* You can change or add subnets after the scaling group is created. For more information, see [Modifying subnets of scaling group](https://docs.byteplus.com/en/docs/as/Modifying-the-subnets-of-a-scaling-group). |subnet02, subnet01 |
   |Associate/select Classic Load Balancer (CLB) |You can associate the scaling group with [a Classic Load Balancer (CLB) instance](https://docs.byteplus.com/en/docs/clb/Product-Overview-01) based on your needs, add backend server groups to the instance, and configure ports and weights for each instance.<br><br><br>* A single CLB supports up to 20 backend server groups, and all CLBs support a maximum of 100 backend servers, suitable for scenarios where a single instance provides multiple types of services.<br><br>* You can also associate or replace a load balancer for the scaling group after the scaling group is created. For more information, see [Configuring load balancer associated with scaling group](https://docs.byteplus.com/en/docs/as/Configuring-the-load-balancer-associated-with-a-scaling-group). |Associate CLB instance, lb01, rs01, 8080, 50 |
   |Associate ALB Instance/Please select an ALB instance |You can associate the scaling group with an [Application Load Balancer (ALB) instance](https://docs.byteplus.com/en/docs/clb/Introduction), add server groups to the instance, and configure ports and weights for the server groups.<br><br><br>* A single ALB supports up to 20 server groups. All ALBs can cumulatively support up to 100 backend servers, which is suitable for a scenario where a single instance provides multiple types of services.<br><br>* You can also associate or replace a load balancer for the scaling group after the scaling group is created. For more information, see [Configuring load balancer associated with scaling group](https://docs.byteplus.com/en/docs/as/Configuring-the-load-balancer-associated-with-a-scaling-group). |Not Associated |
   

7. Configure the policy configuration information for the scaling group.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_280e5d1507bc794aa80e00d75ec95de5.png) </span>

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Scaling Policy |If you select multiple subnets, this parameter is required. After you create the scaling group, you can change the scaling policy based on your needs.<br><br><br>* For automatically triggered adjustments:<br><br>   * Priority policy: The scaling group sorts the availability zones by the order in which you select subnets. The availability zone corresponding to the first selected subnet has the highest priority. In this example, subnet02 has the highest priority.<br><br>      When the scaling group scales out, instances are preferentially deployed in availability zones with higher priority. When the scaling group scales in, instances are preferentially removed from availability zones with lower priority.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If instances cannot be scaled in the target availability zone, other availability zones are selected in order of priority.      </div><br>      <br><br>   * Balanced policy: When the scaling group scales out or in, instances are randomly deployed or removed to ensure that instances in the scaling group are as evenly distributed as possible across all availability zones.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If instances cannot be scaled in the target availability zone, other availability zones are randomly selected.      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If instances cannot be scaled out in the original availability zone, other availability zones are selected in order of priority when "Priority policy" is selected, and randomly selected when "Distributed policy" is selected.      </div><br>       |Priority policy |
   |Scaling mode |When the scaling group [automatically removes instances](https://docs.byteplus.com/en/docs/as/Removing-instances-manually) or [manually deletes instances](https://docs.byteplus.com/en/docs/as/Deleting-instances-manually), the reclaimed instance resources will follow the recycling mode setting here.<br><br><br>* Release mode: Removed instances are deleted with no resources retained.<br><br>* Shutdown recycling mode: Removed instances are disabled in Economical Mode, which reclaims the instance's computing resources (vCPU, GPU, and memory). However, to avoid data loss, the Volume, image, Elastic IP (EIP), and bandwidth (fixed bandwidth mode) are retained.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Do not retain application data, logs, etc., in the instances to avoid the risk of data loss after instance reclamation.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Currently, only Pay\-as\-you\-go instances without local volumes mounted (excluding EBM and HPC\-optimized instances) support Economical Mode.</div><br> |release: releases the instances. |
   |Advanced configuration |Configure the mixed billing methods for instances in the scaling group. You can combine any of the following methods to help reduce costs. This parameter takes effect only when "Spot" is selected for "Billing method" in [Scaling Configuration Sources](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-configuration-sources).<br><br><br>* Minimum Pay\-as\-you\-go Instances/Capacity: The minimum Pay\-as\-you\-go instance count or capacity in the scaling group. When the Pay\-as\-you\-go instance count or capacity in the scaling group is less than the value of this parameter, Pay\-as\-you\-go instances will be created first.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the expected instance count is less than the minimum Pay\-as\-you\-go instance count in the group, all instances in the group will be Pay\-as\-you\-go instances.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This parameter does not affect the final number of instances created in the scaling group. The number of instances is still limited by the instance count information.   </div><br>   <br><br>* Percentage of Pay\-as\-you\-go Instances: The proportion of Pay\-as\-you\-go instances in the scaling group. When the percentage is calculated, the Pay\-as\-you\-go instances corresponding to the minimum Pay\-as\-you\-go instance count in the group are not included.<br><br>* Spot Expiration Replacement: If you select "Enable", about 5 minutes before a spot instance is reclaimed, the scaling group will proactively create a new spot instance to replace the current spot instance.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The current spot instance will be identified as abnormal by the health check feature and removed 5 minutes later.   </div><br>   <br><br>* Use Pay\-as\-you\-go Instances Supplement Spot Capacity: When the [automatic scale-out policy](https://docs.byteplus.com/en/docs/as/Adding-instances-automatically) is met, if spot instances are sold out, Pay\-as\-you\-go instances of the same instance type will be created to meet the scale\-out demand.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the scaling group scales in, supplementary Pay\-as\-you\-go instances will be removed first, and then other instances will be removed based on the <a href="https://docs.byteplus.com/en/docs/as/Removing-instances-manually">automatic scale\-in policy</a>.   </div><br>    |Turn on. Minimum Pay\-as\-you\-go Instances: 3. |
   |Scale\-In Policy |During [automatic scale-instances](https://docs.byteplus.com/en/docs/as/Removing-instances-manually), AS removes instances from the scaling group according to this policy. <br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When both the instance removal policy and the scaling policy exist, the scaling policy is executed first.</div><br> |Earliest instance created from earliest scaling configuration |
   |Select Message Notification |If you select an option, you can receive notifications of scaling results via internal messages, SMS, or email. This way, you can timely learn changes in the scaling group.<br><br><br>* If you do not select an option, message notification will not be used. You can enable message notification later by referring to [Creating message notification](https://docs.byteplus.com/en/docs/as/Managing_message_notifications#.5Yib5bu65raI5oGv6YCa55-l).<br><br>* After you select an option, a message notification will be automatically created. To receive notifications successfully, you also need to configure the message delivery method and recipients. For more information, see [Configuring message notification](https://docs.byteplus.com/en/docs/as/Managing_message_notifications). |Scaling activity failed |
   |Instance Health Check |* When instance health check is enabled for the scaling group, each instance that joins the scaling group immediately has instance health check enabled. Instance health check monitors the running status of instances every 5 minutes. If an instance is in **Error** status, it is considered abnormal. The scaling group will automatically remove or delete abnormal instances.<br><br>* When instance health check is disabled, the scaling group will not process abnormal instances. |Enable |
   



&nbsp;

8. Configure the advanced configuration information for the scaling group.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aeb90e0db937888c4dbcc3b9296f46a4.png) </span>

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Project |(Optional) Select a project based on your needs. A project is a collection of resources. You can add the new instance to a project and manage it centrally at the project level, which helps keep resources independent and maintain data security.<br><br><br>* The default value is empty, indicating that the scaling group is not added to any project.<br><br>* A resource can belong to only one project.<br><br>* After a project is selected, the scaling group can only be used by users with permissions for that project.<br><br>* If you associate a project to a scaling group when you create the scaling group, resources subsequently created or selected for the scaling group, such as ECS instances, EIPs, VPCs, and load balancers, must also belong to this project.<br><br>* If a project is already selected in the top menu bar before the "Create Scaling Group" pop\-up window is displayed, the created scaling group is associated with the selected project by default. To associate the created scaling group with another project, exit the "Create Scaling Group" pop\-up window and change the project to "All Resources" or the target project in the top menu bar.<br><br>* If no other projects are available, click "new project" to[create a project](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management#creating-project) in the IAM console. After you create the project, return to the creation page and select the created project. |default |
   |Tag |A tag consists of a key\-value pair and is used for categorizing and searching resources.<br><br>Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1d3e137a7fd2eeff405adbc924499ba3.png) </span> icon and enter the tag key and tag value to add a tag to the scaling group. |* Tag key: as\-key<br><br>* Tag value: as\-test |
   

9. Click the "OK" button to complete the operation.


At this point, a scaling group is created and is in **Disabled** status. Subsequently, you need to create a scaling configuration and associate it with the scaling group. The scaling group will work as expected only after being enabled. For more information, see [Creating scaling configuration](https://docs.byteplus.com/en/docs/as/Managing_a_scaling_configuration) and [Enabling scaling group](https://docs.byteplus.com/en/docs/as/Enabling-a-scaling-group).

<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations


* You need to [associate a scaling configuration source](https://docs.byteplus.com/en/docs/as/Associating-a-scaling-configuration-source-with-a-scaling-group) with the scaling group to define the compute, storage, network, and security capabilities of cloud resources such as ECS instances. This configuration will be used to create cloud resource instances during elastic scaling.

* After you associate a [scaling configuration source](https://docs.byteplus.com/en/docs/as/Associating-a-scaling-configuration-source-with-a-scaling-group) with the scaling group, you can view the Elastic Strength of the scaling group on the scaling group list page. Elastic Strength refers to the availability of compute resources within the scaling group. The more instance types configured in the group and the larger the stock of these types, the higher the Elastic Strength and the greater the scale\-out success rate.

   If Elastic Strength is weak, we recommend that you adjust the scaling group configuration in the following aspects:

   
   |Reason for weak Elastic Strength |Recommendation |
   |---|---|
   |The instance type has insufficient stock. |The selected instance type has insufficient stock. We recommend that you expand the range of instance types or select an instance type with adequate stock. |
   |The scaling group contains only spot instances, and no pay\-as\-you\-go instances are configured as a supplement. |If the scaling group contains only spot instances, we recommend that you configure Pay\-as\-you\-go instances as a supplement. |
   


<span id="yXIK6S8M"></span>
## Related documents

[CreateScalingGroup](https://docs.byteplus.com/en/docs/as/CreateScalingGroup)
