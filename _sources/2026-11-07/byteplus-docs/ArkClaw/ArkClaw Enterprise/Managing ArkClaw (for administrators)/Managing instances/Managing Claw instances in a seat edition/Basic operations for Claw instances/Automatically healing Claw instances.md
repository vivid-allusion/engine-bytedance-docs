---
title: "Automatically healing Claw instances"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Auto_healing_for_Claw_instances"
---

When an enterprise employee's Claw becomes unavailable due to task exceptions, configuration adjustments, or other reasons, the administrator can use the auto healing feature to restore Claw to its most recent available status. **This article describes how to perform the auto healing operation in the Claw list.** 

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Auto healing automatically identifies the current cause of the Claw instance failure and attempts to roll back the configuration and runtime environment to the most recent backup state where it was running normally. If auto backup is not enabled, the rollback restores the Claw instance to its default state after initial creation.</div>



* <div data-tips="true" data-tips-type="default">Auto healing restores the Claw instance to its most recent available state. During the repair process, the instance is be temporarily unavailable (about 1–3 minutes).</div>


* <div data-tips="true" data-tips-type="default">During the repair process, configuration changes made after the most recent failure may be lost. To retain the configuration, save the instance status using the "Backup/Restore" feature before performing the repair.</div>



<span id="2tacoGm8"></span>
## Scenarios


* Task execution exceptions (such as task hangs or repeated failures)

* Claw fails to start normally after configuration adjustment

* The Claw interface can be opened but features are unavailable


If auto healing is ineffective, refer to [Restarting Claw instances](https://docs.byteplus.com/en/docs/ArkClaw/Restart_Claw_instance?lang=en) or [Restore factory settings for Claw instances](https://docs.byteplus.com/en/docs/ArkClaw/Restore_Claw_instance_to_factory_settings?lang=en).

<span id="WmN2TmVZ"></span>
## Procedure


1. Log in to [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Claw Management \> Claw List".

3. Under the "Instances" tab, the list of currently created employee Claw/shared Claw instances is displayed,

4. In the Claw list, click "Auto Healing" in the "Actions" column for the target Claw instance.

5. In the dialog box that appears, click the "Auto Healing" button to complete the operation.

6. After the operation is completed, return to the Claw list page and confirm that the status of the target Claw instance has been restored to "Running". For further confirmation, enter the terminal or observability page of the target Claw to verify whether the features are functioning normally.
