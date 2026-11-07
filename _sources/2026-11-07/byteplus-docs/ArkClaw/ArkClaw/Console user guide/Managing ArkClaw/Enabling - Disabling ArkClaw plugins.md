---
title: "Enabling/Disabling ArkClaw plugins"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Enabling_Disabling_ArkClaw_plugins"
---

ArkClaw plugins are feature extension components provided by BytePlus official teams and third\-party developers. By managing these plugins, you can enable or disable custom capabilities for your ArkClaw instance. For example, enabling plugins for collaboration platforms such as WeCom and Feishu allows you to quickly implement cross\-platform message push, intelligent Q&A, workflow automation, and other capabilities.

This topic describes how to enable and disable ArkClaw plugins to flexibly control their functional scope.


* **Enable a plugin**

   After you enable a plugin, ArkClaw can invoke the corresponding plugin capabilities during conversations and provide extended services based on the plugin features.

   For example, after you enable the "wecom\-openclaw\-plugin" WeCom plugin, ArkClaw can deliver capabilities including message push and intelligent Q&A via WeCom. Users can also access and use the current agent via WeCom.

* **Disable a plugin**

   After you disable a plugin, ArkClaw will no longer invoke the plugin during conversations.

   For example, after you disable the "wecom\-openclaw\-plugin" WeCom plugin, ArkClaw will stop providing message push, intelligent Q&A, and other capabilities via WeCom. Users will no longer be able to access and use the current agent via WeCom.


<span id="zpF81b5r"></span>
## Procedure


1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/).

2. Switch to the target ArkClaw page and click the Claw details page icon in the upper\-right corner.

3. Select the "Plugin" tab.

4. In the row of the target plugin, enable or disable the plugin as needed **.** 

   * **Enable**: Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f889125e37b4cdf7fdd83f18358ba5d1.png) </span> icon to enable the plugin.

   * **Disable**: Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_10046997799e004b7e9761917eb8622c.png) </span> icon to disable the plugin.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After you enable or disable the plugin, the related service will automatically restart. Please wait.   </div>
