---
title: "Claw instance global configuration"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Global_settings_for_Claw_instances"
---

ArkClaw supports global configuration operations for Claw instances. Administrators can configure settings (such as data backup policies and data masking) globally with a few clicks. This article introduces the effective policy of global configuration and guides the administrator to uniformly set the default backup time and default masking policy for newly created Claw instances.

<span id="0zidw3RS"></span>
## Application scenarios

To **uniformly set the default backup time for newly created instances** or **uniformly set the observability data masking level** and other space\-wide global configurations, thereby reducing the cost of manually configuring each instance, global configuration can be used. Recommendation: If the enterprise only wants to set differentiated configurations for a small number of instances, it is recommended to configure them individually at the instance level (instance\-level configuration takes precedence).

<span id="Digx1BRv"></span>
### Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise)[ArkClaw Group console](https://console.byteplus.com/arkclaw/enterprise/group/).

2. In the left\-side navigation pane, select "Claw Management \> Claw list".

3. Click "Global Configuration" in the upper\-right corner.

4. Configure the global policy.

   
   |Configuration item |Description of configuration |
   |---|---|
   |**Backup and update** |* Control the time and interval for automatic backup of instance data.<br><br>* For detailed actions and description, refer to [Backup/restore ArkClaw instance data](https://docs.byteplus.com/en/docs/ArkClaw/Backing_up_and_restoring_ArkClaw_instances) under the "Configure the initial automatic backup time for Claw instance" tab.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>The global configuration for backup and update only takes effect for newly created employee Claw instances and shared Claw instances created after the configuration is applied. Existing Claw instances are not affected by this configuration</strong>, and the original configuration remains effective.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After the global configuration takes effect, if the configuration (backup time, data masking policy) of a specified Claw instance is modified individually, the result of the individual modification takes precedence, and the Claw instance is no longer affected by the global configuration. Example: The global backup time is set to 02:00. If instance A is later individually changed to 04:00, instance A will remain at 04:00 and will no longer change with the global configuration.</div><br> |
   |**Data masking** |* The rules for masking sensitive information in instance runtime or observability data.<br><br>* For detailed actions and descriptions, please refer to the [observability data masking](https://docs.byteplus.com/en/docs/ArkClaw/Masking_observability_data) tab "Global settings for observability data masking policy".<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>Global configuration for data masking only takes effect for employee Claw instances and shared Claw instances created after configuration. Existing Claw instances are not affected by this configuration</strong>, and the original configuration remains effective.</div><br> |
   |**Integration invocation** |* Control the enablement or disablement of A2A endpoint capability under the current ArkClaw space.<br><br>* Click the toggle next to "**A2A endpoint**" to enable or disable the A2A endpoint capability for the current space as needed.<br><br>   * **Enable (default)** : After enabling this switch, the current space supports A2A endpoint capability. Claw instances under the space can enable A2A endpoint capability and integrate with internal IM, OA, CRM, and many other systems via A2A, or the A2A client can actively invoke the agent to automatically generate the endpoint URL and API key.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Enabling the global configuration A2A capability switch only means the current space supports A2A endpoint capability. If Claw instances need to use A2A capability, the A2A endpoint switch must also be enabled individually for each Claw instance.      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2"><strong>Enable in the admin console</strong>: For details, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Configuring_A2A_endpoints_for_Claw_instances">Configuring A2A endpoints for Claw instances</a>.      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2"><strong>Enable in the employee console</strong>: For details, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Setting_Webhook">Configuring Webhooks</a>.      </div><br>      <br><br>   * **Disable**: If you disable the switch, the current space does not support the A2A endpoint capability. Claw instances in this space cannot have the A2A endpoint switch enabled and cannot use the A2A capability for integration with internal IM, OA, CRM, and other systems. |
