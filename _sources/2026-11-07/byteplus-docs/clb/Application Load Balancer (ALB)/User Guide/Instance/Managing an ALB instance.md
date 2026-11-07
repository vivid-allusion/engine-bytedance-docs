---
title: "Managing an ALB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Managing-instances"
---

This topic describes how to manage created ALB instances through the console, including viewing the instance list, viewing instance details, modifying basic instance information, deleting instances, and cloning instances.

<span id=".5pCc57Si5a6e5L6L"></span>
## View ALB instance list


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. In the left\-side navigation pane, select Instances.

4. On the **Instance** page, you can view information about the created instances, including Instance Name/ID, Status, Network Type, Associated VPC, Instance Domain Name, IP Address, Listeners, etc. Explanations for instance statuses are as follows:

   
   |**Instance state** |**State description** |**Action description** |
   |---|---|---|
   |Provisioning |The instance is being created. This is a transient status. |Modifying the instance configuration or deleting the instance is not allowed. |
   |Active |The instance is running normally. |Modifying the instance configuration or deleting the instance is allowed. |
   |Modifying |The configuration of the instance is being modified. This is a transient status. The instance enters the **Modifying**​ state when you perform the following operations:<br><br><br>* Change the instance basic information.<br><br>* Configure listener.<br><br>* Configure forwarding rule. |Modifying the instance configuration or deleting the instance is not allowed. |
   |Deleting |The instance is being deleted. This is a transient status. |Modifying the instance configuration or performing deletion again is not allowed. |
   


<span id=".5p-l55yL5a6e5L6L6K-m5oOF"></span>
## View ALB instance details


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the project and region.

3. In the left\-side navigation pane, select Instances.

4. Click the target ALB instance name to enter its details page.

5. You can search for a target instance using the instance name, instance ID, VPC ID, EIP, or private IP address.

6. View the instance details. For detailed parameter explanations, see the table below.

   
   |**Parameter** ||**Description** |
   |---|---|---|
   |Basic information |Name |The instance name. |
   ||Instance edition |Instance edition. Instances are categorized into Basic and Standard editions. For a feature comparison between different versions, see [Instance edition comparison](https://docs.byteplus.com/docs/clb/Comparison-between-instance-editions). |
   ||Delete protection |The status of the "Delete protection" feature.<br><br>Delete Protection:​ Once enabled for an instance, it cannot be deleted via the console or API. You can delete the instance normally after disabling this function. |
   ||Modification Protection |Status of the "Modification protection" feature.<br><br>Modification Protection:​ Once enabled for an instance, its configuration cannot be modified via the console, but can still be modified via API. Instance configuration includes the basic instance information and the configuration of its resources, such as listeners and forwarding rules. |
   ||Reason for modification protection |Reason for enabling the "modification protection" feature. |
   ||ID |Instance ID. The instance ID is assigned by the system. |
   ||Regions |The region where the instance resides. |
   ||Tags |The tags bound to the instance. Tags are used to label resources, enabling you to categorize and aggregate resources for management. |
   ||Description |Description of the instance. |
   ||Project |The project to which the instance belongs. |
   ||Instance domain name |The instance domain name. The instance domain name is assigned by the system. For more information, see [Adding a CNAME record pointing to the instance domain name](https://docs.byteplus.com/docs/clb/Configuring-domain-name-resolution). |
   ||Back\-to\-source routing |A subnet assigned to the instance by the system. When an instance is associated with IP\-type backend servers across VPCs, you must manually configure routes for the backend server responses to return to the instance. In these routes, the instance's CIDR block should be set as the destination address. For more information, see [ALB cross-VPC backend server attachment](https://docs.byteplus.com/docs/clb/Mounting-back-end-servers-to-an-ALB-instance-across-VPCs). |
   |Network Configuration |IP type |The type of IP address bound to the instance. There are two IP address types: IPv4​ and IPv4/IPv6 Dual\-Stack. For more information on IP address types, see [Instance IP type](https://docs.byteplus.com/docs/clb/type_of_instance#1ebc9688). |
   ||Network type |Instance network type.<br><br><br>* **Public**: Internet instances have both EIP and private IP addresses. An Internet\-facing instance can be accessed from the Internet and by resources within its VPC.<br><br>* **Private**: A private instance has only a private IP address and can be accessed only by resources within its VPC.<br><br><br>You can change the instance network type. For detailed steps, see [Changing the ALB instance network type](https://docs.byteplus.com/docs/clb/Associating-and-disassociating-an-elastic-IP). |
   ||VPC |VPC to which the instance belongs. |
   ||Availability zone |The availability zone where the instance resides. The instance subnet and IP address are also displayed here.<br><br>You can click **Edit Availability Zone** to modify the Availability Zone of the instance.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When modifying Availability Zones, you must retain at least one Availability Zone where the instance currently resides.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">To use "edit availability zone" feature, please contact your account manager.</div><br> |
   |Log delivery |Access log delivery to TOS |Status of the "Access log delivery to TOS" feature. When enabled, ALB will deliver the instance's access logs to your specified Torch Object Storage (TOS) bucket. You can use access logs to troubleshoot failures, analyze user profiles, and more. For more information, see [Access log delivery to TOS](https://docs.byteplus.com/docs/clb/Sending-access-logs-to-TOS).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you want to use this feature, please contact your account manager to apply.</div><br> |
   ||Health check log |The status of the "health check log delivery" feature. When enabled, ALB will deliver the instance's health check logs to Torch Log Service (TLS). You can use health check logs to troubleshoot health check issues. For more information, see [Health check log](https://docs.byteplus.com/docs/clb/Health-check-logs). |
   |WAF protection ||Status of the "WAF protection" feature. When enabled, the Web Application Firewall (WAF) monitors traffic directed to the ALB and blocks malicious traffic. For more information, see [WAF protection](https://docs.byteplus.com/docs/clb/WAF-protection). |
   |Global Accelerator ||The status of the Global Accelerator feature. When enabled, the Global Accelerator (GA) service accelerates the transmission of your application data. For more information, see [Enabling Global Accelerator for ALB instances](https://docs.byteplus.com/docs/6406/1351431). |
   


<span id="m9WC9VbP"></span>
## Modify ALB instance basic information


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the project and region.

3. In the left\-side navigation pane, select Instances.

4. Click the target ALB instance name to enter its details page.

5. On the **Basic Information** tab, modify the instance name, tags, description, and other information as needed.

6. Click **Confirm** to complete the action.


<span id="c2d02f0e"></span>
## Configure "Delete protection" feature

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After enabling the "Delete Protection" function for an ALB instance, you will not be able to delete the instance via the console or API. You can delete the instance normally after disabling this function.</div>



1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the project and region.

3. In the left\-side navigation pane, select Instances.

4. Click the target ALB instance name to enter its details page.

5. On the **Basic Information** tab, toggle the **Delete protection** switch to enable or disable the "delete protection" feature.


<span id="0b971da8"></span>
## Configure "modification protection" feature

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After enabling the "Modification Protection" function for an ALB instance, you cannot modify the instance configuration via the ALB console, but you can modify it via API.</div>



1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the project and region.

3. In the left\-side navigation pane, select Instances.

4. Click the target ALB instance name to enter its details page.

5. On the **Basic information** tab, toggle the **Modification protection** switch to enable or disable the "Modification Protection" function. After enabling "Modification Protection", you can provide a reason for enabling it.


<span id=".5Yig6Zmk5a6e5L6L"></span>
## Delete ALB instance

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* No listeners exist within the ALB instance. If any exist, please [Delete listeners](https://docs.byteplus.com/en/docs/clb/Managing-listeners).

* The ALB instance has WAF protection enabled. If enabled, please [Disable WAF protection](https://docs.byteplus.com/en/docs/clb/WAF-protection).

* Delete protection is not enabled for the ALB instance. If enabled, please [Disable delete protection](https://docs.byteplus.com/en/docs/clb/Managing-instances).

* Global Accelerator is not enabled for the ALB instance. If it is enabled, please [Disable Global Accelerator feature](https://docs.byteplus.com/en/docs/6406/1351431).


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar. Select the target project and region.

3. In the left\-side navigation pane, select Instances.

4. Click **Delete** on the right side of the target ALB instance.

5. Click **Delete** to complete the action.
