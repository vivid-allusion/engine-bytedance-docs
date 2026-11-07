---
title: "Pay-by-CU"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/VPC-NAT-gateway-billing"
---

VPC NAT Gateways use the Pay\-by\-CU billing method. You are charged based on the NAT Gateways and resources that you use.

Pay\-by\-CU is a billing mode based on the connection usage, and lets you use resources first and pay for them afterwards.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">VPC NAT Gateway is in the beta stage. If you want to use it, please contact the customer manager.</div>


<span id="prerequisites"></span>
## Prerequisites


* Verification is completed for your BytePlus account.For more information, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* Make sure that the balance is greater than or equal to 0.


<span id="performance-caps"></span>
## Performance caps

The following table describes the performance caps for the Pay\-by\-CU VPC NAT gateway:


|Performance Metric |Maximum value |
|---|---|
|New connections per second for a single VPC NAT gateway |100,000 |
|Max connections for a single VPC NAT gateway |2,000,000 |
|The maximum forwarding bandwidth of a VPC NAT gateway |5 Gbps |


<span id="billing-formulas"></span>
## Billing formulas

**Fee of a Pay\-by\-CU VPC NAT Gateway = Instance fee + Concurrent Unit (CU) fee.** 


* **Instance fee = Instance unit price (USD/hour per instance) × Usage duration (hours).** 

   * The instance fee is the cost for using VPC NAT gateway resources.

   * The instance unit price is USD 0.036/hour per instance.

   * The usage duration is the actual duration of using resources, accurate to the second.

* **CU fee per hour = CU unit price (USD/pcs) × Number of CUs consumed by the instance every hour (pcs)** 

   * The CU fee is charged based on the number of concurrent units used.

   * Number of CUs per hour = **Max**. For more information, refer to [CU counting description](https://docs.byteplus.com/en/docs/51/10095#CU-counting-description).

   * The following table describes the CU unit price:

      
      |Region |CU unit price (USD/pcs) |
      |---|---|
      |Asia Pacific (Johor) |0.036 |
      


<span id="cu-counting-description"></span>
## CU counting description


|Performance Metric |Metric Description |CU Coefficient |Measurement Unit |CU counting description |
|---|---|---|---|---|
|Maximum number of new connections per second |The number of new connections per second. |1,000 connections/CU |Second |During the billing cycle, calculate the number of new connections per second and divide the maximum value by the CU coefficient to get the number of CUs. |
|Max Connections |The number of concurrent connections per minute. |10,000 connections/CU |Minute |During the billing cycle, calculate the number of max connections per minute and divide the maximum value by the CU coefficient to get the number of CUs. |
|Data processed |The amount of the data processed (unit: GB). |1 GB/CU |Hour |During the billing cycle, calculate the sum of the amount of data processed and divide the sum by the CU coefficient to get the number of CUs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The data processed refers to the data before any rate limiting is applied to the VPC NAT gateway and after network ACL entries are matched.</div><br> |


<span id="billing-cycle"></span>
## Billing cycle

The billing cycles and settlement cycles are one hour.

At every hour exactly, fees are settled and deducted, and bills are provided.

<span id="billing-example"></span>
## Billing example

A company created a Pay\-by\-CU VPC NAT gateway on September 20, 2023, at 10:30:00 and released the gateway at 12:00:00. The details are as follows:

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5494c4ad417a5dc148eb59b375245704.png) </span>

The number of CUs is calculated as follows:


|Billing Cycle |Performance Metric |Value |Number of CUs |Number of CUs consumed by the instance every hour |
|---|---|---|---|---|
|10:00:00\-11:00:00 |New connections per second |6,000 |6,000 ÷ 1,000 connections/CU = 6 |Take the maximum value, which is 8. |
||Max connections |80,000 |80,000 ÷ 10,000 connections/CU = 8 ||
||Data processed |6 GB |6 GB ÷ 1 GB/CU = 6 ||
|11:00:00\-12:00:00 |New connections per second |8,000 |8,000 ÷ 1,000 connections/CU = 8 |Take the maximum value, which is 10. |
||Max connections |100,000 |100,000 ÷ 10,000 connections/CU = 10 ||
||Data processed |6 GB |6 GB ÷ 1 GB/CU = 6 ||


Assume that the instance unit price is 0.036 USD/hour and the CU unit price is 0.036 USD. The following table describes the costs for each billing cycle:


|Billing Cycle |Instance Fee (USD) |CU Fee (USD) |Total Cost (USD) |
|---|---|---|---|
|10:00:00\-11:00:00 |0.036x 0.5 =0.018 |0.036x 8 =0.288 |0.306 |
|11:00:00\-12:00:00 |0.036x 1 = 0.036 |0.036x 10 =0.36 |0.396 |


<span id="arrears"></span>
## Arrears

For more information on arrears, refer to [Arrears](https://docs.byteplus.com/en/docs/natgateway/Arrears).
