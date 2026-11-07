---
title: "Configuring A2A endpoints for Claw instances"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring_A2A_endpoints_for_Claw_instances"
---

This topic describes how an administrator can enable the A2A endpoint capability for Claw instances. Once enabled, Claw instances can be integrated with internal enterprise IM, OA, CRM, and other systems through A2A. An A2A client can also call the agent to automatically generate the endpoint URL and API key.

<span id="gnY7HnDh"></span>
## Prerequisites

The current space has enabled the A2A global configuration switch. For details, see [Claw instance global configuration](https://docs.byteplus.com/en/docs/ArkClaw/Global_settings_for_Claw_instances).

<span id="AS6aC3en"></span>
## Enable the A2A endpoint switch


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise)[ArkClaw Group console](https://console.byteplus.com/arkclaw/enterprise/group/).

2. In the left\-side navigation pane, select "Claw Management \> Claw List".

3. On the "Employee Claw" or "Shared Claw" tab, configure the A2A endpoint switch for the Claw instance.

   * **Single operation**:

      1. Click "More" in the "Actions" column of the target Claw instance. In the drop\-down box, switch on "A2A endpoint".

      2. In the dialog box that pops up, click the "OK" button to complete the configuration.

   * **Bulk operation**:

      1. Select multiple target Claw instances in the list, then click the "..." button at the bottom of the list, and click the "Enable/Disable A2A endpoint" button in the dropdown menu.

      2. In the dialog box that pops up, select "Enable in bulk", confirm that everything is correct, then click the "OK to enable" button to complete the operation.

         * Under the "Enableable instances" tab, view the Claw instances for which you need to enable A2A endpoints.

         * Under the "Enabled instances" tab, view the Claw instances in the current space that have enabled the A2A endpoint.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Once configured, you can adjust the enable/disable status of the A2A endpoint at any time as needed for subsequent management.   </div>
   

<span id="30pFQg6P"></span>
## View A2A endpoint status and endpoint information


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise)[ArkClaw Group console](https://console.byteplus.com/arkclaw/enterprise/group/).

2. In the left\-side navigation pane, select "Claw management \> Claw list".

3. Under the "employee Claw" tab, click the target instance name, and view it in the "Configuration information" tab's "Basic information" area.
