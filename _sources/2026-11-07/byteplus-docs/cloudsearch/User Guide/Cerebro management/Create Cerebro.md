---
title: "Create Cerebro"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Create_Cerebro"
---

Cerebro is an open\-source visual management tool for Elasticsearch and OpenSearch instances. With Cerebro, you can monitor information such as cluster load, node resources, and index distribution in real time. This document describes how to create Cerebro.

<span id="9zfINzne"></span>
## Operation steps


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the region where you want to create Cerebro.

3. In the left navigation pane, select **Cerebro**, and then click **Create Cerebro**.

4. On the **Create Cerebro instance** page, configure the following parameters, and then click **Confirm order**.

   
   |**Parameter** |**Note** |
   |---|---|
   |Billing type |Select the billing type for the instance. Both **Pay\-as\-you\-go** and **Subscription** are supported. For detailed information about billing, refer to [Billing overview](https://docs.byteplus.com/en/docs/cloudsearch/billing-overview). |
   |Deployment method |Select a deployment method and availability zone based on your business requirements.<br><br><br>* **Single availability zone deployment**: a standard deployment mode typically used for non\-mission\-critical scenarios. Select a suitable availability zone based on your business requirements.<br><br>* **Two Availability Zones Deployment**: a cross\-AZ disaster recovery deployment mode typically used for production scenarios. Select two availability zones.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Deploying across two availability zones improves availability but may introduce a network latency of 2 to 3 ms.</div><br> |
   |Node specification |Select a node specification based on your business requirements. Different specifications have different numbers of CPU cores and amounts of memory. For the node specification types supported by Cloud Search, refer to [Product specifications](https://docs.byteplus.com/en/docs/cloudsearch/specifications). |
   |Number of nodes |The system automatically sets the configuration based on the selected deployment method. This cannot be changed.<br><br><br>* When the **Deployment method** is **Single availability zone deployment**, the number of nodes is**1**。<br><br>* When the **Deployment method** is **Two Availability Zones Deployment**, the number of nodes is**2**。 |
   |Private network |Select a VPC in the same region as your existing cloud services to ensure smooth intranet access. Subnets in different availability zones within the same VPC are interconnected. To create a VPC, refer to [Create private network](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC). |
   |Subnet |The system automatically filters available subnets based on the selected region, availability zone, and private network. To create a subnet, refer to [Create subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet). |
   |Public network access |Select whether to enable public network access. When enabled, the system automatically assigns public network access with dedicated bandwidth, allowing you to access Cerebro from the public network. Enabling public network access incurs additional charges. For details on the fees, refer to [Billing item description](https://docs.byteplus.com/en/docs/cloudsearch/billing-items). The value range is 1 to 200 Mbps. Set the value as needed. |
   |User name |The user name used to log in to Cerebro. Defaults to admin and cannot be changed. |
   |Password |The password for the admin account. Keep it in a safe place. Password requirements are as follows:<br><br><br>* The password must be 8 to 32 characters long and contain at least three of the following: uppercase letters, lowercase letters, numbers, and special characters.<br><br>* The supported special characters are `_#!@$%^&*()+=-`. Spaces and Chinese characters are not allowed. |
   |Confirm password |Enter the password from the previous step. |
   

5. On the **Confirm order** page, complete the subsequent steps based on the selected billing type.

   * If you select **Pay\-as\-you\-go**, on the **Confirm order** page, confirm the order details, read and select **Database Product and Service Terms**, and click **Buy now**.

   * If you select **Subscription**:

      1. On the **Confirm order** page, confirm the order details, read and select **Database Product and Service Terms** and **Unsubscribe Rules**, and then click **Submit order**.

      2. On the **Confirm order information** page, confirm the order information again, and click **Next**.

      3. On the **Submit payment information** page, confirm the payment details and select a payment method, click **Go to payment,**  and follow the prompts to complete the payment and the creation.


<span id="HQnDdH7g"></span>
##
