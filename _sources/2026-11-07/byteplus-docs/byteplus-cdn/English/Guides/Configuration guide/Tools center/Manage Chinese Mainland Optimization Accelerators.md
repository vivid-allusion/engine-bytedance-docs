---
title: "Manage Chinese Mainland Optimization Accelerators"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cross-mlc-border-acceleration_en-us"
---

<span id="overview"></span>
## Overview

BytePlus CDN provides **Chinese Mainland Optimization** in the Tool Center. This feature lets you create and manage dedicated accelerators and bind CDN domains to them. After you bind domains to an accelerator, traffic from the Chinese Mainland to those domains is routed through the accelerator's GA CNAME. This improves performance for users in the Chinese Mainland when they access CDN domains whose service region is set to **Outside the Chinese Mainland**.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you use this feature for the first time, you must authorize BytePlus CDN to use BytePlus Global Accelerator. BytePlus Global Accelerator charges apply. Actual charges are based on your final bill.</div>


<span id="limits"></span>
## Limits

Before you use Chinese Mainland Optimization, note the following limits:


* Each accelerator can be bound to up to 500 CDN domains. The Bind Domains drawer shows how many remaining domains you can bind.

* Only accelerators in the Running state can be bound to domains. If an accelerator is still being configured, wait until the setup is complete.

* Only domains whose service region is Outside the Chinese Mainland can be bound to an accelerator.

* In the Bind Domains drawer, domains with a lock icon cannot be selected.

* You cannot delete an accelerator that is bound to domains. Unbind all domains from the accelerator and wait for the rollback to complete before you delete it.


<span id="open-page"></span>
## Open the Chinese Mainland Optimization page

Steps:


1. Log on to the [BytePlus CDN console](https://console.byteplus.com/cdn).

2. In the left navigation pane, click **Tool Center** \> **Chinese Mainland Optimization**.

3. If authorization is required, click **Authorize Now** and complete the authorization for BytePlus CDN to use BytePlus Global Accelerator.


After authorization is complete, you can view and manage accelerators on the **Chinese Mainland Optimization** page. The list shows **Accelerator ID/Name**, **Status**, **Billing Method**, **Validity Period**, **Domains**, and **Actions**.

<span id="create-accelerator"></span>
## Create an accelerator

Steps:


1. On the **Chinese Mainland Optimization** page, click **Create Accelerator**.

2. In the **Create Dedicated Accelerator** dialog box, review the accelerator configuration and billing information.

3. Click **Confirm and Create**.


The dialog box displays the following configuration details.


|**Configuration** |**Description** |
|---|---|
|Accelerator Type |The accelerator type is **Standard Accelerator**. |
|Service Region |The service region is **Asia Pacific**. |
|Network Type |The accelerator uses **Premium Route** as the network type. |
|Billing Method |The billing method is **Postpaid**. |
|Estimated Cost |Click **View Specifications and Pricing** to view billing details. Actual charges are based on your bill. |


After you create the accelerator, provisioning usually takes 2 to 5 minutes. Do not create another accelerator during this time.

<span id="view-accelerators"></span>
## View and manage accelerators

On the **Chinese Mainland Optimization** page, you can perform the following actions:


* **View Details**: Open the accelerator details page in the Global Accelerator console.

* **Manage Domains**: Open the accelerator details page in the CDN console to view and manage bound CDN domains. You can also click **Accelerator ID/Name** to open this page.

* **Delete**: Delete an accelerator that is not bound to any domains.


On the accelerator details page, you can view **Basic Information** and **Bound CDN Domains**. The **Basic Information** section shows **Accelerator Name**, **Accelerator ID**, **Status**, **Line Type**, and **Billing Method**. For accelerators created by this feature, the **Line Type** value is **Premium Public Network**. The **Bound CDN Domains** section shows **Domain**, **Domain Status**, **Acceleration CNAME**, **Chinese Mainland Optimization**, **Project**, and **Actions**.

<span id="bind-domains"></span>
## Bind domains

You can bind CDN domains to an accelerator. After the domains are bound, their Chinese Mainland traffic uses the selected accelerator. Traffic from the Chinese Mainland to these domains is routed through the accelerator's GA CNAME.

Steps:


1. On the **Chinese Mainland Optimization** page, find an accelerator whose status is **Running**.

2. Click **Manage Domains** to open the accelerator details page.

3. In the **Bound CDN Domains** section, click **Bind Domains**.

4. In the **Bind Domains** drawer, select the CDN domains that you want to bind.

   * You can filter domains by **Project** and **Domain Status**.

   * You can use **Exact Match** or **Fuzzy Match** to search for domains.

   * If a domain has a lock icon, the domain cannot be selected. Domains whose service region is not **Outside the Chinese Mainland** cannot be selected.

5. Click **Confirm**.

6. In the confirmation dialog box, confirm the number of selected domains, and then click **Bind Domains**.


<span id="unbind-domains"></span>
## Unbind domains

After domains are unbound, they no longer use the GA CNAME of the accelerator that they were bound to. Traffic from the Chinese Mainland to these domains returns to standard CDN routing.

Steps:


1. Open the accelerator details page.

2. In the **Bound CDN Domains** section, select the domains that you want to unbind.

3. Click **Bulk Unbind**.

   * To unbind a single domain, you can also click **Delete** in that domain's row.

4. In the confirmation dialog box, confirm the number of selected domains, and then click **Unbind Domains**.


<span id="delete-accelerator"></span>
## Delete an accelerator

You can delete an accelerator that is not bound to any domains.

Steps:


1. On the **Chinese Mainland Optimization** page, find the accelerator that you want to delete.

2. In the **Actions** column, click **Delete**.

3. In the confirmation dialog box, click **Confirm Deletion**.


If the accelerator is bound to domains, the console displays **Cannot Delete Accelerator**. Unbind all domains from the accelerator and wait for the rollback to complete before you delete it.
