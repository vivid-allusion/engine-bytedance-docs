---
title: "Creating a Bandwidth Package and adding an EIP"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/Creating-a-Bandwidth-Package-and-adding-an-EIP"
---

This topic describes how to create a Bandwidth Package, add an Elastic IP Address (EIP) to it, and verify the maximum bandwidth for that EIP, helping you quickly master the use of Bandwidth Package.

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations

Before you begin, complete the following preparations:


* You have registered a BytePlus account and completed real\-name authentication.

* Ensure that the sum of your [available balance](https://docs.byteplus.com/en/docs/6269/100429) and coupons applicable for Bandwidth Package is not less than USD 100.00. Also, ensure your available balance is no less than 0. For specific procedure, see [Recharge guide](https://docs.byteplus.com/en/docs/6269/100434).



&nbsp;

* Apply for an EIP with default protection. For specific procedure, see [Applying for an EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. [Create a Bandwidth Package](https://docs.byteplus.com/en/docs/50/14325#.5q2l6aqk5LiA77ya5Yib5bu65YWx5Lqr5bim5a695YyF): Create a Bandwidth Package instance.

2. [Add an EIP](https://docs.byteplus.com/en/docs/50/14325#.5q2l6aqk5LqM77ya5re75Yqg5YWs572RSVA=): Add the prepared EIP to the new Bandwidth Package instance.

3. [Verification](https://docs.byteplus.com/en/docs/50/14325#.5q2l6aqk5LiJ77ya6aqM6K-B): Check whether the prepared EIP is added to the Bandwidth Package on the Elastic IP console.


<span id=".5q2l6aqk5LiA77ya5Yib5bu65YWx5Lqr5bim5a695YyF"></span>
### Step 1: Create a Bandwidth Package


1. Log in to [the Bandwidth Package console](https://console.byteplus.com/eip/cbwps).

2. In the top menu bar, select region and project. In this example, they are **China (Beijing)**  and **default**.

3. Click **Create Bandwidth Package**.

4. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Billing method |Select a billing method for the Bandwidth Package. |Pay\-as\-you\-go |
   |Region |Select a region for Bandwidth Package.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Bandwidth Package instance only supports adding EIPs in the same region, and does not support changing region after purchase. Proceed with caution.</div><br> |China (Beijing) |
   |Name |Type in a name for the Bandwidth Package. |BandwidthPackage\-01 |
   |Protocol type |Select a protocol type for the Bandwidth Package. |IPv4 |
   |ISP |Select an ISP for Bandwidth Package. |BGP (multi\-line) |
   |Metering method |Select a metering method for Bandwidth Package. |Pay\-by\-bandwidth |
   |Maximum bandwidth |Set the maximum bandwidth for Bandwidth Package. |100 Mbps |
   |Affiliated project |Select a project to which the Bandwidth Package belongs. |default |
   |Tags |Add one or more custom tags for Bandwidth Package as needed. |No tags added |
   

5. Click **Confirm order**.

6. Follow the console guidance to review and accept the legal terms, and click **Buy now** to complete the action.


<span id=".5q2l6aqk5LqM77ya5re75Yqg5YWs572RSVA="></span>
### Step 2: Add an EIP


1. In the Bandwidth Package list, click **Manage EIP** to the right of the target Bandwidth Package instance.

2. Click **Add EIP**.

3. Click the **Select from existing EIPs** tab and select the prepared EIP.

4. Click **Add** to complete the action.


<span id=".5q2l6aqk5LiJ77ya6aqM6K-B"></span>
### Step 3: Verification


1. Log in to [the EIP console](https://console.byteplus.com/eip/eips).

2. In the top menu bar, select the region and project of your target EIP.

3. In the EIP list, view the name and maximum bandwidth of Bandwidth Package to which the EIP is added.
