---
title: "Manage triggers"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Manage_triggers"
---

This article introduces operations for managing triggers, including editing triggers, resetting the Webhook URL, deleting triggers, and more.

<span id=".57yW6L6R6Kem5Y-R5Zmo"></span>
## Edit a trigger

By editing the trigger, you can update its configuration items.


1. Go to the Trigger tab in the pipeline.

   1. Log in to [Code Pipeline Console](https://console.byteplus.com/cp).

   2. Select **workspace** in the left navigation bar.

   3. Click the name of the target workspace to enter that workspace.

   4. In the pipeline tab, click the target pipeline name to enter the run records tab for the current pipeline.

   5. Click **Trigger**, then switch to the Trigger tab.

2. Select the target trigger, click **Edit** in the actions column, and the update trigger panel will open.

3. Modify the content of configuration items as needed. After making changes, click **OK**.


<span id=".6YeN572uLXdlYmhvb2stdXJs"></span>
## Reset webhook URL

Resetting the Webhook URL will revoke the pipeline's current Webhook URL and generate a new one, addressing malicious triggers caused by Webhook URL leakage and enhancing business security.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After resetting the Webhook URL, you must go to the corresponding code repository or your platform to configure a new pipeline Webhook URL. Otherwise, code source triggers or Webhook triggers will not take effect.</div>



1. On the Trigger tab, select the target code source trigger or the webhook trigger, and click **Edit** in the Actions column to open the Update Trigger panel.

2. Click the reset button next to the URL.

3. In the confirmation dialog, click **Reset** to complete resetting the pipeline Webhook URL.


<span id=".5Yig6Zmk6Kem5Y-R5Zmo"></span>
## Delete trigger

Support deleting triggers that are no longer in use.


1. On the trigger tab, select the target trigger, then click **Delete** in the actions column. A confirmation dialog appears.

2. Review the trigger information and click **Delete**.
