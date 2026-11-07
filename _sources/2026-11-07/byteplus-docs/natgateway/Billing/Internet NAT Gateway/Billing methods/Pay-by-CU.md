---
title: "Pay-by-CU"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Pay-by-CU"
---

Pay\-by\-CU is a billing method based on connection usage. It is a post\-pay model where you are billed after using the resources. 

<span id=".6LSt5Lmw5YmN5o-Q"></span>
## Prerequisites


* You have completed enterprise real\-name authentication for your account.

* Ensure that the total value of your account's [available balance](https://docs.byteplus.com/en/docs/6269/100429) and coupons applicable to Internet NAT Gateways is not less than 100.00 USD, and the available balance must be no less than 0. For specific operations, see [Recharge](https://docs.byteplus.com/en/docs/6269/100434).


<span id=".5oCn6IO95LiK6ZmQ"></span>
## Performance

NAT Gateway performance cap:


|Metric |New connections per second |Max connections |Max forwarding throughput |
|---|---|---|---|
|Initial limit |100,000 |2,000,000 |5 Gbps |
|Elastic upper limit |400,000 |8,000,000 |40 Gbps |


<span id=".6K6h6LS55YWs5byP"></span>
## Formula

**The cost for a single Pay\-by\-CU NAT Gateway = Instance fee + Hourly CU fee**


* **Instance fee = Instance unit price (USD/hour) × Usage duration (hours)** 

   * Instance fee is the cost for occupying the NAT Gateway resources.

   * Instance unit price: See the console.

   * Usage duration: The actual usage time, calculated precisely to the second.

* **Hourly CU fee = CU unit price (USD/CU) × Hourly CU consumption (CU)** 

   * The CU fee is calculated based on the consumption of Concurrent Units.

   * Hourly CU consumption = **MAX** [CUs from new connections, CUs from concurrent connections, CUs from data processed] per hour. For details, see CU calculation method.

   * CU unit price: See the console.


<span id=".Q1XmlbDph4_orqHnrpfor7TmmI4="></span>
## CU calculation method


|Performance metric |Metric description |CU coefficient |Metering unit |CU calculation method |
|---|---|---|---|---|
|New connections per second |Number of new connections established per second |1,000 connections/CU |Seconds |Within the billing cycle, the new connections per second are counted. The maximum value from these second\-level counts is taken, divided by the CU coefficient, to obtain the CU count derived from new connections for that billing cycle. |
|Max connections |Number of concurrent connections established per minute |10,000 connections/CU |Minutes |Within the billing cycle, the concurrent connections are counted per minute. The maximum value from these minute\-level counts is taken, divided by the CU coefficient, to obtain the CU count derived from concurrent connections for that billing cycle. |
|Data processed |Volume of data processed (Unit: GB) |1 GB/CU |Hours |Within the billing cycle, sum the volume of data processed. Divide this total by the CU coefficient to get the number of CUs derived from the processed data volume for that billing cycle.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The processed data volume refers to the data after Network ACL rule matching but before NAT Gateway rate limiting.</div><br> |


<span id=".57uT566X5ZGo5pyf"></span>
## Settlement cycle

Both the billing cycle and the settlement cycle are on an hourly basis.

On the hour (UTC+8), the platform settles fees, issues bills and deducts corresponding payments from your account balance. For details on bills, see [Bill management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details).

<span id="89HRh9n4"></span>
## Fee example

A company created a Pay\-by\-CU NAT Gateway on September 20, 2023, at 10:30:00 and released it at 12:00:00. The details are as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9786f8fddf47cc2df89af64ce5c01e3d.png) </span>

CU calculation is as follows:


|Billing cycle |Performance metric |Value |CU equivalent |Hourly CU consumption |
|---|---|---|---|---|
|10:00:00\-11:00:00 |New connections per second |6,000 connections |6,000 connections ÷ 1,000 connections/CU = 6 CUs |The maximum value is taken, i.e., 8 CUs. |
||Max connections |80,000 connections |80,000 connections ÷ 10,000 connections/CU = 8 CUs ||
||Data processed |6GB |6 GB ÷ 1 GB/CU = 6 CUs ||
|11:00:00\-12:00:00 |New connections per second |8,000 connections |8,000 connections ÷ 1,000 connections/CU = 8 CUs |The maximum value is taken, i.e., 10 CUs. |
||Max connections |100,000 connections |100,000 connections ÷ 10,000 connections/CU = 10 CUs ||
||Data processed |6GB |6 GB ÷ 1 GB/CU = 6 CUs ||


Assume the instance unit price is 0.1955 USD/hour and the CU unit price is 0.1955 USD/CU. The cost for each specific billing cycle is as follows:


|Billing cycle |Instance fee (USD) |CU fee (USD) |Total fee (USD) |
|---|---|---|---|
|10:00:00\-11:00:00 |0.1955 x 0.5 =0.09775 |0.1955 x 8 = 1.564 |1.66 |
|11:00:00\-12:00:00 |0.1955 x 1 = 0.1955 |0.1955 x 10 = 1.955 |2.15 |
