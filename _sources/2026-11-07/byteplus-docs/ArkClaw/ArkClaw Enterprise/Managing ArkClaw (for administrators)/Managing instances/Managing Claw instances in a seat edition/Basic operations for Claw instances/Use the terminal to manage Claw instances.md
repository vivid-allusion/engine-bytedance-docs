---
title: "Use the terminal to manage Claw instances"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Use_the_terminal_to_manage_Claw_instances"
---

Administrators can use the terminal to enter an employee's Claw environment and use Shell commands to complete various O&M actions, such as creating tasks, configuring skills, and more. **This document describes how to enter the terminal page of a target instance from the Claw list and execute commands.** 

<span id="pEtaxqY0"></span>
## Scenario

When it is necessary to perform O&M actions that are not directly supported by the console interface, such as debugging Claw scripts, troubleshooting logs, or manually installing or upgrading OpenClaw components, administrators can use the terminal to enter the employee's Claw Shell environment and perform operations.

<span id="OeBbCnE3"></span>
## Operation instruction


* Shell commands executed through the terminal directly affect the target employee's Claw instance environment. **Before performing operations, confirm that no critical tasks are running on the target Claw to avoid interruption.** 

* Terminal actions cannot be undone. It is recommended to use the backup feature to save the current status of the instance before making any changes.

* All terminal operations are recorded in the audit logs and can be traced through [audit logs](https://docs.byteplus.com/en/docs/ArkClaw/View_Claw_instance_observational_data?lang=en).


<span id="Z7OkXbpN"></span>
## Procedure


1. Log in to the [ArkClaw Enterprise console ](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Claw management \> Claw list".

3. Under the "Instances" tab, the list of currently created employee Claw/shared Claw instances is displayed.

4. In the Claw instance list, click "More \> Terminal" in the "Actions" column of the target Claw instance.

5. On the terminal page, enter the specified command and execute it to complete the corresponding action.

   For example, execute the `openclaw -v` command to view the current OpenClaw version.
