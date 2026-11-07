---
title: "Managing triggers"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Managing_triggers"
---

After creating triggers, you can manage them. This article introduces how to view, update, enable, disable, and delete triggers.

<span id="view-trigger"></span>
## View trigger

FaaS supports viewing the information of created triggers.


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. Select the region where your business is located in the top navigation bar.

3. On the **Function** page, find the target function and click the function name.

4. On the function details page, click the **Trigger** tab to view all triggers created for this function.


<span id="update-trigger"></span>
## Update trigger

FaaS supports updating certain parameters of triggers, subject to actual conditions.


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. Select the region where your business is located in the top navigation bar.

3. On the **Function** page, find the target function and click the function name.

4. On the function details page, under the **Trigger** tab, find the trigger that needs updating and select  **`...`**   **\> Edit**.

5. On the **Edit trigger** panel, update the trigger parameters.

6. Click **Confirm** to complete the update.


<span id="enable-disable-trigger"></span>
## Enable/Disable trigger

For triggers with an enable switch, the trigger can only function properly after being enabled. If you temporarily do not need to trigger the function, you can disable the target trigger.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Timer triggers, Kafka triggers, RocketMQ triggers, BMQ triggers, and TLS triggers support enable/disable operations.</div>



1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. Select the region where your business is located in the top navigation bar.

3. On the **Function** page, find the target function and click the function name.

4. On the function details page, under the **Trigger** tab, find the target trigger and toggle the switch in the top right corner to enable/disable the trigger.


<span id="delete-trigger"></span>
## Delete trigger

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Once deleted, a trigger cannot be restored and must be recreated; proceed with caution.</div>



1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. Select the region where your business is located in the top navigation bar.

3. On the **Function** page, find the target function and click the function name.

4. On the function details page, under the **Trigger** tab, find the trigger that needs deleting and select  **`...`**   **\> Delete**.

5. In the pop\-up dialog, click **Confirm** to delete the trigger.
