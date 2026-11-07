---
title: "Associating instance launch templates with scaling groups"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Associating-launch-templates-with-Auto-Scaling"
---

<span id=".5LuA5LmI5piv5by55oCn5Ly457yp"></span>
## What is Auto Scaling (AS)?

[Auto Scaling (AS)](https://docs.byteplus.com/en/docs/as/What-is-Auto-Scaling) provides an on\-demand scalable pool of ECS instances, enabling you to flexibly handle short\-term high\-concurrency scenarios such as events, promotions, and flash sales. When business demand increases, AS automatically scales out ECS instances to ensure business capability. When business demand decreases, AS automatically scales in ECS instances to save resource costs. Intelligent, flexible scaling services enable your business to maintain optimal resource capacity whether during periods of fluctuation or stability, thus ensuring reliable business operations. Instance launch templates can serve as configuration templates for ECS instances in AS. This topic describes how to create a scaling group in the Launch Templates console.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* To associate an instance launch template with a scaling group, the instance launch template must meet the following requirements:

   * The image, security group, and key parameters are configured in the template. The security group in the template belongs to the same VPC as the scaling group.

   * If a VPC is selected in the template, the VPC must be the same as the VPC of the scaling group. If a subnet is selected in the template but the subnet differs from the subnet of the scaling group, the subnet of the scaling group is used. If a VPC or subnet is not selected in the template, the VPC or subnet of the scaling group is automatically inherited.

* When you create a scaling group, you cannot select a launch template that is associated with a Windows image.

* When you create a scaling group, you cannot select a launch template that is associated with the HPC\-optimized GPU instance type.

* Scaling groups do not support creating instances or EIPs with billing methods other than pay\-as\-you\-go. Therefore, when a launch template configured with a billing method other than pay\-as\-you\-go is associated with a scaling group, the instance billing method is automatically changed to [pay-as-you-go](https://docs.byteplus.com/en/docs/ecs/Pay-as-you-go), and the EIP billing method is automatically changed to [pay-as-you-go – pay-by-bandwidth](https://docs.byteplus.com/en/docs/eip/Pay-as-you-go#.5oyJ5bim5a695LiK6ZmQ6K6h6LS5).


<span id=".5Yib5bu65by55oCn5Ly457yp"></span>
## Create a scaling group


1. Log in to the [Launch Templates console](https://console.byteplus.com/ecs/template).

2. In the top menu bar, select a region.

3. In the template or version list, click the "Create Auto Scaling Group" button in the "Actions" column of the target template or version to navigate to the [Create Scaling Group](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group) page. You can refer to the parameter description for the scaling group to complete the configuration.

   The "Instance configuration source" parameter of the scaling group is automatically set to "Launch Template". The currently selected template or version is used.

   * If the default version is selected, "Always use the default version" is automatically selected.

   * If the latest version is selected, "Always use the latest version" is automatically selected.

   * If neither the default version nor the latest version is selected, "Use a custom version" is automatically selected.
