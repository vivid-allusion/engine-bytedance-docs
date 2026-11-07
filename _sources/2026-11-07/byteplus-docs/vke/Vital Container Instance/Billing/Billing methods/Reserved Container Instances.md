---
title: "Reserved Container Instances"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VCI-Reserved-Container-Instance"
---

VCI supports Reserved Container Instances (RCIs). This topic describes RCI in detail and how to purchase RCIs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"> [<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- apply for trial</strong></a>]: This feature is currently in beta. Submit an application to use it.</div>


<span id=".5qaC6L-w"></span>
## Overview

RCI is a prepayment deduction voucher\-style offering that supports resource reservation, and is used to offset fees for pay\-as\-you\-go VCIs.

Compared with pay\-as\-you\-go VCIs, the advantages and disadvantages of RCIs are as follows:


|Sales type |Advantage |Disadvantage |
|---|---|---|
|Pay\-as\-you\-go billing |Supports business scenarios requiring frequent creation, deletion, and switching of VCIs. |* Cannot guarantee resource supply. Instances with certain specifications may be sold out.<br><br>* No monthly discounts are available. |
|Reserved Container Instances |* Offers monthly discounts.<br><br>* Guarantees resource supply.<br><br>* Supports business scenarios requiring frequent creation, deletion, and switching of VCIs. |No |


<span id=".6LSt5LmwLXJjaQ=="></span>
## Purchasing RCIs


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Vital Container Instance** \> **Reserved Container Instance**.

4. On the **Reserved Container Instance** page, click **Purchase Reserved Container Instances**.

5. Configure the RCI parameters according to system prompts and your actual requirements.

   
   |Parameter |Description |
   |---|---|
   |**Basic Information** ||
   |Name |Specify an RCI name that complies with the displayed naming rules. This name uniquely identifies the RCI. |
   |Availability zone |Select an availability zone for the RCI. Supported availability zones are as shown on the RCI purchase page. |
   |**Resource reservation** ||
   |Type |Select the specification type of the VCI, including **General\-purpose** and **GPU Accelerated**. For details, see [VCI specifications](https://docs.byteplus.com/en/docs/vke/VCI-instance-types). |
   |Instance family |Select the specific instance family under the instance type. Supported specifications vary by region and availability zones. For details, see [Regions and availability zones](https://docs.byteplus.com/en/docs/vke/VCI-Regions-and-Availability-Zones). |
   |Specification quantity |Select an instance specification to reserve and enter the reservation quantity. |
   |Reservation time |Select a reservation duration for the instance specification.<br><br>The duration starts one hour after you click **Buy now**. The specified VCI specification will be reserved for the specified reservation duration. |
   |Automatic Renewal |Specify whether the RCI will be automatically renewed upon expiration. If you enable auto\-renewal upon expiration, the platform will automatically deduct the amount from your account balance or available vouchers before the RCI expires, and extend the reservation period according to the pre\-configured reservation duration. You do not need manual renewal.<br><br>You can cancel auto\-renewal in the [Billing center](https://console.byteplus.com/finance/renew).  For details, see [Overview of renewal rules](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-of-renewal-rules). |
   

6. View and confirm the fees displayed in the **Actual cost** field. Click **Buy now**.

   When you create a VCI with specified specifications, the system prioritizes fulfillment of the instance specifications through the reserved resource pool.


<span id=".566h55CGLXJjaQ=="></span>
## Managing RCIs

After purchasing an RCI, you can manage it using the following steps.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Vital Container Instance** \> **Reserved Container Instance**.

4. On the **Reserved Container Instances** page, view and manage your RCIs.

   
   |Action |Description |
   |---|---|
   |View details |Click the RCI name to enter the **Reserved Container Instance details** page, where you can view basic information, reserved resource quantity, package details, and more. |
   |Renew |Configure renewal settings for the RCI to extend the reservation duration beyond the original reservation period.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only RCIs in the <strong>Valid</strong> state support renewal. Other states (such as <strong>Canceled</strong> and <strong>Invalid</strong>) do not support renewal. For RCIs in a state that does not support renewal, you can purchase RCIs again to have equivalent outcomes.</div><br> |
   |Usage details |Go to the [Billing center](https://console.byteplus.com/finance/resource-package/) to view the RCI details. |
   |Cancel subscription |For detailed cancellation rules, see [Unsubscription Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management). |
   |Delete |RCIs that are not in the **In effect** state can be deleted. |
