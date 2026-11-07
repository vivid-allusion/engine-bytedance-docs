---
title: "Managing terminal command permissions"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring_local_command_approval_rules"
---

Command permissions control how terminal commands are processed before local execution. You can configure command permission modes separately for the **global default workspace** and for **each project**. Projects without a separate configuration inherit the global default configuration.

ArkClaw currently supports three modes: **request approval**, **intelligent approval, and full access**. The system also provides built\-in security rules that are enabled by default. These rules identify high\-risk commands and intercept them, request confirmation, or display reminders before command execution.

## Permission evaluation process

When ArkClaw processes a command, it first checks whether the command matches a built\-in security rule, and then checks whether the project has a separate command permission configuration. This process determines whether the command runs directly, requires confirmation, only triggers a reminder, or is denied.

## Command permission modes

Command permission modes define approval policies for regular commands. When you select a mode, we recommend prioritizing two aspects: business risk and automation level. The higher the risk, the more appropriate it is to keep confirmation. The more stable the process, the more suitable custom rules are for automatic processing.

|**Permission mode** |**Confirm before command execution** |**File and network access** |**Application scenarios** |
|---|---|---|---|
|Request approval |Confirmation is required before command execution by default. Confirmation can be skipped if an allow rule is matched. |Depends on rules and approval results |Suitable for scenarios such as initial project integration, unstable permission boundaries, or the need to confirm the impact of each command individually. |
|Intelligent approval |Automatically identifies high\-risk commands and requests approval only when necessary. |Depends on rules and risk assessment results |Suitable for daily development and debugging scenarios, balancing operational efficiency and risk control. |
|Full access |Commands are run directly by default and usually do not require confirmation. |File and network access are unrestricted |Suitable for short\-term, controllable, and trusted batch operations, such as repeated builds, batch reading of project files, or verified automated tasks. |

## Built\-in security rules

Built\-in security rules are ArkClaw's preset global protection capabilities. They are enabled by default and apply to all tasks on the current device. You can adjust how rules are processed based on business needs, but you cannot delete built\-in rules.

If a command matches both a built\-in security rule and a command permission mode, ArkClaw processes the command based on the built\-in security rule first. This design prevents high\-risk commands from running directly when project\-level or global configurations are too permissive.

### Built\-in rule processing methods

Built\-in rules support the following processing methods:

* **Deny**: Commands that match the rule are blocked directly and are not run.

* **Require confirmation**: Commands that match the rule require user confirmation before they are run.

* **Remind**: Commands that match the rule can continue to run, but ArkClaw displays a risk reminder in the conversation.

### Built\-in rule types

Built\-in rules currently include, but are not limited to, the following types:

|**Rule type** |**Description** |
|---|---|
|File deletion and system damage |Identifies high\-risk commands that may cause data loss, disk wiping, or system damage. |
|System shutdown and control |Identifies commands that may shut down or restart the device or interrupt your current work. |
|Privilege escalation and account management |Identifies highly sensitive commands such as privilege escalation, account creation, and account switching. |
|Remote download and execution |Identifies commands that download remote content and execute it directly, reducing the risk of malicious scripts landing on the device. |
|Reverse connections and remote control |Identifies commands that may establish reverse connections or remote control. |
|Network scanning and exposure to the public network |Identifies high\-risk commands such as port scanning, network probing, and tunnel exposure. |
|Auto\-start on boot and persistence |Identifies commands that set auto\-start on boot or long\-term persistence and that may change the device's operating status. |
|Disabling security protection |Identifies commands that disable the firewall or system security protection capabilities. |
|Credential reading |Identifies commands that read keys, credentials, or sensitive system information and provides risk reminders. |

## Prerequisites

[the local device is authorized](https://docs.byteplus.com/en/docs/ArkClaw/Installing_and_using_the_client#ZJ0j4Jsu).

## Switch the permission mode for ArkClaw to execute terminal commands on your local device

When executing terminal commands locally, ArkClaw supports flexible permission control through **command approval modes**. You can choose to confirm each execution manually, grant full access directly, or automatically execute commands based on preset rules, meeting different security and efficiency requirements.

1. Log in to the ArkClaw client locally.

2. Switch to the target ArkClaw.

3. Enter the main session or project session interface.

4. At the bottom of the chat box, click the "Request approval mode" button, and select the required permission mode from the drop\-down list.

## Manage command approval rules

### Add a rule

1. Log in to the ArkClaw client locally.

2. Switch to the target ArkClaw.

3. Enter the main session or project session interface.

4. At the bottom of the chat box, click the "Request approval mode \> ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_282663c0fedd47ce87f1ce9b5283abff.png)".

5. In the "**Command approval rules**" section, click the "+ Add rule" button.

6. In the "Add rule" dialog box that appears, configure the following parameters.

   |Parameter​ |Description |
   |---|---|
   |Decision |Select an approval policy. Values:<br><br><br>* **Deny**: After a command matches a rule, it is blocked directly before execution.<br><br>* **Require confirmation**: The user needs to confirm each command before it can run. However, in **full access** mode, no confirmation is required, and the command is allowed to run directly.<br><br>* **Remind**: The command runs, and a notice is displayed in the conversation to indicate that the command has matched the rule.<br><br>* **Allow**: After a command matches a rule, it runs directly without approval. |
   |Command prefix |Enter the command prefix to match. Separate multiple tokens with spaces, and use `\|` to separate options. Example: `git status\|log`. |
   |Test effect (optional) |Enter a command in the "**Test effect**" input box and click "Test" to verify whether the rule will block the command before saving. |

7. Click the "Add" button to complete the rule configuration.

### Update a rule

1. In the "**Command approval rules**" section, locate the rule you want to edit and click the "Edit" button on the right side of the rule row.

2. In the dialog box that appears, modify the "**Decision**" or "**Command prefix**" parameters.

3. (Optional) In the "**Test effect**" input box, enter a command and click "Test" to verify the effect of the updated rule.

4. Click the "Save" button to complete the edit.

### Delete a rule

> **tip**

> Deleted rules cannot be recovered. Make sure that a rule is no longer needed before deleting it.

In the "**Command approval rules**" section, locate the rule you want to delete and click the "Delete" button on the right side of the rule row.

### Export and import rules

With configuration backup and migration, you can export built\-in rules, custom rules, permission levels, and writable directories as configuration files, and import them to other devices or environments.
