---
title: "Renewal instructions"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/renewal_management"
---

Pay\-as\-you\-go instances are not subject to expiration and do not need to be renewed, while yearly/monthly subscription instances are subject to expiration, and failure to renew upon expiration can cause business interruption or even data loss.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have [created an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance), and the instance is in the **Running** status.

* [The instance billing method is ](https://docs.byteplus.com/en/docs/RDS_for_PG/subscription)yearly/monthly subscription.

* The instance cannot have unpaid orders for conversion to yearly/monthly subscription.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Pay\-as\-you\-go instances are not subject to expiration and do not need to be renewed, while yearly/monthly subscription instances are subject to expiration, and failure to renew upon expiration can cause business interruption or even data loss.

<span id=".5omL5Yqo57ut6LS5"></span>
## Manual renewal


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. Select the region for the instance in the upper\-left corner of the top menu bar.

3. On the **instances** page, click  **...\> Renewal** button of **Actions** column in the right.

4. Confirm the information about the instances to be renewed on the renewal management page.

5. Select the Renewal duration, and then click the **To pay** button.

6. Confirm the amount, and click **Next step** to pay.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also go directly to the <a href="https://console.byteplus.com/finance/renew/">Renewal management</a> page to find the target instance for renewal.</div>


<span id=".6Ieq5Yqo57ut6LS5"></span>
## Automatic renewal

The Volcengine platform supports automatic renewal. After enabling automatic renewal, the system will automatically deduct the renewal fee from your balance 7 days before expiration. After enabling automatic renewal, if your account has available vouchers, the system will prioritize using vouchers for renewal.


1. Log on to the [Expense Center console](https://console.byteplus.com/finance/account-overview/).

2. Click **Renewal management** in the left\-side navigation bar.

3. On the **Manual renewal** items tab of the Renewal management page, click **More \> Activate automatic renewal** in the Actions column of the resource to renew.

4. On the **Automatic renewal** page, select the duration for a one\-time automatic renewal at the bottom left corner, set the number of automatic renewals, and then click the **Activate** button at the bottom right corner to activate the automatic renewal.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If <strong>Preset automatic renewal times</strong> is not checked, automatic renewal will be permanently effective. The system will perform automatic renewal before each resource expires based on the duration of a single automatic renewal. For more details, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-subscription-renewal">Managing Subscription Renewal</a>.</div>
