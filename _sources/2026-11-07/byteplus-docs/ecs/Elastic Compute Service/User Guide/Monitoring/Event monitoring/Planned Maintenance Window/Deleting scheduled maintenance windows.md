---
title: "Deleting scheduled maintenance windows"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Deleting_scheduled_maintenance_windows"
---

Deleted scheduled maintenance window tasks cannot be recovered. Proceed with caution.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Deleting a scheduled maintenance window task in the <strong>Enabled</strong> status:</div>


   * <div data-tips="true" data-tips-type="default">Authorized "Redeploy" operations will continue to completion normally.</div>


   * <div data-tips="true" data-tips-type="default">For any related events subsequently triggered by resources associated with this window, automatic authorization will no longer be performed via this window. To resume automatic authorization, <a href="https://docs.byteplus.com/en/docs/ecs/Creating_scheduled_maintenance_windows">recreate a scheduled maintenance window</a>.</div>


* <div data-tips="true" data-tips-type="default">Deleting a scheduled maintenance window task in the<strong> Disabled </strong>status: This only affects your ability to view the execution task. It does not impact the corresponding services.</div>



<span id="kheEQTLX"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> System Events".

3. Select the region where your business is located.

4. Click the "Scheduled maintenance window" tab.

5. In the "Actions" column of the target scheduled maintenance window, click the "Delete" button.

6. After you confirm the information of the scheduled maintenance window to be deleted, click the "Confirm" button to complete the operation.
