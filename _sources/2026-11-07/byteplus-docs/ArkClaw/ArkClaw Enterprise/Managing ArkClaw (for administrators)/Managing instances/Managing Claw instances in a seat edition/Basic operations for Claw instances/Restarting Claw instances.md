---
title: "Restarting Claw instances"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Restart_Claw_instance"
---

When the administrator needs a Claw instance to load the latest configuration, or when an employee's Claw instance experiences slow responses, task freezes, or other exceptions, the administrator can manually restart the target Claw instance. **This article describes how to perform the restart operation from the Claw list.** 

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">During the restart of the Claw instance, the instance is temporarily unavailable (expected to take about 1 minute). Please perform the operation when employees are idle.</div>


* <div data-tips="true" data-tips-type="warning">Running tasks and sessions are interrupted and cannot be restored. Notify relevant employees in advance.</div>


* <div data-tips="true" data-tips-type="warning">After the restart is completed, the Claw instance automatically loads the latest configuration.</div>



<span id="ro106bsp"></span>
## Operation scenarios


* To apply Claw instance configuration updates: restart the Claw instance.

* If the Claw instance responds slowly or occasionally encounters exceptions: first try to restart; if the restart is ineffective, try [auto healing](https://docs.byteplus.com/en/docs/ArkClaw/Auto_healing_for_Claw_instances?lang=en).

* If the Claw instance crashes and both auto healing and restart are ineffective: [restore factory settings](https://docs.byteplus.com/en/docs/ArkClaw/Restore_Claw_instance_to_factory_settings?lang=en) (this clears data).


<span id="VDHufUSS"></span>
## Procedure


1. Log in to [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, choose "Claw management \> Claw list".

3. The "Instances" tab displays the list of currently created employee Claw and shared Claw instances.

4. In the Claw instance list, click the "More \> Restart" button in the "Actions" column for the target Claw instance.

5. In the dialog box that appears, click the "Restart" button to complete the operation.

6. After the operation is completed, return to the Claw list page and confirm that the target Claw instance status has returned to "Running"; this indicates the restart was successful.
