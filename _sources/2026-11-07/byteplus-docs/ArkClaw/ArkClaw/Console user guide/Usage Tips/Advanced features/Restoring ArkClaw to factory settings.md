---
title: "Restoring ArkClaw to factory settings"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Restoring_ArkClaw_to_factory_settings_and"
---

You can reinitialize the ArkClaw service and reset it to its initial available state when the configuration is corrupted and causes a service crash, or when system failures or abnormal states occur and cannot be recovered.

<span id="nA2jM2oN"></span>
## Procedure


1. Log in to [ArkClaw console](https://console.byteplus.com/arkclaw/), and switch to the target ArkClaw page.

2. In the upper\-right corner of the ArkClaw chat page, click "··· \> Restore factory settings".

3. (Optional) Configure the workspace data retention policy: Before restoring factory settings, you can choose whether to retain the current workspace data based on your actual needs.

   * **To retain the current workspace data**: Check the "**Retain the current workspace and try to restore after a reset**" checkbox. After the factory settings are restored, the system will automatically attempt to restore the original workspace data.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Retention and deletion scopes for workspace data:      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2"><strong>Retained items</strong>: Workspaces in the OpenClaw directory, agent assets, scheduled tasks, team plugins, and all directories and files in the Hermes working directory.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2"><strong>Deleted items</strong>: Extension plugins and OpenClaw system configuration files.      </div>
      

   * **No need to retain the current workspace data (default)** : Leave the checkbox **unchecked**. When the system restores factory settings, all current workspace data will be deleted and cannot be recovered.

4. In the pop\-up window, click "Confirm" to reset the ArkClaw service.
