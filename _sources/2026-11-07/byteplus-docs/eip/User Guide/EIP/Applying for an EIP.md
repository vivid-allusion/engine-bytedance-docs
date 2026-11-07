---
title: "Applying for an EIP"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP"
---

<span id=".5pON5L2c6K-05piO"></span>
## Instructions

This topic describes how to create an Elastic IP Address (EIP) instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Before you begin


* You have registered a BytePlus account and completed real\-name authentication.

* Ensure that the total value of both the available balance and coupons available for EIP in your account is not less than USD 100.00, and the available balance must be no less than 0. For specific actions, see the [Recharge guide](https://docs.byteplus.com/en/docs/byteplus-platform/billing_account).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [EIP console](https://console.byteplus.com/eip/eips).

2. In the top menu bar, select the target region and project.

3. Click **Apply for EIP**.

4. Configure the basic information for the EIP based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Billing method |Select a billing method for the EIP. Supports [Pay-as-you-go](https://docs.byteplus.com/en/docs/eip/Pay-as-you-go) and [Subscription](https://docs.byteplus.com/en/docs/eip/Subscription). |Pay\-as\-you\-go |
   |Region |Select a region for the EIP. You cannot change the region after applying. Confirm that the EIP and the cloud resource to be associated are in the same region. |China (Beijing) |
   |Name |Type the name of the EIP. |eip\-1 |
   

5. Configure ISP specification for the EIP.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |ISP |Select an ISP for the EIP. BGP (Multi\-ISP) is recommended. If you need another ISP, contact your account manager.  |BGP (Multi\-ISP) |
   |Metering method |When the billing method is Pay\-as\-you\-go, select a metering method for the EIP. Pay\-by\-bandwidth and Pay\-by\-data\-transfer are supported. |Pay\-by\-bandwidth |
   |Maximum bandwidth |Set the maximum bandwidth for the EIP, measured in Mbps. After application, you can adjust the maximum bandwidth as needed at any time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The EIP bandwidth applies separately to uplink and downlink bandwidth. For example, if the bandwidth limit is 10 Mbps, the EIP's upstream and downstream bandwidths are both 10 Mbps. For the specific range, see <a href="https://docs.byteplus.com/en/docs/eip/Limits#.5oCn6IO96ZmQ5Yi2">Performance limits</a>.</div><br> |1 |
   |Bandwidth Package |When the billing method is pay\-as\-you\-go, check Add EIP to Bandwidth Package as needed.<br><br><br>* If left unchecked, you can add to a Bandwidth Package as needed later.<br><br>* If checked, you can select an IPv4 Bandwidth Package within the current region that has the same security protection level as your EIP.<br><br>   After being added to the Bandwidth Package, the traffic fee, bandwidth fee, and bandwidth cap specified in the billing method above become invalid.The EIP shares the bandwidth of the Bandwidth Package.<br><br><br>If you remove the EIP from the Bandwidth Package later, the original billing method and bandwidth cap will be restored.<br><br> |No |
   |IP Address Pool |Select a project and choose an IP Address Pool.<br><br>Only Pay\-as\-you\-go EIPs support enabling IP address pools. When enabled, EIPs get their IP addresses from the specified IP address pool and no longer incur IP config fees. For more information, see [IP Address Pool overview](https://docs.byteplus.com/en/docs/eip/IP_address_pool_overview).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The IP address pool is in the beta stage. To request a trial, please contact your account manager.</div><br> |Disable |
   

6. Provide more information and configure advanced options for the EIP.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Quantity |Specify the number of EIPs that you want to apply for. |1 |
   |Purchase time |When the billing method is **Subscription**, set the duration for purchasing an EIP. |1 calendar month |
   |Automatic renewal |When the billing method is **Subscription**, choose whether to enable automatic renewal.<br><br>If automatic renewal is on, the default renewal cycle is one month. The number of renewals is unlimited by default. You can turn off automatic renewal manually or go to the **Billing center** to change the renewal count. For details, see [Automatic renewal](https://docs.byteplus.com/en/docs/byteplus-platform/docs-auto-renewal-rules). |Unchecked |
   |Affiliated project |Select the project to which the EIP belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/eip/Managing-projects).<br><br><br>* If you select All Resources in the top menu bar before going to the application page, you can select an existing project from the drop\-down list.<br><br>* If you select a target project in the top menu bar before accessing the application page, you can only select that project. |default |
   |Tag |Add one or more user tags to the EIP as needed.<br><br>A tag consists of a tag key (Key) and a tag value (Value). It can be used to classify and search for EIPs. For more information, see [Tag management](https://docs.byteplus.com/en/docs/eip/Managing-tags).<br><br><br>* Click the<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_745f4ea6f3f698cebd9adc96c9240260.png) </span> icon to add multiple tags, and a single Elastic IP (EIP) can have up to 20 tags.<br><br>* The Keys of multiple tags for the same EIP must be unique, and each Key can have only one Value.<br><br>* The Key and the Value are case\-sensitive. For example, Key=tag and Key=Tag are two different Keys. |eip1, v1 |
   

7. Follow the console guidance to review and confirm the Legal.

   * Pay\-as\-you\-go: click **Agree and buy** to complete the operation.

   * Subscription: Click **Agree and buy**, click **Next step**, select a payment method, then click **Pay** to complete payment according to the chosen method.

      > After submitting the payment information, complete the payment within the specified time. Otherwise, the order will be canceled.      
      

<span id=".55u45YWz5paH5qGj"></span>
## What to do next


* [Associate a cloud resource](https://docs.byteplus.com/en/docs/eip/Associating-Cloud-Resources-with-an-EIP): After successfully applying for an EIP, you can associate it with Elastic Compute Service, Classic Load Balancer, Internet NAT Gateway, secondary network interface, High\-Availability Virtual IP Address, and other cloud resources to meet different internet scenarios.

* [Add to a Bandwidth Package](https://docs.byteplus.com/en/docs/eip/Adding-an-EIP-to-a-Bandwidth-Package): Add multiple EIPs in the same region to a Bandwidth Package instance to share bandwidth and help reduce internet bandwidth costs.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[AllocateEipAddress](https://docs.byteplus.com/en/docs/eip/AllocateEipAddress): Apply for an EIP.
