---
title: "Granting read-only access to Cloud Monitor"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Grant_read-only_permission_for_account_cloud_monitoring"
---

This topic explains how to give a user read\-only access to Cloud Monitor.

<span id="0ead8fe3"></span>
## Scenario

To view TOS usage statistics, you must have read\-only access to Cloud Monitor.

<span id="caa30b2e"></span>
## Recommended authorization method

We recommend using an IAM policy in this scenario. For more information about IAM policies, see [Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).

<span id="527215fa"></span>
## Notes

If a configured permission does not take effect, we recommend that you retry later, as there is a delay.

<span id="eebd230b"></span>
## Steps


1. Log in to the [IAM console](https://console.byteplus.com/iam/).

2. In the left navigation pane, click **User**.

3. In the **User** list, click **Authorize** in the **Actions** column of the user you want to authorize.

4. On the **Add authorization** page, enter CloudMonitor in the search box. Then, check the box for **CloudMonitorReadOnlyAccess**, and click **Submit**.
