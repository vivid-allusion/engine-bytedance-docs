---
title: "Creating a WAF instance to protect your domain names on CDN"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/docs-system-management"
---

If your domain name has already been accelerated by BytePlus CDN service, you can add your domains to WAF for protection. By integrating BytePlus WAF and CDN, you can improve the security of your website while enhancing its performance. This document describes the operations and precautions for creating a WAF instance to protect CDN domains.

<span id="17ddcf2e"></span>
## Prerequisites


* You have registered a BytePlus account. For related operations, please refer to [Signing up and verifying your BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* Your account is not overdue.


<span id="96ffd561"></span>
## Precautions


* Currently, only one WAF instance can be created per account. After the instance expires, you can purchase a new instance.

* Expired instances only retain forwarding capabilities and no longer offer WAF protection.


<span id="c7a434c4"></span>
## Creating an instance for the first time


1. Log in to the [BytePlus Web Application Firewall Console](https://console.byteplus.com/waf).

2. In the top menu bar, select **Edge(CDN)** , the region where your WAF instance is located.

3. On the welcome page, click **Buy WAF**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have created an instance already, go to <strong>System Management\>Instance Management</strong>, and click <strong>Create instance</strong> to add a new one.   </div>
   

4. Configure the relevant parameters as described below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/45755c4c20c84d5b810ee848d6959ecb~tplv-goo7wpa0wc-image.image) </span>

   
   |**Section** |**Configuration** |**Description** |
   |---|---|---|
   |Instance information |Instance name |Optional parameter. If it is left empty, an instance name will be automatically generated.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Start with a letter or digit.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The name can have letters, digits, periods (.), underscores (_), and hyphens (\-).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The length must be between 1 and 128 characters.</div><br> |
   ||Project |Add the instance to the project which the current account can access. Project management is a resource management method provided by BytePlus, which is conducive to keeping resources independent and maintaining data security.<br><br><br>* The instance will be associated with the project which the account can access by default, and cannot be modified.<br><br>* The primary account can view all projects. After switching the project at the top of the console to **All resources**, you can adjust the project settings. |
   ||Tag |Select a tag or create a new tag for your instance to distinguish resources.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Up to 20 tags can be added.</div><br> |
   |Package specifications |Billing model |Pay\-as\-you\-go |
   ||Specifications |The standard package is now supported. |
   |Advanced configuration |Log service |Upon activating the log service, an associated IAM role is automatically created. This role provides the WAF with the necessary permissions to access other cloud resources. |
   

5. After confirming the configured parameters, please read and agree to the relevant service agreements.

6. Click **Buy Now** to confirm your order.

7. Ensure that the order information is accurate, and proceed with the payment.

   Once you've purchased the instance, it becomes effective immediately. Please promptly integrate your domain that requires protection with the WAF instance and configure the necessary security policies to ensure it is protected.


<span id="ad3f4c7d"></span>
## Viewing the instance details

You can access the details of your purchased instances on the **Instance management** page, where you can check their specifications and validity periods.


1. Log in to the [BytePlus Web Application Firewall Console](https://console.byteplus.com/waf).

2. In the top menu bar, select Edge(CDN), the region where your Cloud WAF instance resides.

3. On the left navigation pane, choose **System Management** \> **Instance Management**.

4. View information such as instance name, ID, and expiration time.

5. (Optional) You can perform the following operations in the instance list:

   * ①: Modify the instance name.

   * ②: Click to view the resources of the project to which the instance belongs, as well as other resources under the project.

   * ③: Change the protection mode of the instance.

      * Enable protection: Enable the protection policy to detect requests made to the domain names under the protection of the instance.

      * Pause protection: The requests will be forwarded to the origin servers by WAF without any detection. The configured protection policies in this mode do not take effect.

   * ④: Unsubscribe the instance.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41d0e5761b4542b7a5b3b2ddf3a7750e~tplv-goo7wpa0wc-image.image) </span>


&nbsp;
