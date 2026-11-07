---
title: "Enabling or disabling public network egress (old version)"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Enabling-or-disabling-public-network-egress-old"
---

Public Network Egress is enabled by default​ after the ArkClaw Enterprise service is enabled. To mitigate security risks associated with data traversing the public network, enterprises can disable the public network egress. This topic introduces how to manage the public network egress and its basic configuration.

<span id="DHMjS1sU"></span>
## Before you begin

The public and private network egresses cannot both be disabled. Before disabling the public network egress, ensure the private network egress is enabled. For procedure, see [Configuring private network egress](https://docs.byteplus.com/en/docs/ArkClaw/Enabling-or-disabling-the-private-egress-Old-version).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In scenarios where the Virtual Private Cloud (VPC) hosting your enterprise services is connected to the ArkClaw VPC via Transit Router (TR) or Cloud Enterprise Network (CEN), the public network egress is enabled by default​ and the private network egress cannot be enabled. However, you can still disable the public network egress in this case.</div>


<span id="y4QiBOh6"></span>
## Enable or disable public network egress


1. Log in to the [ArkClaw Enterprise Edition console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. In the Space Egress section, click "Edit" to the right of Public network egress.

4. In the pop\-up dialog box, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e1c59ae708db1898c2211eb2a4bdad51.png) </span> or <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_80f23e8e15bbf3cbff72d06fa63083f0.png) </span>toggle to enable or disable the public network egress.

5. Click "OK" to complete the action.
