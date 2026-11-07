---
title: "Create and use the Shared Traffic Package"
product: "TrafficPackage"
product_code: "Trafficpackage"
source: "https://docs.byteplus.com/en/docs/Trafficpackage/Create_and_use_the_Shared_Traffic_Package"
---

This article introduces how to quickly create a Shared Traffic Package. Once the Shared Traffic Package is successfully created, it will be immediately used for the deduction of Internet traffic fees in the current Region with a traffic\-based billing mode, without any additional actions.

<span id="preparation"></span>
## Preparation

Before getting started, make the following preparations:


* Complete Account registration and real\-name authentication for VolcanoEngine.

* Apply for an Elastic IP (EIP) with a default protection Type and traffic\-based billing. For more information, refer to [Applying for EIPs](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).


<span id="procedure"></span>
## Procedure


1. Log in to the [Shared Traffic Package console](https://console.byteplus.com/eip/trafficPackages).

2. Click the **Create Shared Traffic Package** button.

3. Configure the basic information of the Shared Traffic Package.



|**Parameter** |**Description** |Example |
|---|---|---|
|Region |Select the Region where the Elastic IP (EIP) is located. After creation, changing the Region is not supported. |China 2 (Beijing) |
|ISP |Select BGP (Multi\-ISP) to remain consistent with the ISP of the Elastic IP (EIP). |BGP (multi\-line) |
|Validity period |Select the activation period for the Shared Traffic Package. After successful purchase, the Shared Traffic Package will take effect immediately. |1 month |
|Type |Select the traffic specification for the Shared Traffic Package. |10GB |
|Quantity |The number of Shared Traffic Packages purchased. In each Region, up to 20 non\-expired Shared Traffic Packages can be purchased, and raising the quota is not supported. |1 Gateway |



4. Please follow the console instructions to review and confirm the Legal, and click **Buy now**.

5. Click the **Next step** button, select the payment method, then click the **Pay** button to proceed with the payment according to the selected method.

> After the payment information is submitted, you must complete the payment within a specified period of time. Otherwise, orders will be canceled.


**Once the Shared Traffic Package is created, it will take effect immediately, and the Elastic IP (EIP) instances charged by traffic in the current Region will first use the traffic in the Shared Traffic Package.**
