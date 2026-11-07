---
title: "Troubleshooting and handling methods for insufficient ArkClaw memory"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Troubleshooting_and_handling_methods_for_insufficient_ArkClaw_memory"
---

When an ArkClaw instance runs out of memory, an insufficient memory alert will be triggered. You can receive notifications via [system messages](https://docs.byteplus.com/en/docs/87732/2356378?lang=zh) or configured [message channels](https://docs.byteplus.com/en/docs/87732/2266749?lang=zh). This issue may cause partial task failures, unexpected service exits, request timeouts, and other anomalies.

This topic guides you to quickly resolve the insufficient memory issue and ensure stable business operations.

<span id="HH3YQnje"></span>
## Causes and trigger scenarios of insufficient memory

When the available memory of the ECS instance hosting the ArkClaw instance drops below the runtime memory threshold, an insufficient memory issue is triggered. High\-load scenarios that commonly exhaust memory resources are listed below:


* **Excessive browser occupancy**: Multiple cloud Chrome windows or tabs run simultaneously.

* **Dependency installation**: Large\-scale dependencies are installed via commands such as npm install and pip install.

* **Data processing**: Sharp memory spikes are caused by reading/writing large files or batch data conversion.

* **Concurrent tasks**: Multiple high\-load tasks (for example, scheduled tasks) run concurrently within a similar time window, causing spikes in memory usage.


<span id="31bEUkKT"></span>
## **Handling methods for insufficient memory**

The following four methods are provided to resolve the insufficient memory issue. Select a method based on your needs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If you <strong>are temporarily unable to determine</strong> the method, we recommend that you troubleshoot and resolve the issue in the following order: "<strong>Close browsers \> Restart ArkClaw \> Check for updates \> Troubleshoot scheduled tasks</strong>".</div>



|**Handling method** |**Application scenarios** |**Chargeable** |**Description** |
|---|---|---|---|
|Close browsers |Applicable when too many browser windows or idle web tasks are opened on the [cloud PC](https://docs.byteplus.com/en/docs/ArkClaw/Overview_cua?lang=zh).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Perform this operation only when ArkClaw is accessible.</div><br> |No |Close browser windows that are no longer required to quickly release running resources and reduce the recurrence of the insufficient memory issue. |
|Restart ArkClaw |Applicable when the issue persists after the browsers are closed, or ArkClaw stops responding and tasks run abnormally. |No |[Restart ArkClaw](https://docs.byteplus.com/en/docs/ArkClaw/Restarting_ArkClaw__?lang=zh) to restore the operating environment and release occupied memory. |
|Check for updates |Applicable when program memory leaks and memory anomalies caused by incompatible plugins occur. |No |Fix memory leaks and resolve memory anomalies caused by incompatible plugins by upgrading ArkClaw to the latest version. |
|Troubleshoot scheduled tasks |Applicable to scenarios where insufficient memory occurs periodically or repeatedly. |No |Optimize memory usage by adjusting the execution time of scheduled tasks or disabling idle tasks. |


<span id="uD7JhtPy"></span>
## Procedure

<span id="U0aWzMUC"></span>
### Method 1: Close browsers (**when ArkClaw remains operational**)

If you have opened multiple Google Chrome windows on the ArkClaw [cloud PC](https://docs.byteplus.com/en/docs/ArkClaw/Overview_cua?lang=zh) or have idle web tasks, we recommend that you close browsers that are no longer required first to release some running resources and reduce the risk of recurring insufficient memory issues.


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Close the target browsers as needed.


<span id="qMbGOelS"></span>
### Method 2: Restart **ArkClaw** to restore the operating environment

If the issue persists after the browsers are closed, ArkClaw becomes unresponsive, or tasks and services run abnormally, you may restart ArkClaw to restore the operating environment and release occupied memory.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">A restart will interrupt all running tasks. Unsaved temporary data, including in\-memory variables and cache not flushed to disks, will be lost. Confirm that no critical tasks are in progress before proceeding with the restart.</div>



1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Go to the target ArkClaw page.

3. In the upper\-right corner of the ArkClaw chat page, select "More  **\>**  Restart". [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Restarting_ArkClaw__?lang=zh).


<span id="yz7dbGtx"></span>
### Method 3: Upgrade the ArkClaw system and component versions by checking for updates

You can fix memory leaks and resolve memory anomalies caused by incompatible plugins by upgrading ArkClaw to the latest version.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Restart ArkClaw first before checking for updates. The update process occupies system resources. If the update is performed under high memory load, it is likely that the update will fail and further increase the operating pressure on the device.</div>



1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Go to the target ArkClaw page.

3. In the upper\-right corner of the ArkClaw chat page, click "...  **\>**  Check for updates". [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Upgrading_ArkClaw_version_?lang=zh).


<span id="uKhTtMqP"></span>
### Method 4: Troubleshoot whether scheduled tasks cause high load

If insufficient memory occurs periodically or repeatedly, it is generally caused by resource occupation of background scheduled tasks. You can optimize memory usage by adjusting the execution time of scheduled tasks or disabling idle tasks.


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Go to the target ArkClaw page.

3. In the left\-side navigation pane, click "Initiate task".

4. In the chat input box, copy and send the following prompt to activate the troubleshooting logic.

   > Prompt: List all scheduled tasks, and check which ones consume high load and whether any tasks have overlapping execution time.   
   

5. If the troubleshooting results indicate high\-load tasks or concurrent tasks with overlapping execution time, we recommend that you adjust the execution time of scheduled tasks or disable idle tasks to relieve memory pressure. For detailed operations, see [Viewing and configuring scheduled tasks](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_and_configuring_scheduled_tasks__?lang=zh).
