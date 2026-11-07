---
title: "Viewing the configuration modification records for an ArkClaw instance"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Viewing_the_configuration_modification_records_for_an_ArkClaw_instance"
---

ArkClaw Enterprise provides configuration modification records for each ArkClaw instance. This allows you to view the modification records of the `openclaw.json` configuration file for ArkClaw instances. This ensures that configuration operations can be audited and traced, meets compliance management requirements, and helps maintain stable system operation. This topic describes how to view the configuration change records for an ArkClaw instance as an administrator.

<span id="nhFbTOZi"></span>
## Background

`openclaw.json` is the core configuration file of the OpenClaw system. It is primarily used to store global settings and manage key modules such as gateway ports, model integration, communication channels, and security policies. It determines system runtime behavior and capability boundaries. Modifying the configurations of `openclaw.json` has a significant impact and may pose risks, such as service interruptions due to invalid configurations, changes in functional behavior, impacts on security policies, and configuration compatibility risks during cross‑version updates.

<span id="xhR5wzS6"></span>
## Prerequisites


* The administrator has completed basic settings (such as enterprise system permissions and callback configuration) and has activated ArkClaw Enterprise. For details, see [ArkClaw management for administrators](https://docs.byteplus.com/en/docs/ArkClaw/Administrator_opens_ArkClaw).

* Enterprise employees have provisioned ArkClaw instances and initiated conversations with them for task processing. For details, see [ArkClaw guide for employees](https://docs.byteplus.com/en/docs/ArkClaw/Employees_use_ArkClaw).


<span id="NUudmYWu"></span>
## Limits

Make sure that the version of the `o11yagent_openclaw` plugin for the current ArkClaw instance is not earlier than v0.0.6.


* Go to the instance terminal page and run the `o11yagentctl ps` command to view the O11yAgent plugin version.

* If the instance version does not meet your requirements, you can upgrade the instance to the latest version. For upgrade instructions, see [Upgrading multiple ArkClaw instances at a time](https://docs.byteplus.com/en/docs/ArkClaw/Upgrading_multiple_ArkClaw_instances_at_a_time).


<span id="zV9GKUee"></span>
## Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click **Claws** to go to the ArkClaw instance management list.

3. Find the target ArkClaw instance and click **More \> Configuration change records** in the Actions column. Then, you'll be redirected to the **Configuration change** tab of the details page for the ArkClaw instance.

4. Select a time range as needed to view the configuration change records within the specified period of time. The records include details such as operation time, event name, resource ID, user ID, and user email address.

5. Click **Configuration details** in the “Actions” column that corresponds to a configuration change record to view the added and deleted entries in the `openclaw.json` configuration file.
