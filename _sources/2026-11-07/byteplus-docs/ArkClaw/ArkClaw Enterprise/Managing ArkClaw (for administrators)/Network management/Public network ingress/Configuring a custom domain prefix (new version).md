---
title: "Configuring a custom domain prefix (new version)"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/configuring-a-custom-domain-prefix-new-version"
---

This topic describes how to configure a custom domain prefix for the ArkClaw public network ingress, enabling concise and memorable access addresses based on the platform\-provided domain, thereby improving the employee login experience.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="default">If you are unable to use the new version of network configuration, go to <a href="https://console.byteplus.com/arkclaw/enterprise">the ArkClaw Enterprise console</a> to find your Space ID, and <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to upgrade the Space.</div>


<span id="rxnwb6zp"></span>
## **Use limits**


* Only administrators of the enterprise space can configure this feature.

* The domain prefix must be globally unique across the entire platform and cannot be reused.

* Only customizing the domain prefix is supported. The domain suffix is uniformly provided by the platform (`arkclaw-enterprise-<region>.volceapi.com`). Binding your enterprise domain is not yet supported.


<span id="rJmBlflY"></span>
## Procedures


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise?_vtm_=a78999.b69280.0_0.0_0.0.49_7646310380663539205) with an administrator account.

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space Ingress" tab.

4. In the "Public network ingress" section, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b4801ed68f363d255f8acaecb67192fa.png) </span>icon to the right of "Custom domain prefix".

5. On the "Edit custom domain prefix" page, configure the following settings.

   
   |Configuration item |Description |
   |---|---|
   |Configure custom domain prefix |Click the "Configure custom domain prefix" toggle to set it to "Enabled".<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f2b18ea6e2715f27794c1cb71f6f7256.webp) </span> |
   |Custom domain prefix |In the input filed, enter your desired domain prefix.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Domain prefix naming rules:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Only supports English letters (a\-z, A\-Z) (case\-insensitive), digits (0\-9) and hyphens (\-).</div><br><br><br>* <div data-tips="true" data-tips-type="default">Must start and end with a letter or digit. Cannot start or end with a hyphen (\-).</div><br><br><br>* <div data-tips="true" data-tips-type="default">Must be between 1 and 63 characters.</div><br> |
   

&nbsp;

6. After configuration, click "OK" in the bottom\-right corner.

   You can view the current domain prefix and the full login address in the "Custom domain prefix" field.

   ## <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f80bac673ecabdabadd5050062f69fcf.webp) </span>    <span id="r5b1qSF3"></span>


<span id="EsKUBtXk"></span>
## Manage a custom domain prefix

<span id="0HWnhpWI"></span>
### Update a custom domain prefix

If you have configured a custom domain prefix, follow these steps to modify the existing one.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise?_vtm_=a78999.b69280.0_0.0_0.0.49_7646310380663539205) with an administrator account.

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space Ingress" tab.

4. In the "Public network ingress" section, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b4801ed68f363d255f8acaecb67192fa.png) </span>icon to the right of "Custom domain prefix".

5. In the "Custom domain prefix" input filed, enter your desired domain prefix.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Domain prefix naming rules:   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Only supports English letters (a\-z, A\-Z) (case\-insensitive), digits (0\-9) and hyphens (\-).   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Must start and end with a letter or digit. Cannot start or end with a hyphen (\-).   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Must be between 1 and 63 characters.   </div>
   

6. After configuration, click "OK".

   You can view the updated domain prefix and the full login address in the "Custom domain prefix" field:

   ## <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f80bac673ecabdabadd5050062f69fcf.webp) </span>    <span id="QjV11V8f"></span>


<span id="gqomddLw"></span>
### Delete a custom domain prefix

If you have configured a custom domain prefix, follow these steps to delete the existing one.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise?_vtm_=a78999.b69280.0_0.0_0.0.49_7646310380663539205) with an administrator account.

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space Ingress" tab.

4. In the "Public network ingress" section, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b4801ed68f363d255f8acaecb67192fa.png) </span>icon to the right of "Custom domain prefix".

5. On the "Edit custom domain prefix" page, click the "Configure custom domain prefix" toggle to set it to "Disabled", then click "OK".

   After successful action, you can delete the configured custom domain prefix.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5635d8c8503ca1b3120bb041085c5784.webp) </span>


&nbsp;

&nbsp;

&nbsp;

<span id="gyybyqqu"></span>
##
