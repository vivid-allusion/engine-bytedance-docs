---
title: "Creating a Bandwidth Package"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/Creating-a-Bandwidth-Package"
---

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have completed the BytePlus account registration and real\-name authentication.

* Ensure that the sum of both your [available balance](https://docs.byteplus.com/en/docs/6269/100429) and the coupons available for Bandwidth Package is not less than USD 100.00, and the available balance must be no less than 0. For procedure, see [Recharge guide](https://docs.byteplus.com/en/docs/6269/100434).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Bandwidth Package console](https://console.byteplus.com/eip/cbwps).

2. In the top menu bar, select a target region and project.

3. Click **Create Bandwidth Package**.

4. Configure the basic information for the Bandwidth Package instance.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Billing method |Select a billing method for the Bandwidth Package. Support Pay\-as\-you\-go and [Subscription](https://docs.byteplus.com/en/docs/bandwidthpackage/Subscription). |Pay\-as\-you\-go |
   |Region |Select the region of the Bandwidth Package. The Bandwidth Package instance only supports adding elastic IP addresses (EIPs) or IPv6 Internet bandwidth in the same region, and does not support changing region after creation. |China (Beijing) |
   |Name |Type in a name for the Bandwidth Package. |BandwidthPackage\-01 |
   |Protocol type |Select a protocol type for the Bandwidth Package.<br><br><br>* IPv4: The Bandwidth Package with IPv4 protocol only supports adding IPv4 EIPs.<br><br>* Dual\-stack: The Bandwidth Package with dual\-stack protocol supports adding both IPv4 EIPs and IPv6 Internet bandwidth. |IPv4 |
   

5. Configure the ISP and bandwidth for the Bandwidth Package instance.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |ISP |Specify an ISP for the Bandwidth Package. The EIP and the IPv6 Internet bandwidth with the same ISP can be added to the Bandwidth Package.<br><br>BGP (multi\-ISP) is recommended. If you need another ISP, contact your account manager. |BGP (multi\-line) |
   |Metering method |When Billing method is set to **Pay\-as\-you\-go**, select a metering method for the Bandwidth Package. Support [Pay-by-bandwidth](https://docs.byteplus.com/en/docs/bandwidthpackage/Pay-by-bandwidth), [Pay-by-main-traffic](https://docs.byteplus.com/en/docs/bandwidthpackage/Pay-by-domain-traffic), and [Pay-by-95th-peak](https://docs.byteplus.com/en/docs/bandwidthpackage/Pay-by-traditional-95th-percentile).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-platform/SplitBills">Split bills</a> are available for Bandwidth Packages metered by Pay\-by\-main\-traffic or Pay\-by\-95th\-peak. With split bills, you can view the usage proportion and cost allocation for each EIP in the Bandwidth Package.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Pay\-by\-95th\-peak is in the beta stage. To request a trial, please contact your account manager.</div><br> |Pay\-by\-bandwidth |
   |Maximum bandwidth |Set the maximum bandwidth for the Bandwidth Package, measured in Mbps. For the bandwidth range, see [Bandwidth limits](https://docs.byteplus.com/en/docs/bandwidthpackage/Limits#.5bim5a696ZmQ5Yi2). |100 Mbps |
   

6. Configure more information and the advanced option for the Bandwidth Package instance.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Purchase time |When Billing method is set to **Subscription**, set a purchase duration for the Bandwidth Package. |1 month |
   |Automatic renewal |When the billing method is set to **Subscription**, check Automatic renewal as needed.<br><br>If Automatic renewal is enabled, the renewal cycle is one month for both monthly and yearly Subscription Bandwidth Packages. The number of renewals defaults to unlimited. You can manually disable automatic renewal or go to the Billing center to edit the auto\-renewal times. For more information, see [Automatic renewal](https://docs.byteplus.com/en/docs/byteplus-platform/docs-auto-renewal-rules). |Enable |
   |Affiliated project |Select a project to which the Bandwidth Package belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/bandwidthpackage/Managing-projects).<br><br><br>* If you select All Resources from the top menu bar before accessing the creation page, you can select an existing project from the drop\-down list.<br><br>* If you select a target project from the top menu bar before accessing the creation page, you can only select the target project.<br><br><br>If you want to migrate the Bandwidth Package to another project after creation, see [Transferring resources in project](https://docs.byteplus.com/en/docs/6649/94337). |default |
   |Tags |Add one or more tags for the Bandwidth Package instance.<br><br>A tag consists of the tag key (Key) and the tag value (Value), and is used to tag Bandwidth Package instances for classification and search. For more information, see [Tag management](https://docs.byteplus.com/en/docs/bandwidthpackage/Managing-tags).<br><br><br>* Click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1cb8ac9d0ff7f7f4b0d373d01a0b23fb.png) </span> icon to add multiple tags. A single Shared Bandwidth Package can have up to 20 tags.<br><br>* The Keys of multiple tags for the same Bandwidth Package must be unique. Each Key has only one Value.<br><br>* The Key and the Value are case\-sensitive. For example, the Key=tag and the Key=Tag are two different Keys. |bwp:v1 |
   

7. Click **Confirm order**.

8. Follow the console guidance to review and accept the legal terms.

   * Pay\-as\-you\-go: Click **Buy now** to complete the action.

   * Subscription: Click **Agree and buy**, click **Next**, select a payment method, and then click **Pay** to complete the payment by the selected method.

      > After submitting the payment information, complete the payment within the specified time. Otherwise, the order will be canceled.      
      

<span id=".55u45YWz5paH5qGj"></span>
## What to do next

[Add EIP or IPv6 Internet bandwidth](https://docs.byteplus.com/en/docs/bandwidthpackage/Managing_resources_in_a_Bandwidth_Package#9HNP4wLa): After the Bandwidth Package is created, you can add an EIP or IPv6 Internet bandwidth to the Bandwidth Package instance to share the same bandwidth resources. This helps reduce your Internet access costs.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateBandwidthPackage](https://docs.byteplus.com/en/docs/bandwidthpackage/CreateBandwidthPackage): Create a Bandwidth Package.
