---
title: "Billing overview"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Billing_overview"
---

This article introduces the billing rules for the API gateway product.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The API gateway is planned to be commercialized and start charging on <strong>April 15, 2025</strong>.</div>


<span id="billing-method"></span>
## Billing method

The API gateway uses a Pay\-as\-you\-go Postpaid method, where you use first and pay later based on the product usage multiplied by the unit price to calculate the bill amount, and the amount is directly deducted from your BytePlus account balance.


* **Billing cycle**: The billing is calculated hourly. Within one billing cycle, if the usage duration is less than one hour, it will be calculated as one hour.

* **Settlement period**: Settlements are made hourly, and a bill is issued every hour; the fees are automatically deducted from the account balance. The specific billing time is based on actuality.


<span id="billing-items"></span>
## Billing items

The billing items for the API gateway consist of **APIG instance fees**, **LoadBalancer (CLB) specification fees**, and **Network fees**.

<span id="apig-instance-fees"></span>
### APIG instance fees

The fees for the APIG instance mainly refer to the costs incurred by hosting an APIG instance. API Gateway currently offers **Standard Edition APIG instance** and **Serverless APIG instance**.


* **Standard Edition APIG instance**

   There are four Standard Edition APIG instance specifications, each corresponding to different performance limits. For specific performance details, please refer to the data on the purchase page. It is recommended to select the specification size according to the business volume, and API Gateway will charge fees based on the selected specification and node count.

   
   |Instance specification (CPU) |Instance specification (memory) |Node unit price ( USD/node/hour) |
   |---|---|---|
   |1 Core |2 GiB |0.09 |
   |2 Core |4 GiB |0.14 |
   |4 Core |8 GiB |0.29 |
   |8 Core |16 GiB |0.58 |
   

* **Serverless APIG instance**

   For BytePlus function services, API Gateway offers a special Serverless type APIG instance. This type of APIG instance waives the hosting charges, and each BytePlus account is allowed to create only one in each region.

   
   |Instance specification (CPU) |Instance specification (memory) |Node unit price (USD/node/hour) |
   |---|---|---|
   |Autoscaler |Autoscaler |0.00 |
   


<span id="loadbalancer-specification-fees"></span>
### LoadBalancer specification fees

API Gateway by default creates a LoadBalancer CLB for each instance as the entry point to the gateway. There are six CLB specifications available. For introductions to different specifications, please refer to [Product types and specifications](https://docs.byteplus.com/en/docs/clb/Product-Overview-02). It is recommended to select the specification size based on the business volume, and API Gateway will charge fees according to the selected specification.


|Specifications |Unit price (USD/unit/hour) |
|---|---|
|Small I |0.012 |
|Small II |0.06 |
|Medium I |0.12 |
|Medium II |0.24 |
|Large I |0.48 |
|Large II |0.96 |


<span id="public-network-costs"></span>
### Public network costs

Public network costs support **billing by bandwidth cap** and **billing by actual usage** methods.


* **Billing by bandwidth cap**

   Charges based on your specified bandwidth cap. The platform will throttle based on your specified bandwidth cap, please configure the bandwidth cap according to the actual business situation.

   
   |Unit price type |Specifications |Johor region unit price (USD/hour/Mbps) |
   |---|---|---|
   |Excess progressive unit price |The bandwidth limit is (1 ~ 5) Mbps |0.006 |
   ||Bandwidth limit exceeds 5 Mbps |0.02 |
   

* **Billing by actual usage**

   Charging is based on the actual traffic used in the outbound direction. For business scenarios with large bandwidth fluctuations, billing by actual usage saves costs compared to billing by bandwidth cap.

   
   |Type of unit price |Line |Unit price (USD/GB) |
   |---|---|---|
   |Fixed price |BGP (multiple lines) |0.81 |
   


<span id="billing-formula"></span>
## Billing formula

**Total cost per instance = APIG instance cost + LoadBalancer specification cost + public network cost**

include:


* APIG instance cost = Fixed price (USD/node/hour) × number of nodes × duration of use (hours)

* CLB specification cost = unit price (USD/piece/hour) × 1 (piece) × usage duration (hour)

* Public network cost

   * Billing based on maximum bandwidth limit

      * If bandwidth cap is less than or equal to 5 Mbps: unit price (USD/hour/Mbps) for (1 ~ 5) Mbps × usage duration (hour) × bandwidth cap

      * If bandwidth cap exceeds 5 Mbps: unit price (USD/hour/Mbps) for (1 ~ 5) Mbps × usage duration (hour) × 5 + unit price (USD/hour/Mbps) for bandwidth over 5 Mbps × usage duration (hour) × (bandwidth cap \- 5) (Mbps)

   * Billing based on actual traffic = unit price (USD/GB) × traffic used (GB)


<span id="billing-example"></span>
## Billing example


* **Example 1**

   In Asia Pacific (Johor) region, an APIG instance with 2 nodes of 2c4g, activates a small II specification CLB, opts for pay\-as\-you\-go traffic billing, uses for 24 hours, with traffic usage of 10 GB.

   Total cost = 0.14 × 2 × 24 + 0.06 × 24 + 0.81 × 10 = 16.26 USD

* **Example 2**

   In Asia Pacific (Johor) region, an APIG instance with 2 nodes of 2c4g, activates a small II specification CLB, select the billing based on bandwidth cap, turn on a 5 Mbps public network, and use it for 24 hours.

   Total cost = 0.14 × 2 × 24 + 0.06 × 24 + 0.006 × 5 × 24 = 8.88 USD

* **Example 3**

   In Asia Pacific (Johor) region, an APIG instance with 2 nodes of 4c8g, activates a medium II specification CLB, select the billing based on actual traffic, use 24 hours, with a traffic usage of 100 GB.

   Total cost = 0.29 × 2 × 24 + 0.24 × 24 + 0.81 × 100 = 100.68 USD

* **Example 4**

   In Asia Pacific (Johor) region,an APIG instance with 2 nodes of 4c8g, activates a medium II specification CLB, select the billing based on bandwidth cap, turn on a 20 Mbps public network, and use it for 24 hours.

   Total cost = 0.29 × 2 × 24 + 0.24 × 24 + 0.006 × 5 × 24 + (20\-5) × 0.02 × 24 = 27.6 USD


<span id="configuration-change-description"></span>
## Configuration change description

Currently does not support changing the type and specification of APIG instance.

<span id="unsubscription-description"></span>
## Unsubscription description

Deleting an APIG instance is equivalent to unsubscribing. The APIG instance will be immediately released/destroyed, and you will receive a unsubscription notification from the platform.
