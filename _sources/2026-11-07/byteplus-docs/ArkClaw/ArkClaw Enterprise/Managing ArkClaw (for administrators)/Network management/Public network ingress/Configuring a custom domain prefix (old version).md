---
title: "Configuring a custom domain prefix (old version)"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/configuring-a-custom-domain-prefix-old-version"
---

This topic describes how to configure a custom domain prefix for the ArkClaw public network ingress, enabling concise and memorable access addresses based on the platform\-provided domain, thereby improving the employee login experience.

<span id="h7yTNm20"></span>
## **Use limits**


* Only administrators of the enterprise space can configure this feature.

* The domain prefix must be globally unique across the entire platform and cannot be reused.

* Only customizing the domain prefix is supported. The domain suffix is uniformly provided by the platform (`arkclaw-enterprise-<region>.volceapi.com`). Binding your enterprise domain is not yet supported.


<span id="ai8naoFP"></span>
## Procedures


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise?_vtm_=a78999.b69280.0_0.0_0.0.49_7646310380663539205) with an administrator account.

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. On the "Network Configuration" page, locate the "Public network ingress" section and click "Edit".

4. On the "Custom domain for public network ingress" page, locate the "Method 2: Custom domain prefix" section, then configure the following settings.

   
   |Configuration item |Description |
   |---|---|
   |Configure custom domain prefix |Click the "Configure custom domain prefix" toggle to set it to "Enabled". |
   |Custom domain prefix |In the input filed, enter your desired domain prefix.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Domain prefix naming rules:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Only supports English letters (a\-z, A\-Z) (case\-insensitive), digits (0\-9) and hyphens (\-).</div><br><br><br>* <div data-tips="true" data-tips-type="default">Must start and end with a letter or digit. Cannot start or end with a hyphen (\-).</div><br><br><br>* <div data-tips="true" data-tips-type="default">Must be between 1 and 63 characters.</div><br> |
   

&nbsp;

5. After configuration, click "OK" in the bottom\-right corner.

   You can view the current domain prefix and the full login address in the "Custom domain prefix" field.


<span id="RnnnIz1D"></span>
## Manage a custom domain prefix

<span id="nzvzAAuz"></span>
### Update a custom domain prefix

If you have configured a custom domain prefix, follow these steps to modify the existing one.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise?_vtm_=a78999.b69280.0_0.0_0.0.49_7646310380663539205) with an administrator account.

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. On the "Network Configuration" page, locate the "Public network ingress" section and click "Edit".

4. On the "Custom domain for public network ingress" page, locate the "Method 2: Custom domain prefix" section.

5. In the "Custom domain prefix" input filed, enter your desired domain prefix.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Domain prefix naming rules:   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Only supports English letters (a\-z, A\-Z) (case\-insensitive), digits (0\-9) and hyphens (\-).   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Must start and end with a letter or digit. Cannot start or end with a hyphen (\-).   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Must be between 1 and 63 characters.   </div>
   

6. After configuration, click "OK".

   You can view the updated domain prefix and the full login address in the "Custom domain prefix" field.


&nbsp;

<span id="zQIGYJZo"></span>
### Delete a custom domain prefix

If you have configured a custom domain prefix, follow these steps to delete the existing one.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise?_vtm_=a78999.b69280.0_0.0_0.0.49_7646310380663539205) with an administrator account.

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. On the "Network Configuration" page, locate the "Public network ingress" section and click "Edit".

4. On the "Custom domain for public network ingress" page, locate the "Method 2: Custom domain prefix" section.

5. Click the "Configure custom domain prefix" toggle to set it to "Disabled", then click "OK".

   After successful action, you can delete the configured custom domain prefix.


&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

<span id="KKT4vGAf"></span>
##
