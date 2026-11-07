---
title: "Enabling/Disabling ArkClaw plugins"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Enabling_and_Disabling_ArkClaw_plugins"
---

ArkClaw plugins are feature extension components provided by BytePlus official teams and third\-party developers. By managing these plugins, you can enable or disable custom capabilities for your ArkClaw instance. For example, enabling plugins for collaboration platforms such as WeCom and Feishu allows you to quickly implement cross\-platform message push, intelligent Q&A, workflow automation, and other capabilities.

This topic describes how to enable and disable ArkClaw plugins to flexibly control their functional scope.


* **Enable a plugin**

   After you enable a plugin, ArkClaw can invoke the corresponding plugin capabilities during conversations and provide extended services based on the plugin features.

   For example: After "Feishu IM" is enabled, ArkClaw can provide message notification, intelligent Q&A, and other capabilities via Feishu. Users can access and use the current agent from Feishu.

* **Disable a plugin**

   After you disable a plugin, ArkClaw will no longer invoke the plugin during conversations.

   For example: After "Feishu IM" is disabled, ArkClaw will stop providing message notification, intelligent Q&A, and other capabilities via Feishu, and users will no longer be able to access or use the current agent from Feishu.


<span id="lYwtCA40"></span>
## Plugin types


|Plugin type |Description |
|---|---|
|Official plugin |Plugins of this type are independently developed by BytePlus and can be enabled or disabled as needed. |
|Built\-in plugin |Functional plugins of this type are pre\-configured on the ArkClaw platform and can be enabled or disabled as needed. |
|System\-required plugin |Plugins of this type are fundamental to the stable operation of ArkClaw. They are enabled by default and **cannot be disabled**, and the information on the page is for display purposes only. |


<span id="ut1cKjR5"></span>
## Procedure


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw and click the details icon at the top.

3. Select the "Plugins \> Plugins" tab.

4. In the row of the target plugin, enable or disable the plugin as needed **.** 

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After you enable or disable the plugin, the related service will automatically restart. Please wait.   </div>
   

   * **Enable**: Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f889125e37b4cdf7fdd83f18358ba5d1.png) </span> icon to enable the plugin.

   * **Disable**

      1. Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_10046997799e004b7e9761917eb8622c.png) </span>.

      2. After confirming that the plugin to be disabled is correct, click the "Confirm" button to complete the operation.


<span id="gD55URlY"></span>
## Other operations


|Feature |Description |
|---|---|
|View plugin type |You can view the corresponding plugin type below each plugin. |
|Filter plugins by type |By default, all plugins are displayed. You can quickly filter plugins by type, which is suitable for viewing plugins of the same type in bulk.<br><br>In the upper\-right corner of the page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_234c81df05b44dff563106456f84bb47.png) </span> icon. Then, select "Official plugin", "Built\-in plugin", or "System\-required plugin" as needed to filter plugins. |
|Search for and locate a plugin |Use the search feature to quickly locate the target plugin.<br><br><br>1. In the upper\-right corner of the page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d70b2240d4e78156a7ca1f12baeddeab.png) </span>icon.<br><br>2. Enter the plugin name or a keyword in the search box to quickly locate the target plugin. |
