---
title: "Setting network mode for VPN gateways"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-setting-network-mode-for-vpn-gateways_1"
---

SealSuite VPN gateways support two distinct network modes to balance security and performance: **Full Tunnel Mode** and **Split Tunnel Mode**.


* **Full Tunnel Mode:**  When a user connects in this mode, **all** of their device's network traffic is routed through the VPN tunnel. This provides maximum security by encrypting all data but increases the load on the VPN node.

* **Split Tunnel Mode:**  When a user connects in this mode, only traffic destined for specific, pre\-defined corporate network resources is routed through the VPN tunnel. All other traffic (e.g., to public websites) goes directly through the user's local network. This conserves bandwidth, reduces load on the VPN node, and improves the user's general internet performance.


This guide explains how to configure which modes are available on a specific VPN node.

<span id="1fb95428"></span>
# Prerequisite

You can configure network modes for a VPN gateway only when the status of the VPN gateway is **Running**.

<span id="9e367106"></span>
# Procedure


1. Log in to the Admin Console.

2. In the left navigation bar, click **Zero Trust Access** \> **Gateway Config** \> **VPN Gateway**.

3. On the **VPN Gateway** page, click the card for the VPN node you want to configure.

4. Under the **Network Mode** tab, click **Edit**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97620f1ea5194e5d94aaa317989345ce~tplv-goo7wpa0wc-image.image) </span>

5. Choose which modes this VPN node should support. By default, **Full Tunnel Mode** and **Split Tunnel Mode** are selected. You can enable one or both.

6. (Optional) Configure **Split Tunnel Mode** Resources. If you enable **Split Tunnel Mode**, you must define which network resources should be routed through the VPN. You can configure these resources specifically for this individual node. For a detailed explanation of the difference between global and node\-specific resources, see [Managing split tunnel network resources](https://docs.byteplus.com/docs/sealsuite/docs-managing-split-tunnel-network-resources_1).

7. (Optional) Specify the effective scope for each mode.

   By default, any user who can see the VPN node can use any of its enabled modes. However, if both modes are enabled, you can restrict who is allowed to use each one.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">These changes will only take effect the next time a user connects to the VPN.   </div>
   

   1. Enable the **Specify the Effective Scope** toggle.

   2. Select the **Specify Global Mode visibility** or **Specify Split Tunnel Mode visibility** tab.

   3. Click  **+ Add Scope** and select the departments, roles, or individual users who should be able to use that specific mode.

   4. You can remove an object from the list at any time by clicking **Remove** in the **Action** column of its row.
