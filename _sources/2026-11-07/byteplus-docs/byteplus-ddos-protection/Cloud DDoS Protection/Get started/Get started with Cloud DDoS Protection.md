---
title: "Get started with Cloud DDoS Protection"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/Get_started_with_Cloud_DDoS_Protection"
---

To safeguard your cloud resources against DDoS attacks, you can use BytePlus Cloud DDoS Protection. This guide provides step\-by\-step instructions on how to purchase a protection instance, associate it with your Elastic IPs (EIPs), and configure protection rules to enable automatic, transparent security for your services.

<span id="38fd75ca"></span>
## Important notes

Please be aware that prepaid Cloud DDoS Protection subscriptions are non\-cancellable and non\-refundable once purchased.

<span id="8977eb6a"></span>
## Prerequisites


* Your BytePlus account is enterprise\-verified.

* You have an active BytePlus EIP. For purchase instructions, see [Apply for an EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).


<span id="f147827f"></span>
## Step 1: Create a Cloud DDoS Protection instance

Before using the service, you must purchase a protection instance. Cloud DDoS Protection is available with a subscription (annual/monthly) billing model. For detailed billing information, please refer to [Billing details of Cloud DDoS Protection](https://docs.byteplus.com/docs/byteplus-ddos-protection/Billing_details_of_Cloud_DDoS_Protection).


1. Log in to [Cloud DDoS Protection Console](https://console.byteplus.com/ddos-protection/).

2. In the left navigation pane, select **Cloud DDoS Protection \> Instance list**.

3. Click **Purchase Cloud DDoS Protection Instance**.

4. Select your desired specifications.

   
   |Configuration ||Description |
   |---|---|---|
   |Basic information |Product type |Select **Cloud DDoS Protection**. |
   ||Region |The region where the instance IP is located.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">Protection is limited to cloud resources within the same region and does not support cross\-region protection.</div><br> |
   ||Specifications |Select **Advanced Edition**. |
   ||Billing model |**Subscription** |
   |Basic specifications |Provisioning mode |Transparent access. No DNS changes are required. The service directly protects BytePlus resources bound to public IPs. |
   ||Protected resources |ECS, NAT Gateway, CLB, WAF, and other standard cloud products. |
   ||Bandwidth type |BGP |
   ||Protection capabilities |Integrates with cloud resources to provide comprehensive protection and supports rules customized by experts. |
   |Protection plan |Protection capability |Cloud DDoS Protection includes **50 protected IP addresses** and **50 Mbps of protected business bandwidth** by default. |
   ||Protected IPs |The number of IP addresses that can be added to a single instance.<br><br><br>* **Default: 50**. Can be expanded for an additional fee.<br><br>* **Maximum: 500** per instance. |
   ||Bandwidth |* The amount of clean business traffic after it is scrubbed by the Cloud DDoS Protection engine. Your business bandwidth must be greater than the peak value of either the traffic to origin or the outbound traffic of the instance. If your actual traffic consistently exceeds the business bandwidth you purchased for the Cloud DDoS Protection instance, packet loss may occur and affect your services. We recommend that you adjust the business bandwidth promptly.<br><br>* A single instance provides 50 Mbps of business bandwidth by default. Expansion is supported, and the expanded portion is billed on a tiered basis. Each 50 Mbps expansion is billed at a rate determined by the new total business bandwidth tier. The total business bandwidth is the sum of the bandwidth included in the default full protection plan and the expanded bandwidth. That is, **Total business bandwidth** = **Default business bandwidth (50 Mbps)**  + **Expanded business bandwidth**.<br><br>* A single instance can protect a business bandwidth of up to 20 Gbps (20,000 Mbps). |
   ||Quantity |The total number of instances to purchase. |
   ||Project |Project is a grouping mechanism provided by BytePlus to help achieve logical resource isolation. You can use resource projects for management operations such as project\-based authorization and bill management. |
   |Duration ||* The duration of protection for the service.<br><br>* If you select **Auto\-renewal**, the instance will be automatically renewed monthly based on the current instance specifications seven days before it expires. |
   |Service agreement ||By checking this box, you acknowledge that you have read and agree to the relevant terms, agreements, and their explanations. |
   

5. After completing the setup, click **Create Instance** to go to the order confirmation page.

6. After confirming that the information is correct, click **Next** to pay for the order.


After payment is completed, you can go to the **Instance List** to view instance details.

<span id="c89b73e8"></span>
## Step 2: Add EIPs to your instance

Cloud DDoS Protection instances protect your BytePlus Elastic IPs (EIPs). If you need to create a new EIP, see [Apply for an EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).


1. On the instance list page, select the target instance and click **Add EIP** to go to the protection resource list page.

2. Click **Add EIP**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c6e937ca9ebf479493b1300e91980069) </span>

3. Select the EIPs required by your business and add them to the protection list.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If no EIPs are available, please go to the <a href="https://console.byteplus.com/eip">EIP console</a> to purchase one.   </div>
   

For detailed instructions on adding an EIP, see [Add an EIP to your instance](https://docs.byteplus.com/docs/byteplus-ddos-protection/Add_an_EIP).

<span id="eac061e8"></span>
## Step 3: Associate an EIP address with a protection rule group

Protection rules for Cloud DDoS Protection take effect through rule groups. Therefore, you must associate a protected resource with a rule group to apply the rules to that resource. For descriptions of the different rule groups, refer to [Overview of protection policies](https://docs.byteplus.com/docs/byteplus-ddos-protection/Overview_of_protection_policies).


* **Default rule group**: This group contains general protection rules to mitigate DDoS attacks on the network and transport layers. The BytePlus DDoS protection engine develops these rules from extensive real\-world attack data. The default rule group automatically applies to any protected EIPs not assigned to a custom rule group, so you do not need to manually configure an IP range.

* **Custom rule groups**: You can create and configure rule groups based on your specific business needs and security requirements. You can view and modify the rules and their associated IP ranges at any time. For information on how to create a custom rule group, refer to [Create a custom rule group](https://docs.byteplus.com/docs/byteplus-ddos-protection/Create_a_custom_rule_group).


<span id="558ea42f"></span>
## Step 4: View protection details

After completing the above steps, you can start using the BytePlus Cloud DDoS Protection service. You can view various protection data in real time on the traffic report page, including traffic trend reports and attack event details. To learn more about protection reports, refer to [View details of DDoS attack protection](https://docs.byteplus.com/docs/byteplus-ddos-protection/View_dashboard_details).
