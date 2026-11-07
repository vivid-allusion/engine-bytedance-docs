---
title: "Managing custom plugins"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Managing_custom_plugins"
---

After you create and install a custom plugin, you can manage its lifecycle as your business evolves. This topic describes how to create a version of, change the version of, disable, delete, and uninstall custom plugins in the APIG console.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><strong>[Beta · apply for trial]</strong>: This feature is currently in Beta. To use this feature, contact your account manager.</div>


<span id="bF6BftgD"></span>
## Create a new plugin version

After the plugin feature iteration, you can add a new version for the plugin. The new version coexists with previous versions, allowing you to switch between versions or roll back to a previous version.


1. Log in to the [APIG console](https://console.byteplus.com/veapig).

2. Select the target region in the top navigation bar.

3. In the left navigation pane, select the target instance from the **Instance management ** drop\-down list. Then, click **Plugin Center**.

4. In the "**Custom plugin**" section under "Plugin category", click `...` **\> Create version** of the target plugin card, configure the following information for the new version, and click **Confirm.** 

   * **Lua script**: In the script editor, upload a new Lua script to configure the new logic that takes effect.

   * **WASM file**: Upload a compiled .wasm file that contains the plugin logic to be executed in the gateway.

   * **Version:**  Enter a new version number for the plugin. The version number must be different from any existing version number. For example, 1.0.1.

   * **Version description**: Briefly describe the features or changes of this version, for example, added rate limiting.


<span id="IqBOvFMM"></span>
## Change the plugin version

When a custom plugin has multiple versions, you can switch to a specific version for objects that have the plugin installed to upgrade or roll back the version.


1. Log in to the [APIG console](https://console.byteplus.com/veapig).

2. Select the target region in the top navigation bar.

3. In the left navigation pane, select the target instance from the **Instance management ** drop\-down list. Then, click **Plugin Center**.

4. In the "Custom plugin" section under "Plugin category", click the target plugin card, and click **Change version.** 

5. In the pop\-up **Change version** dialog box, select the version you want to change to, and then click **Confirm**.


<span id="Esu3llUL"></span>
## Disable a plugin

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After a plugin is disabled, the plugin rules that you configured no longer take effect on your services. Proceed with caution.</div>



1. Log in to the [APIG console](https://console.byteplus.com/veapig).

2. Select the target region in the top navigation bar.

3. In the left navigation pane, select the target instance from the **Instance management ** drop\-down list. Then, click **Plugin Center**.

4. In the "Custom plugin" section under "Plugin category", select the target plugin card, and click **Disable** in the Actions column on the right of the target plugin.

5. In the pop\-up dialog box, click **Confirm**.


<span id="thK7uZCe"></span>
## Delete a plugin

Deleting a plugin means deleting the plugin rules on a specific object, such as an instance, service, or route. After a rule is deleted, the traffic that matches the rule is no longer processed by the plugin. After all rules of a plugin are deleted, the plugin no longer takes effect on any traffic.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Before you delete a plugin, you must disable it first. Only disabled plugins can be deleted. For details, see <a href="https://docs.byteplus.com/en/docs/apig/Managing_custom_plugins?lang=en#Esu3llUL">Disable a plugin</a>.</div>



1. Log in to the [APIG console](https://console.byteplus.com/veapig).

2. Select the target region in the top navigation bar.

3. In the left navigation pane, select the target instance from the **Instance management ** drop\-down list. Then, click **Plugin Center**.

4. In the "Custom plugin" section under "Plugin category", select the target plugin card, and click **Delete** in the Actions column on the right of the target plugin.

5. In the pop\-up dialog box, click **Confirm**.


<span id="PTFUTIOb"></span>
## Uninstall a plugin

When you no longer need a custom plugin, you can delete it in Plugin Center.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Before you delete a plugin, delete all its rules. For details, see <a href="https://docs.byteplus.com/en/docs/apig/Managing_custom_plugins?lang=en#thK7uZCe">Delete a plugin</a>.</div>



1. Log in to the [APIG console](https://console.byteplus.com/veapig).

2. Select the target region in the top navigation bar.

3. In the left navigation pane, select the target instance from the **Instance management ** drop\-down list. Then, click **Plugin Center**.

4. In the "Custom plugin" section under "Plugin category", click `...` **\> Delete** of the target plugin card.

5. In the pop\-up dialog box, click **Delete**.
