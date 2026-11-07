---
title: "Restore factory settings for Claw instance"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Restore_Claw_instance_to_factory_settings"
---

When an employee Claw experiences configuration corruption resulting in service crashes, system failures, or abnormal status, and neither restart nor auto healing resolves the issue, the administrator can restore Claw to factory settings to reset it to its initial available status. **This article describes how to restore factory settings for a Claw instance.** 

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Restoring factory settings will <strong>clear all configurations and data of the target Claw instance</strong> (including task records, skill configurations, files, and more) and restore it to its initial state. <strong>This operation is irreversible.</strong></div>


* <div data-tips="true" data-tips-type="warning">To retain current data, please create a manual backup in advance using the <a href="https://docs.byteplus.com/en/docs/ArkClaw/Backing_up_and_restoring_ArkClaw_instances?lang=en">backup/restore</a> feature before performing the operation.</div>


* <div data-tips="true" data-tips-type="warning">During the factory reset process, the Claw instance will be unavailable, and the process is expected to take about 1 minute.</div>


* <div data-tips="true" data-tips-type="warning">After the restore is complete, employees need to reconfigure the skills, preferences, and other settings for Claw. It is recommended to notify relevant employees in advance.</div>



<span id="Lw8U2JTb"></span>
## Scenario

Restoring factory settings is the last resort. It is recommended to attempt recovery in the following priority order:


1. [Restart Claw instance](https://docs.byteplus.com/en/docs/ArkClaw/Restart_Claw_instance?lang=en)

2. [Auto healing](https://docs.byteplus.com/en/docs/ArkClaw/Auto_healing_for_Claw_instances?lang=en)

3. [Restore backup](https://docs.byteplus.com/en/docs/ArkClaw/Backing_up_and_restoring_ArkClaw_instances?lang=en) (retain data and roll back to a normal time point)

4. Restore factory settings (this article, clear all data)


<span id="eYrsPFzp"></span>
## Procedure


1. Log in to [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise)[ArkClaw Group console](https://console.byteplus.com/arkclaw/enterprise/group/)[ArkClaw OMNI console](https://console.byteplus.com/arkclaw/enterprise/omni).

2. In the left navigation pane, click "Claw Management \> Claw List".

3. Under the "Instances" tab, you can view the list of employee Claw/shared Claw instances that have been created,

4. In the Claw instance list, click "More \> Restore factory settings" in the "Actions" column for the target Claw instance.

5. In the dialog box that appears, click "Restore factory settings" to complete the operation.

6. After the operation is complete, return to the Claw list page, confirm that the target Claw instance status has been restored to "Running", and notify employees that the Claw instance has been reset and that they need to reconfigure skills and preferences.
