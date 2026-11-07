---
title: "Managing audit logs"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Manage_Audit_log"
---

After enabling log audit, you can configure the log retention period and disable this feature in the CR console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more TLS information, see <a href="https://docs.byteplus.com/en/docs/tls/What_is_TLS">What is Torch Log Service</a>.</div>


<span id=".5YWz6Zet5pel5b-X5a6h6K6h"></span>
## Disable log audit

You can disable log audit for an instance to save log service costs.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After you disable this feature, the CR audit log topic will be deleted from the TLS. After deletion, historical logs cannot be restored. If you re\-enable the audit log feature, only newly generated logs can be viewed.</div>



1. Log in to the target instance.

   1. Log in to the[ CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **Instance list**. Then, in the **Instance list** area, find the Standard Edition instance where you need to create an artifact repository and click **Enter instance**.

2. On the Standard Edition instance details page, click **Audit log** in the left navigation bar.

3. On the **Audit log** page, click **Close associated logs**.

4. On the confirmation page, enter the required confirmation information as prompted.

5. Click **confirm** to complete the operation.


<span id=".6K6-572u5pel5b-X5L-d5a2Y5pe26Ze0"></span>
## Set log retention time

You can specify the log retention period based on your business needs.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The retention time can be set from 1 to 3650 days. You are charged for TLS for any retention period beyond 7 days. For TLS billing details, see <a href="https://docs.byteplus.com/en/docs/tls/billable_items">Billable items</a>.</div>



1. Log in to the target instance.

   1. Log in to the[ CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **Instance list**. Then, in the **Instance list** area, find the Standard Edition instance where you need to create an artifact repository and click **Enter instance**.

2. On the Standard Edition instance details page, click **Audit log** in the left navigation bar.

3. On the **Audit log** page, click **Set log retention time**.

4. Enter the required retention time in **Retention time**.
