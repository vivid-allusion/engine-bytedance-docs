---
title: "Creating a bandwidth package"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/TR-bandwidth-packages-01"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

Transit Router (TR) bandwidth packages provide bandwidth resources for cross\-region communication scenarios. Create a bandwidth package when you need to achieve cross\-region connectivity through a TR.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">TR bandwidth packages are divided into cross\-border bandwidth packages and non\-cross\-border bandwidth packages. A cross\-border bandwidth package means one of interconnected regions is in <strong>China Mainland</strong> and the other is outside <strong>China Mainland</strong>. For example: China Mainland \- Asia Pacific.</div>


<span id=".5pON5L2c6K-05piO"></span>
## Instructions


* A single account can create up to 10 bandwidth packages by default. If this quota is insufficient, you can request an increase through the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=Auto_Scaling), up to an absolute upper limit of 100 packages.

* The default maximum bandwidth for a bandwidth package is 10,000 Mbps. If the default quota is insufficient for your needs, contact your account manager.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The BytePlus account has completed enterprise authentication. If your account is a personal verified account, see [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Bandwidth Package console](https://console.byteplus.com/trbandwidthpkg/trbp).

2. In the top navigation bar, select the target project.

3. Click **Create bandwidth package** and configure the bandwidth package parameters based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |Billing method |The billing method for the bandwidth package to be created.<br><br><br>* Subscription: A prepaid metering method that charges based on your purchased duration. |Subscription |
   |Name |Type the name for the bandwidth package to be created. |trbp\-01 |
   |**Bandwidth configuration** |||
   |Interoperability area |The bandwidth package requires interoperatable local and peer areas. For TR supported regions, see Areas and Regions. |Chinese mainland \- Chinese mainland |
   |Line operator |Select the line operator that provides cross\-border bandwidth for you. Supports China Unicom and China Telecom.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required when one end of the interoperability area is a China Mainland region and the other is a region outside China Mainland.</div><br> |China Unicom |
   |Bandwidth |Set the bandwidth value for the bandwidth package to be created. Valid range: 2 to 10,000. Unit: Mbps.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The maximum bandwidth of your cross\-border bandwidth package is determined by the bandwidth purchased from the line operator.</div><br> |100 Mbps |
   |Purchase duration |Select the purchase duration for the bandwidth package.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The purchase duration of the cross\-border bandwidth package must not exceed the cross\-border service duration you contracted with the line operator.</div><br> |1 month |
   |Automatic renewal |Specify whether to enable automatic renewal. By default, it is disabled. When automatic renewal is enabled, the system will automatically renew the instance upon expiration if your account has sufficient balance. The default renewal cycle is 1 month with unlimited renewals. |Not selected |
   |**More information** |||
   |Affiliated project |Select the project to which the bandwidth package belongs. After the project is selected, the created bandwidth package can only be used by users with permissions for that project. Bandwidth packages cannot be shared across different projects. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Projects)<br><br><br>* If you select **All Resources** in the top menu bar before entering the creation page, the bandwidth package belongs to the default project by default. You can reselect a project as needed.<br><br>* If you select a specific project in the top menu bar before entering the creation page, the bandwidth package belongs to that project by default. To associate it with another project, change the project to **All Resources** or the target project in the top menu bar. |default |
   |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Tags)<br><br>Click **Add tag**, type the tag key and tag value to add tags to the bandwidth package. |* Tag key: trbp\-k1<br><br>* Tag value: trbp\-v1 |
   

4. In the right\-side Configuration details section, follow the console guidance to review and accept the legal terms.

5. Click **Submit order** to confirm the order amount.

6. Click **Next** and follow the guidance to complete the order payment.

7. Click **Go to console** to view the created bandwidth package.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

After creating a TR bandwidth package, you also need to allocate cross\-region bandwidth for the inter\-region attachment to enable cross\-region communication. For details, see [Creating an inter-region attachment](https://docs.byteplus.com/en/docs/transitrouter/Inter-region-peering-attachments-01) or [Add to a TR bandwidth package](https://docs.byteplus.com/en/docs/transitrouter/Inter-region-peering-attachments-02#.5Yqg5YWl5bim5a695YyF).

<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[CreateTransitRouterBandwidthPackage](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterBandwidthPackage): Create a TR bandwidth package.
