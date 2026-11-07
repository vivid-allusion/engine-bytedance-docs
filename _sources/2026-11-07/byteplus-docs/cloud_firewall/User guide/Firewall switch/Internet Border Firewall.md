---
title: "Internet Border Firewall"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Enabling-Internet-firewall"
---

Cloud Firewall helps protect traffic between the internet and your public IP assets. It minimizes the attack surface of public\-facing assets, lowers the risk of intrusions, and effectively blocks unauthorized outbound access from internal networks. After you enable the Cloud Firewall service, you can turn the Internet Firewall on or off for the public IP assets under your Volcengine account. This article explains how to enable or disable the Internet Firewall.

<span id="f1f5cd48"></span>
## Steps


1. Log in to [Cloud Firewall Console](https://console.byteplus.com/firewall/overview), and in the left navigation pane, click **Firewall Settings**.

2. On the **Firewall Settings** page, click **Internet Firewall**.

   * The **Public Asset List** displays the public IP assets across all regions. The displayed information includes: Asset IP/name, Region, 7\-Day peak traffic, Instance type, Status, and Firewall settings.

   * Public IP asset types include: ECS, CLB, NAT, ALB, HaVip, Network Interface, SSL VPN, WAF.

   * Click on the asset name to view the traffic trend chart of this public IP asset for the recent period.

3. You can **manually turn on the firewall switch, and newly added assets can be protected by enabling automatic protection for new assets**. After the asset firewall switch is turned on, the **firewall status** is updated to **protected** (indicating that the internet traffic in and out of the asset has been connected to the cloud firewall) or **unprotected** (indicating that the internet traffic in and out of the asset has not been connected to the cloud firewall).

   * You can turn on or off the internet perimeter firewall for single or multiple public IP assets as needed. Click the **operation** column on the right, and **turn the firewall switch** on or off for it.

   * The **automatic protection for new assets** switch is off by default. If you need to automatically turn on the firewall switch for future newly added **ECS** and **auxiliary network card** asset types, you can enable this feature.

4. Asset protection overview.

   * Unprotected: The number of public IP assets whose firewall switch is not turned on.

   * Protected: Shows the number of public IP assets with the firewall switch turned on.

   * Asset authorization specifications: The total specifications authorized for the firewall package, with the advanced version at 1000, the enterprise version at 2000, and the flagship version at 5000.

   * Total traffic peak bandwidth: The total traffic bandwidth of all public IP assets with the firewall switch currently turned on.

   * Bandwidth authorization specifications: The protection bandwidth specifications authorized for the firewall package.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">When turning the internet boundary firewall on and off, you do not need to change the current network topology; you can integrate and protect resources with a one\-click instant connection or disable protection without impacting business operations.</div>


2. <div data-tips="true" data-tips-type="tip">If the service traffic exceeds the protection bandwidth specifications of the internet boundary firewall, the cloud firewall will not guarantee security effectiveness, which may lead to network throttling, packet loss, and other issues. If you need greater traffic handling bandwidth, please expand in a timely manner.</div>
