---
title: "Managing callback configuration"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-a-callback-task"
---

To receive automatic notifications for key live stream events, you can configure callbacks in the BytePlus MediaLive console. This topic provides instructions on how to add, edit, and delete configurations to get notified about streaming, recording, and screenshot events for a specific domain or application.

It may take approximately 3\-5 minutes for the configuration changes to take effect.

<span id="b5ad255d"></span>
## Prerequisite

A callback address to receive callback messages. Both HTTP and HTTPS are supported.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details on callback request reliability and descriptions of the fields in each callback message, see <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-callback-description">Callback description</a>.</div>


<span id="432bb0ac"></span>
## Procedure

<span id="d437fd90"></span>
### **Adding a callback configuration**


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, select **Settings** \> **Feature configuration**. Click the **Callback** tab.

3. Find **Domain name space** at the top of the page and select a domain name space from the drop\-down menu.

4. Click **Add configuration** to open the **Add callback configuration** dialog box.

5. Configure the relevant settings.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/32a38b0f955740dca04be2319f105e36~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Description** |
   |---|---|
   |Callback address |A callback address to receive callback messages. The address must be 1\-100 characters in length. Both HTTP and HTTPS are supported. |
   |Callback type |The type of callback messages to be received.<br><br><br>* **Stream pushing starts**: The callback is triggered when stream pushing starts.<br><br>* **Stream pushing ends**: The callback is triggered when stream pushing ends.<br><br>* **Recording events**: The callback is triggered when a recording event occurs.<br><br>* **Screenshot events**: The callback is triggered when a screenshot\-related event occurs. |
   |Domain name |Select the domain name for which you want to configure callbacks.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Configure this setting if you select <strong>Stream pushing starts</strong> or <strong>Stream pushing ends</strong> as the callback type.</div><br> |
   |AppName |Enter the application name for which you want to configure callbacks.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Configure this setting if you select <strong>Recording events</strong> or <strong>Screenshot events</strong> as the callback type.</div><br> |
   |Applies to transcoded stream |Whether to receive callback messages from transcoded streams.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Configure this setting if you select <strong>Stream pushing starts</strong> or <strong>Stream pushing ends</strong> as the callback type.</div><br> |
   |Callback key |A key used for authentication. By enabling authentication and setting this key, you can use the `sign` and `t` fields in the callback message to verify that the callback originated from BytePlus MediaLive. The key can contain digits and letters and has a maximum length of 32 characters. |
   

6. Click **Confirm** to save the configuration.


<span id="d4712e49"></span>
### Editing a callback configuration

You can click **Edit** in the **Actions** column to update the callback configurations.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Not all settings can be edited after you create a callback configuration. Editable items include:</div>



* <div data-tips="true" data-tips-type="tip">the callback key.</div>


* <div data-tips="true" data-tips-type="tip">whether callbacks for transcoded streams are enabled for the <strong>Stream pushing starts</strong> and <strong>Stream pushing ends</strong> events.</div>



<span id="82e20243"></span>
### Deleting a callback configuration

You can click **Delete** in the **Actions** column to delete a callback configuration.
