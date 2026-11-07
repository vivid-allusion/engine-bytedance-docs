---
title: "Renewal management"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/renewal_management"
---

You can manually renew a yearly/monthly subscription instance before it expires to prevent your business from being affected by its expiration.

<span id="prerequisites"></span>
## Prerequisites


* The instance has been created and is in the **Running** status.For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* The instance is billed in yearly/monthly subscription mode. For details, refer to [Yearly or monthly subscription](https://docs.byteplus.com/en/docs/RDS_for_MySQL/subscription).

* The instance cannot have unpaid orders for conversion to yearly/monthly subscription.


<span id="precautions"></span>
## Precautions

Post paid billing instances are not subject to expiration and do not need to be renewed, while yearly/monthly subscription instances are subject to expiration, and failure to renew upon expiration can cause business interruption or even data loss.

<span id="renewal-methods"></span>
## Renewal methods

RDS for MySQL supports the following two renewal methods:


* **Automatic renewal**: You can enable automatic renewal when creating a yearly/monthly subscription instance to prevent your business from being affected by the expiration of the instance in case you forget to manually renew the instance. Once it is enabled, the system will automatically renew the instance before expiration each time, so please make sure that your account has a sufficient balance.

* **Manual renewal**: You can manually renew an instance at any time before it expires.


<span id="manual-renewal"></span>
## Manual renewal


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. Select the region for the instance in the upper\-left corner of the top menu bar.

3. Click **Instances** in the left\-side navigation bar.

4. In the **Action** column to the right of the instance on the **Instances** page, click **Renewal**.

5. Confirm the information about the instances to be renewed on the renewal management page.

6. Select the **Renewal duration**, and then click the **Pay** button.

7. On the **Confirm order information** page, confirm the order information and click **Next step**.

8. On the **Submit payment information** page, confirm the payment details and select the payment method, click **Pay**, and complete payment according to the prompts to complete renewal.


<span id="automatic-renewal"></span>
## Automatic renewal

BytePlus supports automatic renewal. After automatic renewal is enabled, the system will automatically deduct the renewal fee from your balance 7 days before the expiration date. After automatic renewal is enabled, the system will first use the cash coupons for renewal if cash coupons are available in your account.


1. Log on to the [Expense Center console](https://console.byteplus.com/finance/overview).

2. Click **Renewal management** in the left\-side navigation bar.

3. On the **Manual renewal items** tab of the **Renewal management** page, click **More \> Activate automatic renewal** in the **Action** column of the resource to renew.

4. You can select the duration of a single automatic renewal in the lower\-left corner of the **Automatic renewal** page and preset the number of times of automatic renewal. Then, click **Enable** in the lower\-right corner to enable automatic renewal.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">If <strong>Preset number of automatic renewals</strong> is not checked, it indicates that automatic renewal takes effect permanently, and the system will automatically renew the instance for the specified duration every time it is set to expire. For more information, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-of-renewal-rules">Renewal Management</a>.</div>
