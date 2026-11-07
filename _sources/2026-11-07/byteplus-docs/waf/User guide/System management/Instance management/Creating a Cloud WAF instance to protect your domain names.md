---
title: "Creating a Cloud WAF instance to protect your domain names"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Creating_a_Cloud_WAF_instance"
---

If your website's domain is not hosted on BytePlus Cloud or hasn't yet utilized BytePlus CDN services, you can create a Cloud WAF instance to safeguard your domain. Once the instance is created, you should integrate the domain you wish to protect and configure the necessary rules to ensure effective security. This document outlines the steps and considerations to create a Cloud WAF instance.

<span id="b8d6fcec"></span>
## Prerequisites


* You have already registered a Byte Plus account. For related operations, see [Signing up and verifying your BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* Your account is not overdue.


<span id="8f3eaeda"></span>
## Precautions


* Each account is limited to creating one Cloud WAF instance. After the instance expires, you can purchase a new one.

* An expired instance will retain only its forwarding capabilities and will no longer offer WAF protection. Domains integrated through WAF CNAME will not experience any changes to their CNAME records. Please ensure you update your domain's DNS settings in advance to avoid any impact on your business operations.


<span id="6cd1923c"></span>
## Creating an instance for the first time


1. Log in to the [BytePlus Web Application Firewall Console](https://console.byteplus.com/waf).

2. In the top menu bar, select the region for the Cloud WAF instance, Asia Pacific (Johor).

3. On the welcome page, click **Buy WAF**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have created an instance already, go to <strong>System management \> Instance management</strong>, and click <strong>Create instance</strong> to add a new one.   </div>
   

4. Configure the relevant parameters as explained below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a790d5ad5f964a69aa46df156a25386a~tplv-goo7wpa0wc-image.image) </span>

   
   |**Section** |**Configuration** |**Description** |
   |---|---|---|
   |Instance information |Instance name |Optional configuration. If it is left empty, an instance name will be automatically generated.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Start with a letter or digit.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The name can have letters, digits, periods (.), underscores (_), and hyphens (\-).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The length must be between 1 and 128 characters.</div><br> |
   ||Instance type |Cloud WAF is supported currently. |
   ||Project |Add the instance to the project which the current account can access. Project management is a resource management method provided by BytePlus, which is conducive to keeping resources independent and maintaining data security.<br><br><br>* The instance will be associated with the project which the account can access by default, and cannot be modified.<br><br>* The primary account can view all projects. After switching the project at the top of the console to **All resources**, you can adjust the project settings. |
   ||Tag |Select a tag or create a new tag for your instance to distinguish resources.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Up to 20 tags can be added.</div><br> |
   |Package specification |Region |The region where WAF instance is located. Asia Pacific (Johor) is supported currently. |
   ||Payment model |* Annual or monthly payment is supported.<br><br>* Free trial: The account should have a free trial quota (you can apply for a voucher). You can choose Contact sales in the top right corner of the BytePlus official webpage to submit your free trial request. |
   ||Package specification |Cloud WAF instances support four editions: Basic edition, Advanced edition, Enterprise edition, and Flagship edition. |
   |Advanced configuration |Log service |Upon activating the log service, an associated IAM role is automatically created. This role provides the WAF with the necessary permissions to access other cloud resources. |
   ||Log capacity |The available range for log capacity is 1 to 500 TiB. |
   ||Domain extension pack |You can purchase domain extension packs to increase the number of domain names you can protect. Each pack allows you to add a quota for 10 domain names under a single top\-level domain. Up to 1000 extension packs can be purchased. |
   ||QPS extension pack |You can purchase QPS extension packs to enhance the QPS capacity that your WAF can manage. Each pack adds an extra quota of 1000 QPS, and you can buy up to 20 extension packs. |
   ||Duration |Validity period of the instance.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Instances will be reclaimed 15 days after the expiration date. Please adjust your domain name resolution settings beforehand to ensure your operations continue smoothly.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">An expired instance will retain only its forwarding capabilities and will no longer offer WAF protection. Domains integrated through WAF CNAME will not experience any changes to their CNAME records.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When you purchase an instance, it is set to automatically renew upon expiration. This means that if your account balance is sufficient, the instance will be automatically renewed for one month before it expires. You can manually uncheck or modify your settings anytime after activation by going to <a href="https://console.byteplus.com/finance/renew">Billing center \> Renewal management</a>.</div><br> |
   

5. After confirming the configured parameters, please read and agree to the related service agreements.

6. Click **Buy now** to confirm your order.

7. Ensure that the order information is accurate, and proceed with the payment.

   Once you've purchased the instance, it becomes effective immediately. Please promptly integrate your domain that requires protection with the WAF instance and configure the necessary security policies to ensure it is protected.


<span id="215e5c36"></span>
## Viewing the instance details

You can access the details of your purchased instances on the **Instance management** page, where you can check their specifications and validity periods.


1. Log in to the [BytePlus Web Application Firewall Console](https://console.byteplus.com/waf).

2. In the top menu bar, select the region for the Cloud WAF instance, Asia Pacific (Johor).

3. In the left navigation, select **System management \> Instance management**.

4. View the instance's details, including type, region, specifications, and expiration time.

5. (Optional) You can perform the following operations in the instance list.

   * ①: Edit the instance name.

   * ②: Change the protection mode of the instance.

      * Enable protection: Enable the protection policy to detect requests made to the domain names under the protection of the instance.

      * Pause protection: The requests will be forwarded to the origin servers by WAF without any detection. The configured protection policies in this mode do not take effect.

   * ③: Enable/Disable the auto\-renewal function.

   * ④: Upgrade the instance. Within the validity period of the instance, you can upgrade the package to a higher specification to meet business needs.

   * ⑤: Manual renewal. Before the instance is recycled, you can manually renew the current specification package to extend the service usage time and avoid the unavailability of protection functions due to service expiration.

   * ⑥: View the rule details of the instance.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f4590a37064549c8ad80ef53b531d694~tplv-goo7wpa0wc-image.image) </span>
