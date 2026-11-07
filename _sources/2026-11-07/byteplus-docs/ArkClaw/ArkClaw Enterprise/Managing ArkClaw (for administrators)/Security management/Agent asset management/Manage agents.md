---
title: "Manage agents"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Manage_agents"
---

Assistant management helps you centrally manage and protect all connected assistants (such as ArkClaw or Claw deployed in other third\-party environments). You can view the operating status and security risks of each assistant, configure protection policies for them, and ensure the secure operation of assistants within the enterprise.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To manage both ArkClaw assistants and third\-party Claw assistants simultaneously, contact your business representative to add your account to the allowlist.</div>


<span id="230aVEiT"></span>
## Key features


* **Automated asset discovery**:

   * Assistants with the ClawSentry plugin installed and service registration completed can be automatically discovered and synchronized to the asset list, simplifying the management process.

   * ArkClaw assistants can be automatically discovered and synchronized to the asset list without manual registration.

* **Real\-time status monitoring**: Display the online/offline status and security status of assistants to quickly identify anomalies.

* **Protection policy configuration**: Support configuring protection policies for one or more assistants, including prompt injection protection, sensitive data disclosure prevention, and high\-risk behavior control.

* **Enable protection on demand**: Use the "Enable Protection" switch to activate the purchased protection quota for specified assistants and control costs as needed.

* **Protection version switching**: Support switching the protection version for different assistants and configuring protection capabilities according to business scenarios and security requirements.


<span id="VNdXonEu"></span>
## Typical scenarios


* **Unified asset inventory**: Quickly understand the number, distribution, and basic information of all assistants within the enterprise.

* **Routine security inspection**: Regularly check the security status of assistants to promptly identify and handle risky assistants.

* **Attack incident response**: In the event of a security incident, locate affected assistants, view related events, and adjust protection policies.

* **Compliance policy implementation**: Configure protection policies for assistants in different business scenarios according to enterprise data security and behavioral compliance requirements.


<span id="Gc8dIIgj"></span>
## Prerequisites

You have connected the assistants to the ClawSentry service. For connection methods, refer to [Enable security protection](https://docs.byteplus.com/en/docs/ArkClaw/Enable_security_protection?lang=en).

<span id="p2bcUqws"></span>
## Procedure


1. Log in to the [ArkClaw Enterprise Edition Console](https://console.byteplus.com/arkclaw/enterprise).

2. Select **Security Management** from the menu on the left.

3. View information about assistants that have already been connected in the **Assistant Security** list.

   
   |**Field** |**Description** |
   |---|---|
   |**Agent name/ID** |The name and unique identifier of the assistant. If not set during input, there is no information. |
   |**Associated user** |Information about users who use this assistant, such as account name, email, and so on. If not set during input, there is no information. |
   |**Skills** |The list of skills installed for this assistant is automatically scanned and identified by ClawSentry. |
   |**Security plugin status** |Displays the running status of the security plugin. The system continuously collects the heartbeat of the ClawSentry plugin on the endpoint. The following situations may cause the plugin to go offline:<br><br><br>* Network is unreachable<br><br>* Plugin is disabled<br><br>* Plugin is uninstalled |
   |**Enable protection**<br><br>  |The current protection enabled status for the assistant. Each assistant with protection enabled occupies one protection seat. Disabling protection releases the seat.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the assistant's security plugin is offline, protection cannot be enabled or disabled.</div><br> |
   |**Protection version** |The protection version (Standard or Advanced) for the current assistant can be switched manually.<br><br>When an assistant is connected, protection is enabled by default, with Standard protection enabled as the default.<br><br>For differences between versions, see [ClawSentry Billing Information](https://docs.byteplus.com/en/docs/ClawSentry/ClawSentry_billing_details?lang=en). |
   |**Actions** |* **More \> Change Protection Version**: Switch the protection version for the current assistant. Before switching, ensure that there are available seats for the target version. You can free up seats by purchasing additional seats or disabling the assistant's protection status.<br><br>* **More \> Remove**: Remove assistants that are no longer in use from the asset list. Before removal, ensure that the security plugin has been uninstalled. |
   

4. Click the name of any assistant to enter the assistant details page and view the following information:

   * **Basic Information**: Assistant name/ID, user, skills, plugin version, security status, update time, and more.

   * **Skill List**: Skill information, status (secure/risky), scan time
