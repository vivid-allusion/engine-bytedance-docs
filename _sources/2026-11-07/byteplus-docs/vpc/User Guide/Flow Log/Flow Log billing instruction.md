---
title: "Flow Log billing instruction"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Flow-log-billing"
---

Flow logs currently support pay\-as\-you\-go billing.

<span id=".6K6h6LS56aG5"></span>
## Billing items


* **VPC Flow Log Generation Fee**

   **Single VPC flow log generation fee = Flow Log Generation Volume (GB) × Generation Unit Price (USD/GB).** 

   VPC Flow Log Generation Fee refers to the cost charged by the Virtual Private Cloud (VPC) for collecting, processing, and generating flow logs from network interface data.

   * **Flow log generation unit price**

      The unit price for each calendar month is as shown in the table below:

      
      |Flow Log Generation Volume Tiers (per calendar month) |Generation unit price (USD/GB) |
      |---|---|
      |0TB\-10TB |0.37 |
      |10TB\-30TB |0.185 |
      |30TB\-50TB |0.074 |
      |Greater than 50 TB​​ |0.037 |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">1TB = 1024GB.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Each account receives a 5GB free tier quota (flow log generation volume) per calendar month.      </div>
      

   * **Billing example**

      The flow log generation details for a user in June are shown in the figure below:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_08c1224f60c9a696abd26b2eba711a72.png) </span>

      The VPC Flow Log generation fees are detailed in the following table:

      
      |Flow Logs Volume Tier (Monthly) |Flow log generation volume (TB) |Generation unit price (USD/GB) |VPC flow log generation fee (USD) |
      |---|---|---|---|
      |0TB\-10TB |10 |0.37 |(10 x 1024 \- 5) x 0.37 =3786.95 |
      |10TB\-30TB |20 |0.185 |20 x 1024 x 0.185= 3788.8 |
      |30TB\-50TB |20 |0.074 |20 x 1024 x 0.074  =  1515.52 |
      |Greater than 50 TB​​ |5 |0.037 |5 x 1024 x 0.037 = 179.2 |
      |Total ||| 9279.47 |
      

   * **Billing cycle**

      Billing Cycle & Settlement Cycle: Both are based on calendar hours.

      On the hour of each hour (UTC+8), the platform settles fees, issues bills and deducts payments. For details on bills, see [Bill management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details).

* **TLS fee**

   VPC Flow Log data is stored in the Torch Log Service (TLS), where you can view and analyze the data. 


<span id=".5qyg6LS56K-05piO"></span>
## Arrears description

An overdue account balance will lead to the suspension of Flow Log services and may even result in resource release. The platform has set a grace period for resources. Within the grace period, the resources are retained and you can continue using the resources after you recharge your account and clear overdue payments. No impact on the features of resources. If the payment overdue period is exceeded, Flow Log resources will be forcibly reclaimed, and all related data will be permanently irrecoverable. Regardless of whether your instances are suspended or released, you shall settle the issued bills based on the actual. 

The operational and billing status of flow log resources after payment becomes overdue is shown in the following diagram:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_308004eb840dc7310cd3a783c1868825.png) </span>

Based on Your settings, the platform will send you reminders via SMS, email, or internal message during stages such as flow log arrears, service suspension due to arrears, and resource release due to arrears. The specific suspension time is subject to the actual situation.
