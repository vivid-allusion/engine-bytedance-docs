---
title: "Enabling or disabling private access to apps"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Enabling_or_disabling_private_access_to_apps"
---

<span id="g399hIfQ"></span>
## Scenarios

ArkClaw Enterprise's private network egress enables private app access. It allows ArkClaw to reach enterprise AI assets registered in Application Center over the private network, such as Agents and MCP (Method, Capability, Plugin). This helps employees discover, invoke, and manage AI assets securely and efficiently via ArkClaw.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If you are unable to use this feature, go to <a href="https://console.byteplus.com/arkclaw/enterprise">the ArkClaw Enterprise console</a> to find your Space ID, and <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to upgrade the Space.</div>



* <div data-tips="true" data-tips-type="default">Before the upgrade is complete, private network addresses for enterprise Agents and MCPs from the "Custom" source in Application Center are temporarily inaccessible. Agents and MCPs from "AgentKit" and "Shared Claw" are not affected.</div>


* <div data-tips="true" data-tips-type="default">After the upgrade, the "Configure private access to apps" toggle is enabled by default. You do not need to manually configure it as this topic described. ArkClaw can access registered enterprise AI assets (Agents, MCPs, etc.) in Application Center over the private network.</div>



<span id="W7m2ZVGU"></span>
## Before you begin


* The private apps to be accessed have been registered in ArkClaw Application Center. If not, see [Registering an app](https://docs.byteplus.com/en/docs/ArkClaw/Application_management).

* The private network egress is enabled. If not, see [Enabling private network egress](https://docs.byteplus.com/en/docs/ArkClaw/Enabling-or-disabling-the-private-egress-New-version).


<span id="u80DrwCh"></span>
## Procedure


1. Log in to [the ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space Egress" tab, select the "Private network egress" tab, then click "Edit" to the right of Configuration.

4. On the private network egress page, check "Specify the target IP address range for access" to ensure the accessible app addresses fall within this range.

5. Toggle "Configure private access to apps" on or off

   * **On**: ArkClaw can access private IP addresses (such as private domains or private IPs) configured in the Application Center over the private network.

   * **Off**: ArkClaw does not access the private IP address configured in Application Center over the private network. Access may fail if an app provides only private IP addresses.

6. Click "OK" to complete the action.
