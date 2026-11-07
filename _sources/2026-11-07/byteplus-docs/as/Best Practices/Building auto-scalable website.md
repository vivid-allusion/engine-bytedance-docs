---
title: "Building auto-scalable website"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Building-a-website-that-scales-automatically"
---

This topic describes how to use Auto Scaling to build an auto\-scalable website application, which can automatically scale out or in instances during short\-term high\-concurrency scenarios. Such scenarios include campaigns, promotions and flash sales. Your business will maintain optimal resource capacity during traffic fluctuations and stable periods.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* In the example provided in this topic, the CentOS 7.6 operating system is used. Make sure that you have purchased a Linux instance and built a website as required. For information about how to build a website, see [Building website](https://docs.byteplus.com/en/docs/ecs/Building-websites).

* You have completed the preparation steps by following the [quick start](https://docs.byteplus.com/en/docs/as/Preparations). The planned resources are as follows:

   * CLB instance lb01 and backend server group rs01.

   * VPC vpc01 and subnet subnet01.

   * The port used by the instance to provide services externally is 8080. Traffic is expected to be evenly distributed across all instances.

* The created instance is not associated with an EIP or load balancer, and does not belong to any scaling group.


<span id=".5q2l6aqk5LiA77ya5Yib5bu65bey5pCt5bu6572R56uZ55qE6Ieq5a6a5LmJ6ZWc5YOP"></span>
## Step 1: Create a custom image of the website

You need to create a custom image based on the instance where your website is already deployed. When Auto Scaling automatically scales out instances, it will create new instances with the pre\-deployed website environment.


1. Remotely connect to and log in to the ECS instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Clear Cloud\-Init configuration.

   Execute the following command to delete the /var/lib/cloud file. This way, the Cloud\-init configuration is cleared. If you do not delete the file, information such as the hostname and password cannot be injected into ECS instances created by using the custom image.

   `rm -rf /var/lib/cloud`

3. Create a custom image from the instance.

   1. On the instance list page, click "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e3af353c483da5a7de52ae2f71a5e716.png) </span>\> Volumes & Image \> Create custom image" in the "Actions" column of the target instance.

   2. In the pop\-up window, enter the name of the custom image.

   3. Click the "Confirm" button and wait for the custom image to be created. Approximately 1 to 10 minutes are required to create a custom image.


<span id=".5q2l6aqk5LqM77ya5Yib5bu65a6e5L6L5ZCv5Yqo5qih54mI"></span>
## Step 2: Create an instance launch template

An instance launch template is a collection of instance configuration information used for quick instance purchase. We recommend that you use an instance launch template as the scaling configuration source.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the region of the target instance.

3. On the Instances page, click "... \> Instance settings \> Save as Template" in the "Actions" column of the instance.

4. Confirm the configuration information. If the configuration does not meet your business requirements, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fd2e651e3b950693bafee80a636bf56e.png) </span> icon to go to the corresponding configuration page. Pay special attention to the following configuration information to avoid subsequent operation failure:

   * The image selected for the instance is the custom image created in Step 1.

   * The login method should be "Key Pair", and a key pair must be selected.

5. After you confirm that all information is correct, enter the name of the launch template.

6. Click the "Create Now" button to complete the operation.


<span id=".5q2l6aqk5LiJ77ya5Yib5bu65Ly457yp57uE"></span>
## Step 3: Create a scaling group


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group).

2. Click the "Create Scaling Group" button to enter the scaling group creation page.

3. Configure the basic information of the scaling group.

   
   |Parameter​ |Description | |
   |---|---|---|
   |Region |Select the region to which the scaling group and instances belong. The region must the same as that of the created instances. |China (Beijing) |
   |Scaling Group Name |Configure the name of the scaling group. |as01 |
   

4. Configure the instance configuration source for the scaling group. In this example, "Launch Template" is selected and the template created in Step 2 is selected.

5. Configure the quantity information of the scaling group.

   
   |Parameter​ |Description |Example value |
   |---|---|---|
   |Minimum Number of Instances |The minimum number of instances in the scaling group. |In the example provided in the topic, the number of instances is set to "2" for daily operations |
   |Maximum Number of Instances |The maximum number of instances in the scaling group. |In the example provided in the topic, the maximum number of instances is set to "5" for daily operations |
   |Expected instance count |The fixed value for the number of instances in the scaling group. |Do not configure |
   |Cooldown time |The cooldown time after the scaling group executes an adjustment. |Keep the default value "300s" |
   

6. Configure the network configuration information for the scaling group.

   
   |Parameter​ |Description |Example value |
   |---|---|---|
   |Virtual Private Cloud |Select the VPC to which the scaling group and the instances belong. |Select the same VPC as the created instances. |
   |Subnet |Select the subnet to which the scaling group and instances belong. |You can select any subnet. |
   |Associate/select Classic Load Balancer (CLB) |Associate the scaling group with [Classic Load Balancer (CLB)](https://docs.byteplus.com/en/docs/clb/Product-Overview-01), select the backend server group, and specify the port and weight for the instances (one or more). |Associate CLB instance, lb01, rs01, 8080, 50 |
   |Associate ALB Instance/Please select an ALB instance |Associate the scaling group with an [ALB instance](https://docs.byteplus.com/en/docs/clb/Introduction). In this scenario, association is not required. |Not Associated |
   

7. Configure the policy configuration information for the scaling group.

   
   |Parameter​ |Description |Example value |
   |---|---|---|
   |Scaling Policy |When multiple subnets are selected for the scaling group, you can use this parameter to configure the target availability zone for the instances involved in adjustments. Since this topic uses one selected subnet as an example, keep the default option. |Priority policy |
   |Instance removal policy |When the scaling group scales in, the instances to be moved out are selected based on the specified scale\-in policy. |Keep the default value "Earliest instance created from earliest scaling configuration" |
   |Select Message Notification |If you select an option, you can receive notifications of scaling results via internal messages, SMS, or email. This way, you can timely learn changes in the scaling group. |In this example, no option is selected. |
   |Instance Health Check |After you check this option, once an instance joins a scaling group, the health check feature is enabled immediately. The instance status is monitored every 5 minutes. If an instance shows an Error status, it is marked as unhealthy, and the scaling group will automatically remove the unhealthy instance. |Keep the default value "Enable" |
   

8. Configure the advanced configuration information for the scaling group.

   
   |Parameter​ |Description |Example value |
   |---|---|---|
   |Project |Select the project to which the scaling group belongs. |Keep the default value, which is an empty value |
   |Tag |Select the tag to which the scaling group belongs. |Keep the default value, which is an empty value |
   

9. Click the "Confirm" button to complete the creation of the scaling group.


<span id=".5q2l6aqk5Zub77ya5ZCv55So5Ly457yp57uE"></span>
## Step 4: Enable the scaling group

After you enable the scaling group, scaling operations will be triggered immediately. The scaling group will scale out based on the minimum number of instances you specify, and monitor the instance status.


1. In the scaling group list, click the "Enable" button corresponding to the created scaling group.

2. Click the "Confirm" button to enable the scaling group.


<span id=".5q2l6aqk5LqU77ya5re75Yqg5bey5pyJ5a6e5L6L5Yiw5Ly457yp57uE"></span>
## Step 5: Add existing instances to the scaling group

This operation adds existing instances to the scaling group, where they will be subject to scaling group health checks to ensure normal business operation.


1. Click the name of the scaling group and select the "Instance Management" tab.

2. Click the "Add existing instance" button and select the instances you have created.

3. Do not select "Enable the scaling group to manage the instance lifecycle".

4. Click the "Confirm" button to complete the operation.


<span id=".5q2l6aqk5YWt77ya5Yib5bu65oql6K2m5Ly457yp6KeE5YiZ"></span>
## Step 6: Create alert\-based scaling rules

Alert\-based scaling rules monitor instance metric data and check if instance operation meets expectations once per minute. This enables dynamic scaling for sudden or unpredictable business scenarios, such as breaking hot news.


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group).

2. Click the name of the scaling group and select the "Scaling Rules" tab.

3. Click the "Create scaling rules" button to go to the page for adding scaling rules.

4. Configure the relevant parameters based on the table below.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Rule Name |The name of the scaling rule. |as\-rule01 |
   |Rule Type |Select "Alarm task", which specifies that adjustments are triggered based on monitoring metrics. |Alarm task |
   |Monitoring metric |Set the threshold for monitoring metric data. When the threshold is reached, an alert is triggered.<br><br><br>* To retrieve Agent monitoring metrics, you need to install the Agent plugin and complete authorization on the instance first. Otherwise, the monitoring metrics cannot be retrieved. For installation instructions, refer to [ECS monitoring overview](https://docs.byteplus.com/en/docs/cloudmonitor/Overview-1). |Average out\-of\-band CPU utilization \> 80%. This indicates that the average CPU usage of all instances in the scaling group exceeds 80%. |
   |Triggered After |When monitoring metric data reaches the threshold for several consecutive times, the adjustment is triggered. |3, which means the adjustment is triggered after three consecutive alerts. |
   |Adjustment |Specify the adjustment to be executed when the trigger time of the rule arrives. You can increase or decrease the scaling group capacity, or adjust the capacity to the specified amount. The adjustment amount can be set to an exact value or a percentage. |Add instances, 2 |
   |Cooldown time |The interval from the successful execution of an adjustment based on the scaling rule (which is when the adjustment is completed for the last instance) to the next adjustment becoming executable. During this period, services running on newly created instances can be initialized. |300s |
   |Status After Creation |Specify whether the scaling rule is enabled immediately upon creation. |Enable |
   

5. Click the "Confirm" button to complete the operation.

6. Repeat this step to create a scaling rule with the monitoring metric "Average out\-of\-band CPU utilization < 80%" and the adjustment "Reduce instances, 2".


<span id=".5omn6KGM57uT5p6c"></span>
## Execution results

The scaling group checks the operation status of each instance every minute and performs related operations based on the results:


* When the average out\-of\-band CPU usage of all instances exceeds 80%, the scaling group automatically creates 2 new instances based on the instance launch template configuration.

* When the average out\-of\-band CPU usage of all instances is below 80%, the scaling group automatically reduces 2 instances.

* When an instance is in the **Error** state, it is marked as abnormal and automatically deleted.

* When the number of instances in the scaling group is less than the minimum instance count requirement, the scaling group automatically creates new instances to meet the configured number.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

We recommend configuring [scaling notifications](https://docs.byteplus.com/en/docs/as/Overview_of_notification_channels) for the scaling group. This allows you to learn the scaling status of instances in the group timely and manage scaling operations efficiently.
