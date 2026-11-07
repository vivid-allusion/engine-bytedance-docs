---
title: "Quickly creating scaling tasks"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Quick-start"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

In this topic, a scheduled scaling task configured with [CLB](https://docs.byteplus.com/en/docs/clb/Product-Overview-01) is used as an example to describe how to quickly create a scheduled task.

Your website requires two instances for daily operation. You plan to start a multi\-day promotion that needs three additional instances. After the promotion, the additional instances are no longer needed.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have completed the preparation steps by following the [quick start](https://docs.byteplus.com/en/docs/as/Preparations). The planned resources are as follows:


* CLB instance lb01 and backend server group rs01.

* VPC vpc01 and subnet subnet01.

* The port used by the instance to provide services externally is 8080. Traffic is expected to be evenly distributed across all instances.

* When using the Auto Scaling service for the first time, you need to enter the Auto Scaling console and click the "Authorize" button to confirm "Cross\-service access authorization". This allows the service to use products such as ECS instances.


<span id=".5q2l6aqk5LiA77ya5Yib5bu65Ly457yp57uE"></span>
## Step 1: Create a scaling group


1. Log in to the[ Auto Scaling console](https://console.byteplus.com/as/group). 

2. Click the "Create Scaling Group" button to enter the Create Scaling Group page.

3. Configure the basic information of the scaling group.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7b141620def4c4334ee71a24e34e131d.png) </span>

   
   |Parameter​ |Description |Example value |
   |---|---|---|
   |Region |Select the region to which the scaling group and instances belong. |Keep the default value "China (Guangzhou)" |
   |Scaling group name |Enter the name of the scaling group. |as01 |
   

4. Configure the instance configuration source of the scaling group. Here, select "Not set now".

5. Configure the quantity information of the scaling group.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7c681ef8e5b71479c922a479cb379f22.png) </span>

   
   |Parameter​ |Description |Example value |
   |---|---|---|
   |Minimum Number of Instances |The minimum number of instances in the scaling group. |In the example provided in the topic, the number of instances is set to "2" for daily operations |
   |Maximum Number of Instances |The maximum number of instances in the scaling group. |In the example provided in the topic, the maximum number of instances is set to "5" for daily operations |
   |Expected Number of Instances |The fixed value for the number of instances in the scaling group. |Do not configure |
   |Cooldown Time |Cooldown time after the scaling group executes an adjustment job. |Keep the default value "300s" |
   

6. Configure the network information of the scaling group.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d7379a9f9c824ffad24921c4a35b2a15.png) </span>

   
   |Parameter​ |Description |Example value |
   |---|---|---|
   |VPC |Select the VPC to which the scaling group and the instances belong. |vpc01 |
   |Subnet |Select the subnet to which the scaling group and instances belong. |Select the subnet "subnet01" |
   |Associate/select Classic Load Balancer (CLB) |Associate the scaling group with [Classic Load Balancer (CLB)](https://docs.byteplus.com/en/docs/clb/Product-Overview-01), select the backend server group, and specify the port and weight for the instances (one or more). |Associate CLB instance lb01, specify backend server group rs01, and set the port and weight to 8080 and 50, respectively |
   |Associate/select Application Load Balancer (ALB) |Associate the scaling group with [ALB](https://docs.byteplus.com/en/docs/clb/Introduction). In the example provided in the topic, this option is not selected. |Not Associated |
   

7. Configure the policies of the scaling group.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7f81241dcc68387926cfbd141d56b01e.png) </span>

   
   |Parameter​ |Description |Example value |
   |---|---|---|
   |Scaling Policy |When multiple subnets are selected for the scaling group, you can use this parameter to configure the target availability zone for the instances involved in adjustments. Since this topic uses one selected subnet as an example, keep the default option. |Priority policy |
   |Instance reclaim policy |AS removes instances from the scaling group according to this policy. |Release Mode |
   |Instance removal policy |When the scaling group scales in, the instances to be moved out are selected based on the specified scale\-in policy. |Keep the default value "Earliest instance created from earliest scaling configuration" |
   |Select message notification |After this option is selected, you can receive notifications of scaling results via internal messages, SMS, or email. This way, you can timely learn changes in the scaling group. |Keep the default options selected |
   |Instance Health Check |After you check this option, once an instance joins a scaling group, the health check feature is enabled immediately. The instance status is monitored every 5 minutes. If an instance shows an **Error** status, it is marked as unhealthy, and the scaling group will automatically remove the unhealthy instance. |Keep the default value "Enable" |
   

9. Configure the advanced option of the scaling group.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aeb90e0db937888c4dbcc3b9296f46a4.png) </span>

   
   |Parameter​ |Description |Example value |
   |---|---|---|
   |Project |Select the project to which the scaling group belongs. |Keep the default value, which is an empty value |
   |Tag |A tag consists of a key\-value pair and is used for categorizing and searching resources. |Keep the default value, which is an empty value |
   

9. Click the "Confirm" button to complete the operation. 


At this point, the scaling group is successfully created and is in **Inactive** status.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_104b105b0b36a5d6f125f8752a794979.png) </span>


<span id=".5q2l6aqk5LqM77ya5Yib5bu65Ly457yp6YWN572u"></span>
## Step 2: Create scaling configuration


1. Click the "Add scaling configuration source" button to enter the "Scaling Configuration Sources" tab.

2. Select the "Scaling configurations" tab and click the "Create Scaling Configuration" button to enter the Create Scaling Configuration page.

3. The parameters required to create the scaling configuration are generally the same as those for purchasing an ECS instance. The following table describes the parameters specific to scaling configuration creation. For more information, see [Purchasing ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   
   |Differential parameter |Description |Example value |
   |---|---|---|
   |Billing method |Select the instance billing method. |Pay\-as\-you\-go |
   |Region |This parameter uses the same region as the scaling group and cannot be modified. |\- |
   |Availability zone |This parameter uses the same availability zone to which the subnet of the scaling group belongs. In the example provided in this topic, this parameter is not shown. |\- |
   |Multi\-type |In the example provided in this topic, only one instance type is selected. Therefore, you do not need to check the "Multi\-type" option.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The supported instance types displayed in the console prevail.</div><br><br><br>* <div data-tips="true" data-tips-type="default">We recommended selecting instance types with normal stock to improve the scale\-out success rate.</div><br> |\- |
   |VPC/subnet |This parameter uses the same VPC and subnet as the scaling group and cannot be modified. |vpc01，subnet01 |
   |Secondary network interface |Instances created via a scaling group do not support associating secondary network interfaces |\- |
   |Purchase information |The number of instances in the scaling group is controlled by the scaling group and scaling rules, requiring no manual configuration. |\- |
   |Instance Names/Hostnames |You can configure ordered and unique names or hostnames for scale\-out instances. The configuration rules differ slightly from those for ECS instances. Refer to [Setting sequential and unique names or hostnames for instances](https://docs.byteplus.com/en/docs/as/Setting-sequential-and-unique-names-or-hostnames-for-instances). |\- |
   |Scaling configuration name |The name of the scaling configuration. |as\-con01 |
   |Status After Creation |Specify whether to immediately associate the scaling configuration with the scaling group upon creation. After this option is checked, scale\-out instances are created based on the scaling configuration. |Associate scaling group |
   

4. Click Create Now to complete the actions.


At this point, the scaling configuration is successfully created, automatically associated with the scaling group, and in the **Active ** status.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5d88e0e473bf1540199895043318e535.png) </span>

<span id=".5q2l6aqk5LiJ77ya5ZCv55So5Ly457yp57uE"></span>
## Step 3: Enable scaling group


1. Click the "Enable scaling group" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_60d837f5c25118a803d9ab92758f0186.png) </span>

2. Click the "Confirm" button to complete the operation.


At this point, the scaling group changes to the **Active** state, and two instances are automatically created based on the scaling configuration to meet your daily operational needs.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_44cb54dd071c0d6ae4370d1c6a56ed85.png) </span>

Click the current number of instances to view the created instances.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e580db44c29c3755894b264ba2e042b8.png) </span>

<span id=".5q2l6aqk5Zub77ya5Yib5bu65Ly457yp6KeE5YiZ"></span>
## Step 4: Create scaling rules

<span id=".5Yib5bu65omp5a656KeE5YiZ"></span>
### Create a scaling\-out rule


1. Click the name of the scaling group and select the "Scaling Rules" tab.

2. Click the "Create scaling rules" button to enter the Create Scaling Rules page.

3. Configure the relevant parameters based on the table below.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3bf06c97f172d003ce0c99b65f9acb5d.png) </span>

   
   |Parameter​ |Description |Example value |
   |---|---|---|
   |Rule Name |The name of the scaling rule. |as\-rule00 |
   |Rule Type |"Scheduled task" indicates executing adjustment at a specified time. |Scheduled tasks |
   |Trigger time |Select the trigger time for the adjustment.<br><br>You can click the "Select date" and "Select time" buttons to switch the selection page. After the time is selected, click the "Confirm" button to complete the configuration. |April 24, 2025 17:00 |
   |Adjustment |Specify the adjustment to be executed when the trigger time arrives. |Add instance, count: 1 |
   |Cooldown Time |The interval from the successful execution of an adjustment job based on the scaling rule (which is when the last instance completes the adjustment) to the next adjustment job becoming executable. |300s |
   |Status After Creation |Specify whether the scaling rule is enabled immediately upon creation. |Enable |
   

4. Click the "Confirm" button to complete the operation.


<span id=".5Yib5bu657yp5a656KeE5YiZ"></span>
### Create a scaling\-in rule


1. Click the name of the scaling group and select the "Scaling Rules" tab.

2. Click the "Create scaling rules" button to enter the Create Scaling Rules page.

3. Configure the relevant parameters based on the table below.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_796db145bc490588a2c28c79cb25a7ae.png) </span>

   
   |Parameter​ |Description |Example value |
   |---|---|---|
   |Rule Name |The name of the scaling rule. |as\-rule01 |
   |Rule Type |"Scheduled task" indicates executing adjustment at a specified time. |Scheduled tasks |
   |Trigger time |Select the trigger time for the adjustment.<br><br>You can click the "Select date" and "Select time" buttons to switch the selection page. After the time is selected, click the "Confirm" button to complete the configuration. |April 31, 2025 16:00<br><br> |
   |Adjustment |Specify the adjustment to be executed at the trigger time. |Reduce instances, count: 1 |
   |Cooldown Time |The interval from the successful execution of an adjustment job (which is when the last instance completes the adjustment) to the next adjustment job becoming executable. |300s |
   |Status After Creation |Specify whether the scaling rule is enabled immediately upon creation. |Enable |
   

4. Click the "Confirm" button to complete the operation. 


<span id=".5omn6KGM57uT5p6c"></span>
## Execution results


* After the scaling group is enabled, two instances are automatically created, bringing the total number of instances in the group to two.

* At April 24, 2025 17:00, one instance is automatically created, bringing the total number of instances in the group to three.

* At April 31, 2025 16:00, the number of instances is reduced by one, bringing the total number of instances in the group to two.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

We recommend configuring [scaling notifications](https://docs.byteplus.com/en/docs/as/Overview_of_notification_channels) for the scaling group. This allows you to learn the scaling status of instances in the group timely and manage scaling operations efficiently.
