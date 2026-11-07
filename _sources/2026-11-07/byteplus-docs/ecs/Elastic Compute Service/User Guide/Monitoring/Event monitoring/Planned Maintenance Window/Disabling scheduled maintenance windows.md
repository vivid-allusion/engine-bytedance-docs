---
title: "Disabling scheduled maintenance windows"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Disabling_scheduled_maintenance_windows"
---

You can disable a scheduled maintenance window in the **Enabled** status as needed. After the scheduled maintenance window is disabled:


* O&M actions in progress will continue uninterrupted and complete normally.

* Automatic authorization for O&M events triggered by resources associated with this window will be suspended. Proceed with caution.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Disabling a window only suspends the automatic authorization mechanism. The window configuration will not be deleted. The mechanism resumes when you re\-enable the window.</div>


<span id="YKy5u602"></span>
## Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> System Events".

3. Select the region where your business is located.

4. Click the "Scheduled maintenance window" tab.

5. In the "Actions" column of the target scheduled maintenance window, click the "Disable" button to complete the operation.
