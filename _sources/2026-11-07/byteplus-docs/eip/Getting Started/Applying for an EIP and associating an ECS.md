---
title: "Applying for an EIP and associating an ECS"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP-and-associating-an-ECS-instance"
---

This section describes how to associate an Elastic IP Address (EIP) with an Elastic Compute Service (ECS) instance to help you quickly master the use of EIPs.

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations


* Complete the BytePlus account registration and real\-name authentication.

* Ensure the total of your available balance and vouchers applicable to the EIP is no less than USD 100.00, with the available balance not less than 0. For details, see [Recharge guide](https://docs.byteplus.com/en/docs/byteplus-platform/billing_account).

* Create an ECS instance without any EIP associated. For details, see [Purchasing an instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. [Apply for an EIP](https://docs.byteplus.com/en/docs/48/10122#.5q2l6aqk5LiA77ya55Sz6K-35YWs572RSVA=): Apply for an EIP.

2. [Associate the EIP with an ECS](https://docs.byteplus.com/en/docs/48/10122#.5q2l6aqk5LqM77ya5LqR5pyN5Yqh5Zmo57uR5a6a5YWs572RSVA=): Associate the newly applied EIP with the prepared ECS instance.

3. [Verify](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP-and-associating-an-ECS-instance#.5q2l6aqk5LiJ77ya6aqM6K-B): Log in to the prepared ECS instance and test its connectivity with the internet.


<span id=".5q2l6aqk5LiA77ya55Sz6K-35YWs572RSVA="></span>
### Step 1: Apply for an EIP


1. Log in to the [EIP console](https://console.byteplus.com/eip/eips).

2. In the top menu bar, select region and project. This example selects **China (Beijing)**  and **default**.

3. Click **Apply for EIP**.

4. Configure the relevant parameters according to the table below.

   
   |Parameter |Notes |Sample value |
   |---|---|---|
   |Billing method |Select a billing method for the EIP. Pay\-as\-you\-go and Subscription are supported. |Pay\-as\-you\-go |
   |Region |Select the region for the EIP.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The region of EIP must be the same as that of the prepared ECS.</div><br> |China (Beijing) |
   |Name |Type in a name for the EIP. |eip\-1 |
   |ISP |Select the ISP type for the EIP. BGP (Multi\-ISP) is recommended. |BGP (Multi\-ISP) |
   |Metering method |When the billing method is **Pay\-as\-you\-go**, two metering methods are supported: Pay\-by\-bandwidth and Pay\-by\-data\-transfer. Select a metering method for the EIP based on the interface prompts and your business requirements. |Pay\-by\-data\-transfer |
   |Bandwidth Package |When the billing method is pay\-as\-you\-go, check Add EIP to Bandwidth Package as needed.<br><br>After being added to the Bandwidth Package, the EIP invalidates the billing method’s traffic fee or bandwidth fee and bandwidth limit, and shares the bandwidth of the Bandwidth Package. |No |
   |IP Address Pool |Only Pay\-as\-you\-go EIPs support enabling IP address pools. When enabled, EIP gets the IP address from the specified IP address pool, and no longer incurs IP config fee.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This feature is currently in Beta. For trial requests, please contact your account manager.</div><br> |Disable |
   |Maximum bandwidth |Set the maximum bandwidth for the EIP. |1 Mbps |
   |Quantity |Type the number of EIPs applied. |1 |
   |Affiliated project |Select the project to which the EIP belongs. |default |
   |Tags |Add one or more custom tags to the EIP as needed. |No tags added |
   

5. Follow the console guidance to review and accept the legal terms.

6. Click **Agree and buy** to complete the action.


<span id=".5q2l6aqk5LqM77ya5LqR5pyN5Yqh5Zmo57uR5a6a5YWs572RSVA="></span>
### Step 2: Associate the EIP with an ECS


1. In the EIP list, click **Associate** to the right of the target EIP to open the associate EIP page.

2. Select the prepared ECS instance and click **Associate** to complete the action.


<span id=".5q2l6aqk5LiJ77ya6aqM6K-B"></span>
### Step 3: Verify


1. Log in to the prepared ECS instance.

2. Run the `ping 114.114.114.114` command.

3. A successful ping indicates that the ECS instance is connected to the Internet.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If ping to 114.114.114.114 fails, see <a href="https://docs.byteplus.com/en/docs/eip/EIP-FAQs#.5Li65LuA5LmI5LqR5pyN5Yqh5Zmo5a6e5L6L57uR5a6a5YWs572RSVDku43nhLbml6Dms5Xov57mjqXkupLogZTnvZHvvJ8=">Why can't an ECS instance still connect to Internet after associating an EIP</a>.   </div>
