---
title: "Associating scaling configuration source with scaling group"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Associating-a-scaling-configuration-source-with-a-scaling-group"
---

This topic describes how to associate a scaling configuration source with a scaling group. For more information, see [Scaling configuration source](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-configuration-sources).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have [created a scaling configuration](https://docs.byteplus.com/en/docs/as/Managing_a_scaling_configuration), [created a launch template](https://docs.byteplus.com/en/docs/ecs/Creating-launch-templates), or [created a version of a launch template](https://docs.byteplus.com/en/docs/ecs/Creating-launch-template-versions).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* You can associate a scaling group with only one scaling configuration source. When you associate a new scaling configuration source with a scaling group, the old scaling configuration source will be automatically disassociated. In subsequent scaling activities, instances are created based on the new scaling configuration source. Existing instances in the scaling group will not be affected.

* Make sure that the instance type and image selected in the new scaling configuration are available in any availability zone selected for the scaling group.


<span id=".57uR5a6aL-abtOaNouS8uOe8qemFjee9rg=="></span>
## Associate or replace a scaling configuration

You can refer to this procedure to associate or replace a scaling configuration. To modify an associated scaling configuration, see [Change scaling configuration](https://docs.byteplus.com/en/docs/as/Managing_a_scaling_configuration#.5L-u5pS55Ly457yp6YWN572u).


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select "Scaling Configuration Sources \> Scaling configurations".

4. Click the "Associate scaling group" button to the right of the scaling configuration with which you want to associate the scaling group.

5. Click the "Confirm" button to complete the operation.


<span id=".57uR5a6aL-abtOaNouWQr-WKqOaooeadvw=="></span>
## Associate or replace a launch template

Make sure that the new instance launch template meets the following conditions. Otherwise, you cannot associate the new template or replace the old one successfully.


* The image, security group, and key parameters are configured in the template. The security group in the template belongs to the same VPC as the scaling group.

* If a VPC is selected in the template, the VPC must be the same as the VPC of the scaling group. If a subnet is selected in the template but the subnet differs from the subnet of the scaling group, the subnet of the scaling group is used. If a VPC or subnet is not selected in the template, the VPC or subnet of the scaling group is automatically inherited.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently, associating a launch template configured with a Windows image is not supported.</div>


* <div data-tips="true" data-tips-type="tip">Scaling groups do not currently support creating non\-Pay\-as\-you\-go and non\-Spot instances, or EIPs with a billing method other than Pay\-as\-you\-go. Therefore, when a launch template configured with a billing method other than pay\-as\-you\-go is associated with a scaling group, the instance billing method is automatically changed to <a href="https://docs.byteplus.com/en/docs/ecs/Pay-as-you-go">pay\-as\-you\-go</a>, and the EIP billing method is automatically changed to <a href="https://docs.byteplus.com/en/docs/eip/Pay-as-you-go#.5oyJ5bim5a695LiK6ZmQ6K6h6LS5">pay\-as\-you\-go – pay\-by\-bandwidth</a>.</div>


* <div data-tips="true" data-tips-type="tip">If you associate the default version or the latest version of a launch template, changes to the version configuration will not affect the association status. However, when the scaling group creates instances, it will re\-validate the configuration. If the above conditions are not met, instance creation will fail.</div>



<span id=".6YCJ5oup5ZCv5Yqo5qih5p2_"></span>
### Select a launch template

You can select only one launch template for a scaling group. When you select a launch template, the template is associated with the scaling group.


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. Click the name of the scaling group and select "Scaling Configuration Sources \> Launch Templates".

3. Click the "Select Launch Template" button and select a launch template and template version.

4. Click the "Confirm" button to complete the operation.


<span id=".5L-u5pS55ZCv5Yqo5qih5p2_"></span>
### Replace a launch template

After you select a launch template, you can replace it with a new template or template version based on your needs. After you replace a launch template or template version, the new configuration will only apply to subsequent instance creations using this template or version. It will not impact existing instances in the scaling group.


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. Click the name of the scaling group and select "Scaling Configuration Sources \> Launch Templates".

3. Click "Modify the Launch Template" to the right of the launch template, select a new launch template or template version, and modify the extended launch template configuration. For more information, see [Creating scaling groups](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The extended launch template configuration is used to select multiple instance types, configure their weights, and adjust priorities. After the extended launch template configuration is modified, a <a href="https://docs.byteplus.com/en/docs/as/Health-checks">health check</a> will be triggered immediately to adjust the instance configuration in the scaling group.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This capability is currently in Beta. To apply for a trial, contact your account manager.   </div>
   

4. Click the "Confirm" button to complete the operation.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [ModifyScalingConfiguration](https://docs.byteplus.com/en/docs/as/ModifyScalingConfiguration): Modifies scaling configuration

* [EnableScalingConfiguration](https://docs.byteplus.com/en/docs/as/EnableScalingConfiguration): Replace scaling configuration
