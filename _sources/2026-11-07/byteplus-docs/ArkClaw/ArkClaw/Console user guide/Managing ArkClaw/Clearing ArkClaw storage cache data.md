---
title: "Clearing ArkClaw storage cache data"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Clearing_ArkClaw_storage_cache_data0"
---

This topic describes how to use the one\-click cleanup feature to safely and quickly free up storage capacity on your ArkClaw. This feature only clears temporary cache data generated during ArkClaw runtime. It does not affect your personal data, installed skills, or plugins.

<span id="s5OiyeNZ"></span>
## Applicable scenarios

You can use one\-click cleanup to clear the cache in the following scenarios:


* **Insufficient storage space**: Storage usage on your ArkClaw is close to or has reached the upper limit (for example, more than 80% of total capacity), which affects normal task execution.

* **Routine maintenance**: After a long time of usage, the accumulated cache causes ArkClaw to respond slowly or run sluggishly.

* **Troubleshooting of storage usage exception**: When storage usage increases abnormally, you need to rule out cache accumulation before further investigation.


<span id="KsHwrUgZ"></span>
## Limits

Only ArkClaw in **Running ** status supports one\-click cleanup.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You cannot use one\-click cleanup when the target ArkClaw is in Restarting, Repairing, Initializing, or other exception status. Wait until ArkClaw resumes normal operation before proceeding.</div>


<span id="xf3M3IhS"></span>
## Usage notes

The one\-click cleanup feature only deletes temporary **cache data ** generated during ArkClaw runtime. ArkClaw remains available both during and after the cleanup process. The cleanup scope is as follows:


|Data type |Clear |Description |
|---|---|---|
|npm cache |Yes |Dependency cache generated during npm package installation. |
|npx runtime cache |Yes |Temporary runtime cache generated when npx executes tools. |
|System package manager cache |Yes |Installation packages and index data downloaded by the built\-in system package manager (such as apt or yum) when installing or updating software. |


<span id="cCbEd6bP"></span>
## Procedure


1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/).

2. Switch to the target ArkClaw page and click the Claw details page icon in the upper\-right corner.

3. On the ArkClaw details page, select the "Status and usage" tab.

4. Click the "Clear" button.

5. In the dialog box, confirm the cache data to be cleared, and then click "Clear" to start the cleanup.

6. After the cleanup is complete, view the result from the dialog box, including the total amount of cache released and the cleanup details for each cache type. Confirm the result, and then click "Complete" to close the dialog box.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The cleanup task runs in the background. You can close the dialog box directly <strong>without interrupting the cleanup</strong>. The result takes effect automatically after the task is complete.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To manage or clear non\-cache files (for example, skill installation packages or plugins).   </div>
