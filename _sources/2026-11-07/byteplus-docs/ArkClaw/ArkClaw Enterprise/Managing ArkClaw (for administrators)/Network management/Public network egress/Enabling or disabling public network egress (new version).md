---
title: "Enabling or disabling public network egress (new version)"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Enabling-or-disabling-public-network-egress-new"
---

Public Network Egress is enabled by default​ after the ArkClaw Enterprise service is enabled. To mitigate security risks associated with data traversing the public network, enterprises can disable the public egress. This topic introduces how to manage the public network egress and its basic configuration.

<span id="K2Ffy8LV"></span>
## Before you begin

The public and private network egresses cannot both be disabled. Before disabling the public network egress, ensure the private network egress is enabled. For procedure, see [Configuring private network egress](https://docs.byteplus.com/en/docs/ArkClaw/Enabling-or-disabling-the-private-egress-New-version).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In scenarios where the Virtual Private Cloud (VPC) hosting your enterprise services is connected to the ArkClaw VPC via Transit Router (TR) or Cloud Enterprise Network (CEN), the public network egress is enabled by default​ and the private network egress cannot be enabled. However, you can still disable the public network egress in this case.</div>


<span id="2AtfU3td"></span>
## Enable or disable public network egress


1. Log in to the [ArkClaw Enterprise Edition console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space Egress" tab.

4. In the "Public network egress" section, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b4801ed68f363d255f8acaecb67192fa.png) </span>icon to the right of Configuration.

5. In the pop\-up dialog box, turn on or off the public network egress toggle.

6. Click "OK" to complete the action.
